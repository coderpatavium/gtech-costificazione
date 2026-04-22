# Dettagli Funzionalità

## 🎯 Modulo 1: Estrazione Dati PDF (COMPLETATO ✅)

### Cosa fa
Legge un PDF con lista di taglio e estrae automaticamente tutti i dati in formato Excel strutturato.

### Input
- Uno o più PDF in formato Zinetti Technologies
- Formato nome file: es. `Report_Ordini_20260226_102537.pdf`

### Processing
1. **Parsing Regex:** Cerca pattern "Cod." nel testo e estrae:
   - Codice articolo
   - Quantità
   - Materiale
   - Spessore
   - Peso
   - Dimensioni (Larghezza × Lunghezza)
   - Tempo di taglio (H:MM:SS)

2. **Elaborazione:**
   - Arrotondamento in eccesso dimensioni
   - Conversione tempo in Minuti:Secondi separati
   - Formattazione numeri all'italiana (virgola decimale)
   - Raggruppamento per famiglia (codici con _01, _02, _03)
   - Assegnazione lettere padre-figlio (A, B, C...)
   - Creazione automatica righe padre se mancanti

3. **Output Excel:**
   - Headers blu con testo bianco
   - Dati centrati e formattati
   - Colonne auto-dimensionate
   - Righe vuote tra famiglie diverse

### Output Colonne (in ordine)
| Num | Colonna | Descrizione |
|-----|---------|-------------|
| 1 | File PDF | Nome del file source |
| 2 | Codice | Codice articolo |
| 3 | Padre Figlio | Lettera (A, B, C...) per famiglia |
| 4 | Quantità | Numero pezzi |
| 5 | Larghezza | mm (arrotondato ceiling) |
| 6 | Lunghezza | mm (arrotondato ceiling) |
| 7 | Spessore | Numero netto |
| 8 | Materiale | Tipo materiale (es. Fe360Dec) |
| 9 | [Vuota] | Per annotazioni cliente |
| 10 | [Vuota] | Per annotazioni cliente |
| 11 | Minuti | Tempo taglio minuti |
| 12 | Secondi | Tempo taglio secondi |
| 13 | Peso | Kg (arrotondato all'italiano) |

### Esempi Output
```
File PDF | Codice | PF | Qty | Largh | Lungh | Spess | Materiale | [1] | [2] | Min | Sec | Peso
Report.pdf | 75015634-00_1 | A | 1 | 398 | 50 | 10 | Fe360Dec | | | 0 | 52 | 1,54
Report.pdf | 75015634-00_2 | A | 1 | 150 | 50 | 10 | Fe360Dec | | | 0 | 31 | 0,58
Report.pdf | 75015634-00 | A | | | | | | | | | | 
```

---

## 🔮 Modulo 2: Preventivatore DXF (IN SVILUPPO)

### Cosa farà
Stimerà il tempo di taglio da un file DXF senza fare il nesting completo.

### Input
1. **File DXF:** Disegno del pezzo (contorno + fori)
2. **Parametri:**
   - Materiale (Fe360, Inox, Alluminio...)
   - Spessore (mm)
   - Tipo taglio (Laser, Plasma, Waterjet - opzionale)

### Processing (da implementare)
1. **Parse DXF:**
   - Calcola perimetro totale (contorni + fori)
   - Conta numero sfondamenti (= numero contorni chiusi)
   - Estrae lunghezza totale in mm

2. **Applica Formula:**
```
Tempo_taglio = (Lunghezza_totale / Velocità_taglio) 
             + (N_sfondamenti × Tempo_sfondamento) 
             + Tempo_rapidi
```

3. **Stima Rapidi:**
   - Forfettario 5-10% del tempo di taglio
   - O calcolo basato su area della lamiera

### Output
```json
{
  "pezzo": "75015634-00_1.dxf",
  "materiale": "Fe360Dec",
  "spessore": 10,
  "perimetro_mm": 1245.5,
  "sfondamenti": 3,
  "tempo_taglio_min": 0.87,
  "tempo_taglio_sec": 52,
  "tempo_rapidi_sec": 5,
  "tempo_totale_sec": 57,
  "velocita_taglio": "1430 mm/min",
  "margine_errore": "±5%"
}
```

### Parametri Macchina (Tabella da customizzare)
```
Materiale | Spessore | Velocità (mm/min) | Tempo Sfondamento (sec)
Fe360 | 1 | 2500 | 0.8
Fe360 | 2 | 2400 | 0.9
Fe360 | 3 | 2300 | 1.0
Fe360 | 4 | 2200 | 1.1
Fe360 | 5 | 2000 | 1.2
Fe360 | 6 | 1800 | 1.3
Fe360 | 8 | 1500 | 1.5
Fe360 | 10 | 1430 | 1.7
Inox 304 | 1 | 2000 | 1.0
Inox 304 | 2 | 1900 | 1.1
Inox 304 | 3 | 1800 | 1.2
...
```

---

## 📱 Interfaccia Utente

### Modulo Estrazione (Attuale)
```
┌─────────────────────────────────────┐
│      ESTRAZIONE DATI TAGLIO          │
├─────────────────────────────────────┤
│  📄 Trascina PDF qui                 │
│     o clicca per selezionare         │
├─────────────────────────────────────┤
│  [🚀 Estrai e Scarica Excel]         │
│  [🗑️ Cancella]                       │
└─────────────────────────────────────┘
```

### Menu Futuro (Multi-Modulo)
```
┌──────────────────────────────────────┐
│  GTECH COSTIFICAZIONE                │
├──────────────────────────────────────┤
│  [ 1. Estrazione PDF ]  [ 2. DXF ]  │
├──────────────────────────────────────┤
│  ... contenuto modulo selezionato   │
└──────────────────────────────────────┘
```

---

## 🛠️ Configurazione Parametri (Futuro)

Interfaccia per customizzare la tabella dei parametri macchina:

```
┌─────────────────────────────────────────┐
│  PARAMETRI MACCHINA TAGLIO              │
├─────────────────────────────────────────┤
│  Materiale: [Fe360▼]                    │
│  Spessore: [10▼] mm                     │
│                                          │
│  Velocità taglio: [1430] mm/min         │
│  Tempo sfondamento: [1.7] secondi       │
│  Tempo rapidi: [5] % del taglio         │
│                                          │
│  [💾 Salva Parametri]                   │
│  [📋 Mostra Tabella Completa]           │
└─────────────────────────────────────────┘
```

---

## 📊 Formati Supportati

### Attualmente
- ✅ PDF (solo lettura testo)
- ✅ Excel (creazione)

### In Futuro
- 🔄 DXF (lettura geometria con ezdxf)
- ❓ STEP/IGES (se richiesto)
- ❓ JSON (export parametri)

---

*Ultimo aggiornamento: Aprile 2026*
