# GTECH Costificazione - Architettura della Soluzione

## 📋 Panoramica Generale

Applicazione web per automazione processi di taglio GTECH con due funzionalità principali:

### 1️⃣ **Modulo Estrazione Dati** (ATTIVO ✅)
Estrae automaticamente i dati dalle liste di taglio PDF generate dal software di nesting.

**Input:** PDF liste di taglio (formato Zinetti Technologies)  
**Output:** Excel strutturato con dati dei pezzi

**Colonne Output:**
- File PDF
- Codice
- Padre Figlio (lettera per raggruppamento famiglia)
- Quantità
- Larghezza (arrotondata in eccesso)
- Lunghezza (arrotondata in eccesso)
- Spessore (numero netto)
- Materiale
- [Colonna vuota 1]
- [Colonna vuota 2]
- Minuti
- Secondi
- Peso

---

### 2️⃣ **Modulo Preventivatore DXF** (IN SVILUPPO 🔄)
Stima il tempo di taglio direttamente da file DXF senza dover fare il nesting completo.

**Input:** 
- File DXF (del singolo pezzo o lamiera)
- Materiale (con tabella parametri)
- Spessore

**Output:** 
- Tempo di taglio stimato (±5%)
- Costo preventivato

**Formula di calcolo:**
```
Tempo Totale = (Lunghezza_taglio / Velocità_taglio) 
             + (N_sfondamenti × Tempo_sfondamento) 
             + (Tempo_rapidi % forfettario)
```

**Parametri necessari:**
- Velocità di taglio per materiale/spessore (mm/min)
- Tempo sfondamento per materiale/spessore (secondi)
- Velocità rapidi (stima forfettaria 5-10%)

---

## 🏗️ Architettura Tecnica

```
gtech-costificazione/
├── app.py                          # Backend Flask principale
├── requirements.txt                # Dipendenze Python
├── static/
│   └── index.html                  # Frontend web
├── README.md                        # Guida utente
├── ARCHITECTURE.md                 # Questo file
├── FEATURES.md                      # Dettagli funzionalità
└── ROADMAP.md                       # Piano di sviluppo
```

---

## 🔧 Stack Tecnologico

**Backend:**
- Flask (Python web framework)
- pdfplumber (estrazione testo PDF)
- ezdxf (parsing file DXF - per funzionalità futura)
- openpyxl (creazione Excel)

**Frontend:**
- HTML5
- CSS3
- JavaScript vanilla (niente framework)

**Hosting:**
- Render.com (deployment gratuito)
- GitHub (repository)

---

## 📊 Flusso Dati Attuale

### Estrazione PDF → Excel
```
PDF Upload 
  ↓
extract_raw_data() - Parsing regex
  ↓
organize_by_family() - Raggruppamento padre/figli
  ↓
create_excel() - Formattazione Excel
  ↓
Download Excel
```

---

## 🚀 Prossimi Passi

1. **Sviluppare Modulo Preventivatore:**
   - Parser DXF con ezdxf
   - Calcolo perimetro e sfondamenti
   - Tabella parametri macchina customizzabile
   - Interfaccia UI per upload DXF e selezione parametri

2. **Integrare con Modulo Estrazione:**
   - Menu principale per scegliere funzionalità
   - Persistenza parametri macchina

3. **Aggiungere Gestione Parametri:**
   - Form per settare velocità/tempi per materiale/spessore
   - Salvataggio locale (LocalStorage)

---

## 📝 Specifiche Completate

✅ Estrazione dati PDF liste di taglio  
✅ Raggruppamento padre-figlio automatico  
✅ Formattazione Excel professionale  
✅ Deploy su Render  

## 🔄 Specifiche in Sviluppo

🔄 Modulo Preventivatore DXF  
🔄 Tabella parametri macchina  
🔄 Interfaccia utente multilingue  

---

*Ultimo aggiornamento: Aprile 2026*
