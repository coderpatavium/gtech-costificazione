# ROADMAP di Sviluppo

## 📅 Fasi di Sviluppo

### ✅ FASE 1: MVP Estrazione PDF (COMPLETATA)
**Stato:** Completato e in produzione  
**Data:** Aprile 2026

**Deliverable:**
- ✅ Web app per estrazione dati da PDF liste di taglio
- ✅ Output Excel strutturato con 13 colonne
- ✅ Deploy su Render.com
- ✅ Raggruppamento padre-figlio automatico
- ✅ Formattazione all'italiana (virgola decimale)

**Collaudo:**
- ✅ Test con PDF reale (28 articoli estratti correttamente)
- ✅ Verifica excel output
- ✅ Test multi-file (più PDF in un'unica estrazione)

---

### 🔄 FASE 2: Modulo Preventivatore DXF (IN SVILUPPO)
**Stato:** Pianificazione  
**Stima:** 2-3 settimane di sviluppo

#### Sprint 2.1: Infrastruttura DXF
- [ ] Integrare libreria `ezdxf` in requirements.txt
- [ ] Creare endpoint `/api/estimate-dxf`
- [ ] Implementare parsing DXF:
  - [ ] Calcolo perimetro totale
  - [ ] Conteggio sfondamenti
  - [ ] Estrazione bounding box
- [ ] Unit test parser

#### Sprint 2.2: Logica di Stima
- [ ] Implementare formula di calcolo tempo
- [ ] Tabella parametri macchina in memoria
- [ ] Calcolo con margine ±5%
- [ ] Validazione input
- [ ] Test formula con dati reali

#### Sprint 2.3: UI Preventivatore
- [ ] Aggiungere tab "Preventivatore DXF" all'interfaccia
- [ ] Form upload DXF
- [ ] Dropdown materiale/spessore
- [ ] Visualizzazione risultati
- [ ] Download PDF preventivo (futuro)

#### Sprint 2.4: Gestione Parametri
- [ ] Interfaccia customizzazione parametri
- [ ] Salvataggio in localStorage
- [ ] Import/Export tabella parametri
- [ ] Preset per macchine comuni

---

### 📋 FASE 3: Integrazione e Polish
**Stato:** Non iniziata  
**Stima:** 1 settimana

- [ ] Menu principale per scegliere modulo
- [ ] UI responsive
- [ ] Gestione errori migliorata
- [ ] Help/Tutorial
- [ ] Documentazione API

---

### 🚀 FASE 4: Features Advanced (Opzionale)
**Stato:** Backlog

- [ ] Supporto STEP/IGES
- [ ] Calcolo costo automatico (con tariffe)
- [ ] Export PDF preventivo formale
- [ ] Multi-lingua (IT/EN)
- [ ] Database parametri macchina
- [ ] Storico preventivi
- [ ] Integrazione con gestionale (API)

---

## 📊 Timeline Stimata

```
APRILE 2026
├─ ✅ Fase 1 (Estrazione PDF) - COMPLETATA
│
MAGGIO 2026
├─ 🔄 Sprint 2.1 (Parser DXF) - IN PROGRESSO
├─ 🔄 Sprint 2.2 (Logica Stima) - IN PROGRESSO
│
GIUGNO 2026
├─ 🔄 Sprint 2.3 (UI Preventivatore)
├─ 🔄 Sprint 2.4 (Gestione Parametri)
│
LUGLIO 2026
├─ 📋 Fase 3 (Integrazione)
│
FINE LUGLIO 2026
└─ 🚀 V1.0 Completa
```

---

## 🎯 Criteri di Completamento

### Fase 2 - Preventivatore Considerato Completato Quando:

**Funzionalità:**
- [ ] Upload DXF funziona correttamente
- [ ] Parser DXF estrae geometria correttamente
- [ ] Formula stima entro ±5% dai dati reali
- [ ] Tabella parametri customizzabile
- [ ] Export risultati (Excel/PDF)

**Qualità:**
- [ ] Nessun bug critico
- [ ] UI intuitiva e responsive
- [ ] Documenti aggiornati
- [ ] Test con dati reali GTECH

**Collaudo Finale:**
- [ ] Test con 10+ DXF reali
- [ ] Confronto con nesting software ufficiale
- [ ] Feedback cliente approvato
- [ ] Performance acceptable (<2 sec upload)

---

## 🔧 Dipendenze e Prerequisiti

### Per Fase 2
```
pip install ezdxf==1.0.0
```

### Parametri Macchina Iniziali Richiesti
- Velocità di taglio per materiale/spessore
- Tempo sfondamento per materiale/spessore
- Tipo di macchina (Laser/Plasma/Waterjet)

**Da richiedere al cliente:**
- Tabella velocità/tempi della macchina reale
- Esempi DXF per testing
- Tolleranza massima errore (ora ±5%)

---

## 📝 Note Importanti

1. **Formula Tempo di Taglio:**
   - Viene considerato il perimetro totale (contorni + fori)
   - Numero sfondamenti = numero contorni chiusi nel DXF
   - Tempo rapidi stimato forfettariamente (5-10%)

2. **Margine ±5%:**
   - Accettabile per preventivi
   - Se serve più precisione: implementare nesting parziale

3. **Parametri Macchina:**
   - Variano molto per macchina
   - Devono essere customizzati con dati reali GTECH
   - Suggerire di creare preset per le macchine più comuni

4. **Scalabilità Futura:**
   - Progettare tabella parametri in modo estensibile
   - Preparare API per integrazione gestionale

---

## 🤝 Input Cliente Richiesti

Per procedere con la Fase 2:

1. **Tabella Velocità Taglio:**
   ```
   Materiale | Spessore | Velocità (mm/min) | Tempo Sfondamento (sec)
   ```

2. **File DXF di Test:**
   - Almeno 5 esempi reali GTECH
   - Con tempo reale misurato per validazione

3. **Approvazione Scope:**
   - ✅ Formula ±5% accettabile?
   - ✅ Priorità: UI o estensioni extra?

---

*Ultimo aggiornamento: 22 Aprile 2026*
