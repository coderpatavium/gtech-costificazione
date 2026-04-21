# Estrazione Dati Taglio - GTECH

Web app per estrazione automatica di dati dalle liste di taglio PDF e generazione di file Excel.

## 🎯 Funzionalità

- ✅ Upload di uno o più PDF
- ✅ Estrazione automatica di: Codice, Quantità, Dimensioni, Materiale, Tempo di taglio
- ✅ Generazione di Excel strutturato pronto per l'uso
- ✅ Eliminazione dell'inserimento manuale

## 📋 Dati Estratti

Per ogni pezzo nel PDF, il sistema estrae:
- **Codice**: Codice articolo
- **Quantità**: Q.tà
- **Larghezza**: Prima dimensione (da "Dimensioni LxH")
- **Lunghezza**: Seconda dimensione
- **Spessore**: Spessore del materiale
- **Materiale**: Tipo di materiale (es. Fe360Dec)
- **Minuti**: Minuti di tempo di taglio
- **Secondi**: Secondi di tempo di taglio

## 🚀 Installazione e Avvio

### Prerequisiti
- Python 3.8+
- pip

### Setup

1. **Installa le dipendenze:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Avvia l'app:**
   ```bash
   python app.py
   ```

3. **Accedi all'interfaccia:**
   ```
   http://localhost:5000
   ```

## 📱 Utilizzo

1. Apri il browser a `http://localhost:5000`
2. Trascina uno o più PDF nell'area di caricamento (o clicca per selezionare)
3. Premi il pulsante "Estrai e Scarica Excel"
4. L'Excel verrà scaricato automaticamente con i dati estratti

## 📂 Struttura del Progetto

```
project/
├── app.py                 # Backend Flask
├── requirements.txt       # Dipendenze Python
├── static/
│   └── index.html        # Frontend web
└── README.md
```

## ⚙️ Configurazione

Per cambiare la porta di ascolto, modifica l'ultima riga di `app.py`:
```python
app.run(debug=True, host='0.0.0.0', port=5000)  # Cambia 5000 con la porta desiderata
```

## 🔧 Troubleshooting

### "ModuleNotFoundError: No module named 'flask'"
Installa nuovamente le dipendenze:
```bash
pip install -r requirements.txt --upgrade
```

### L'app si avvia ma non riesco ad accedere
Controlla che la porta 5000 sia disponibile. Se occupata, cambia la porta in `app.py`.

## 📝 Note

- I file PDF devono seguire il formato standard di Zinetti Technologies
- L'app supporta upload multipli (elabora tutti i file in una sola operazione)
- L'Excel generato ha headers formattati e colonne auto-dimensionate

## 👤 Sviluppato per

GTECH Costificazione - Automazione processo di estrazione dati dalle liste di taglio
