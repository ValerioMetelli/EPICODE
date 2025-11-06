README – Preparazione Dataset e Analisi in Power BI “Prenotazioni
2022–2025 – Capital Rooms”

1.  Fase di pulizia e unione (Power Query – Excel) Obiettivo: unificare
    tutti i file mensili e annuali delle prenotazioni in un unico
    dataset coerente. Strumenti: Power Query (Excel)

Operazioni principali: 
	1. Importazione automatica da cartella di tutti i file .csv mensili. 
	2. Ispezione e uniformazione dei nomi colonna (date, importi, OTA, nazionalità, ecc.). 
	3. Rimozione di righe vuote, totali, intestazioni duplicate e note manuali. 
	4. Conversione dei formati (date, testi, numeri, valute). 
	5. Unione di tutti i mesi → per anno → in un unico dataset triennale. 
	6. Pulizia finale con normalizzazione dei valori numerici. 

Risultato: Prenotazioni_completo_pulito.xlsx, dataset unico pronto per la modellazione.

2.  Fase di normalizzazione e modellazione (Python – Pandas) Obiettivo:
    costruire un modello dati coerente in star schema. Strumenti: Python
    (Pandas)

Operazioni principali: 
- Rimozione caratteri speciali e simboli di valuta. 
- Creazione colonne logiche (id_status, lead_time, length_of_stay). 
- Correzione automatica dei record incoerenti (notti = 0 ma date valide). 
- Normalizzazione importi lordo/netto e gestione formati.

3.  Creazione delle tabelle di dimensione

-   D_cliente: ID, nome, telefono, nazionalità.
-   D_ota: ID OTA, piattaforma (Booking, Airbnb, Expedia, Privato).
-   D_stanza: ID stanza, nome, capienza.
-   D_status: ID status, descrizione (Confermata, Cancellata).

4.  Creazione delle tabelle di fatto

-   F_prenotazioni: 1 riga per prenotazione (check-in/out, notti,
    importi, OTA, stanza, cliente).
-   F_notti: 1 riga per notte (data, importo per notte, chiavi esterne).
    Le due tabelle sono collegate tramite le stesse FK per analisi
    temporali e metriche derivate.

5.  Esportazione finale e relazioni in Power BI Tutte le tabelle
    esportate in .csv e collegate in Power BI con relazioni uno-a-molti
    a direzione singola:

-   D_cliente → F_prenotazioni → F_notti
-   D_ota → F_prenotazioni → F_notti
-   D_stanza → F_prenotazioni → F_notti
-   D_status → F_prenotazioni

6.  Fase di Analisi e Visualizzazione (Power BI) Obiettivo: creare una
    dashboard interattiva per analizzare 3 anni di performance,
    stagionalità e canali di vendita. Strumenti: Power BI Desktop

Modello dati e KPI:
- Creata tabella calendario DAX completa (date, anno, mese, trimestre, stagionalità, weekend). 
- KPI principali calcolati con misure DAX personalizzate: 
- ADR = DIVIDE([Tot lordo], [Tot notti]) 
- RevPAR = DIVIDE([Tot lordo], [Tot notti disponibili]) 
- % Occupazione = DIVIDE([Tot notti], [Tot notti disponibili]) 
- Lead Time = AVERAGE([Giorni tra prenotazione e check-in]) 
- Length of Stay = AVERAGE([Notti]) 
Queste misure consentono analisi dinamiche per anno, OTA, nazionalità, stagione e tipo stanza.

Dashboard e Storytelling: Struttura in 5 pagine principali:
1. Overview: KPI generali (revenue, ADR, RevPAR, occupancy, lead time, cancellazioni) e grafici di sintesi. 
2. Performance & OTA: analisi mensile dei ricavi con focus su ADR per piattaforma (Booking, Airbnb, Expedia, Privato). 
3. Segmenti per Nazionalità: mappa interattiva + tabelle ranking dei paesi più redditizi. 
4. Stagionalità: analisi del comportamento degli ospiti (Lead time & LoS) e performance economiche per stagione. 
5. Conclusioni:sintesi visiva dei trend e raccomandazioni operative per migliorare la redditività.

Elementi avanzati: 
- Pulsanti di navigazione tra le pagine (effetto “sito web interattivo”). 
- Bottoni on/off per cambiare viste (“Performance economiche” / “Comportamento ospiti”). 
- Tooltip descrittivi e mini didascalie sotto i grafici per guidare la lettura. 
- Grafici chiave: barre, combo linee+colonne, mappe geografiche, grafici ad anello e diagrammi ad albero.

Pagina finale 
– Sintesi Strategica e Raccomandazioni Operative: 
- Sintesi dei principali trend 2021–2025 (stagionalità, mercati, OTA, ADR). 
- Tre azioni operative consigliate: 
1. Potenziare il canale diretto 
2. Ottimizzare la bassa stagione 
3. Diversificare i mercati 

-Footer: Analisi e visualizzazione a cura di Valerio Metelli · Dataset:
2021–2025
