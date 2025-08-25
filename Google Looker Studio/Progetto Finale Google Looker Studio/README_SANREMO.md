
# Progetto Finale - Analisi Festival di Sanremo (1951-2023)

## Obiettivo

L'obiettivo di questo progetto è analizzare le edizioni del Festival di Sanremo dal 1951 al 2023 per individuare pattern, ricorrenze e anomalie. Il focus principale è stato capire se esiste una tendenza alla ripetitività tra **presentatori, vincitori e autori**, partendo dalla provocazione:  
**“Sanremo: le solite facce?”**

---

## Dataset

- `dati-festival-sanremo-1951-2023.xlsx` → Info su edizioni e presentatori
- `dati-classifica-sanremo-1951-2023.xlsx` → Classifiche, interpreti, autori
- `dati-canzoni-spotify-sanremo-1951-2023.xlsx` → non utilizzato (join non lineare / poco utile al tema)

---

## Scelte metodologiche

- F/NF: contati come presenze ma esclusi da piazzamenti (vittorie/podio/top10)
- Co-interpreti/ co-autori: contati singolarmente (una canzone può generare più crediti)
- Normalizzazione nomi: sostituito connettori con virgole, rimosso parentesi e spazi doppi

## Operazioni nel notebook (Python/pandas)

1) Caricamento e ispezione iniziale - controllo valori nulli o duplicati
2) Pulizia base
- Rimozione colonne inutili (`Unnamed: 0`)
- Conversione del campo `anno` in formato `datetime` per compatibilità con Looker Studio
- Estrazione numero da posizione (gestione 1°/2°); F/NF trattati come Nan

3) Explode: una riga per nome
- Creazione di due dataset "interpreti_expl" e "autori_expl" 

4) Esportazione
- Creazione di file puliti per Looker Studio:
  - `sanremo_classifica_clean.csv`
  - `sanremo_festival_clean.csv`
  - Autori (`sanremo_interpreti_exploded.csv`)
  - Interpreti (`sanremo_autori_exploded.csv`)

---

## Google Looker Studio

1) Caricamento dei CSV come sorgenti

2) Creazione campi calcolati
- Decennio
- Winner_flag (CASE WHEN posizione_num = 1 THEN 1 ELSE 0 END)

3) KPI (panoramica): Edizioni, Presentatori unici, interpreti unici, autori unici e vincitori.
4) Grafici temporali per evidenziare l'andamento dei partecipanti sia dalla parte degli autori che dalla parte degli artisti
5) Grafici a barre orizzontali necessari per la visualizzazione delle top 10 rispetto a diverse metriche
6) Tabelle pivot heatmap per evidenziare edizioni condotte e artisti vincitori per decenni
7) Filtri dinamici per lasciare libertà di esplorazione all'utente finale

---

## 👤 Autore

Valerio Metelli  
Bootcamp Epicode - Data Analysis  
Agosto 2025
