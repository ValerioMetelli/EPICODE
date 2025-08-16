
# Progetto Finale - Analisi Festival di Sanremo (1951-2023)

## Obiettivo

L'obiettivo di questo progetto è analizzare le edizioni del Festival di Sanremo dal 1951 al 2023 per individuare pattern, ricorrenze e anomalie. Il focus principale è stato capire se esiste una tendenza alla ripetitività tra **presentatori, vincitori e autori**, partendo dalla provocazione:  
**“Sanfemo: le solite facce?”**

---

## Dataset

Sono stati forniti tre file principali:
- `dati-festival-sanremo-1951-2023.xlsx` → Info su edizioni e presentatori
- `dati-classifica-sanremo-1951-2023.xlsx` → Classifiche, interpreti, autori
- `dati-canzoni-spotify-sanremo-1951-2023.xlsx` → Non utilizzato

---

## Operazioni svolte nel notebook

### Caricamento e ispezione iniziale
- Verifica della forma e della presenza di duplicati o valori nulli

### Pulizia dati
- Rimozione colonne inutili (`Unnamed: 0`)
- Conversione del campo `anno` in formato `datetime` per compatibilità con Looker Studio
- Pulizia della colonna `posizione`, gestione dei valori `F`, `NF` e conversione a interi

### Normalizzazione nomi
- Uniformati separatori come "e", "feat", "&", "-" in tutte le colonne di nomi
- Rimozione delle informazioni tra parentesi futili ai fini del report

### Estrazione multipli
- Creazione di colonne multiple per:
  - Interpreti (es. `interprete_1`, ..., `interprete_5`)
  - Autori (`autore_1`, ..., `autore_9`)
  
### Esportazione
- Creazione di file **“puliti”** per Looker Studio:
  - `CLASSIFICA.csv`
  - `PRESENTATORI.csv`
- Creazione di file **“esplosi”** (una riga per nome) per:
  - Autori (`AUTORI.csv`)
  - Interpreti (`INTERPRETI.csv`)


---

## Prossimi step

Caricamento dei file su **Google Looker Studio** per la realizzazione di una dashboard dinamica, visualizzando:
- Frequenze di partecipazione di singoli autori/interpreti/presentatori
- Evoluzione della struttura delle edizioni (numero partecipanti, durata, ecc.)
- Filtri interattivi per navigare tra le edizioni

---

## Autore

Valerio Metelli  
Bootcamp Epicode - Data Analysis  
Agosto 2025
