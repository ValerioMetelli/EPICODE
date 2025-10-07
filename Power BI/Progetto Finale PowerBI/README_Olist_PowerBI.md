# 📘 Olist Store – Sales Overview 2016–2018

**Autore:** Valerio Metelli  
**Strumento:** Microsoft Power BI  

---

## 🎯 Obiettivo

Analizzare l’andamento delle vendite, dei ricavi e della soddisfazione clienti di **Olist Store** nel triennio 2016–2018, attraverso un modello dati relazionale e un report interattivo costruito in Power BI.

---

## 🧩 Dataset utilizzati

L’analisi si basa sui principali file del dataset **Olist**:
- olist_orders_dataset.csv  
- olist_order_items_dataset.csv  
- olist_order_payments_dataset.csv  
- olist_order_reviews_dataset.csv  
- olist_products_dataset.csv  
- product_category_name_translation.csv  
- olist_customers_dataset.csv  
- olist_sellers_dataset.csv  
- olist_geolocation_dataset.csv  

---

## ⚙️ Pulizia e modellazione (Power Query)

In **Power Query** ho effettuato una prima fase di pulizia e selezione delle colonne utili all’analisi:
- Eliminazione di campi ridondanti o nulli.  
- Uniformazione dei nomi delle colonne e formati data.  
- Creazione della tabella **Calendar** con colonne per anno, mese e descrizione mese.  

Il modello è stato impostato con **schema a stella**, con le principali relazioni:
- Calendar 1 to n Order Date  
- Customers 1 to 1 Order Date  
- Order Date 1 to n Review  
- Order Date 1 to n Order Price  
- Products 1 to n Order Price  

---

## 🧮 Principali misure DAX

Nel modello ho creato varie misure per analizzare KPI di vendita, performance e rating.  
Tra le principali:

- `%ConteggioOrdini = DIVIDE([Order Items]-[Order Items PY], [Order Items PY])`
- `Delivered % = DIVIDE(CALCULATE(DISTINCTCOUNT('ORDER DATE'[order_id]),'ORDER DATE'[order_status] = "delivered"),DISTINCTCOUNT('ORDER DATE'[order_id]))`
- `Freight % = DIVIDE(SUM('ORDER PRICE'[freight_value]), [Revenue])`
- `Order Items = COUNTA('ORDER PRICE'[order_item_id])`
- `Order Items % VAR = DIVIDE([Order Items] - [Order Items PY], [Order Items PY])`
- `Order Items PY = CALCULATE([Order Items], PARALLELPERIOD('CALENDAR'[Date], -12, MONTH))`
- `Revenue = SUMX('ORDER PRICE', 'ORDER PRICE'[price] + 'ORDER PRICE'[freight_value])`
- `Revenue % VAR = DIVIDE([Revenue] - [Revenue PY], [Revenue PY])`
- `Revenue PY = CALCULATE([Revenue], PARALLELPERIOD('CALENDAR'[Date], -12, MONTH))`

---

## 📊 Visualizzazioni e struttura report

Il report è composto da **4 pagine principali**, navigabili tramite pulsanti interattivi:

### 🏠 Home
- KPI principali (Avg Ticket, Freight %, Avg Review, Delivered %).  
- Grafico *Top 10 categorie per ricavi*.  
- Grafico ad anello *Distribuzione ricavi per stato cliente*.  

### 📦 Andamento Ordini
- KPI: ordini totali, ordini anno precedente, variazione %.  
- Grafico combinato barre/linea per analisi mensile.  

### 💰 Andamento Ricavi
- KPI: revenue, revenue PY, var% YoY.  
- Grafico combinato per confronto mensile.  

### ⭐ Distribuzione Rating
- KPI: numero recensioni e valutazione media.  
- Grafico combinato (media punteggi + volume recensioni).  
- Grafico a torta con distribuzione punteggi 1–5.  

---

## 🧾 Conclusione

Il progetto fornisce una visione chiara dell’evoluzione delle performance di **Olist Store** nel triennio, mettendo in relazione andamento delle vendite, ricavi e soddisfazione clienti.  
La dashboard consente di esplorare i dati in modo interattivo e di identificare pattern stagionali, categorie top e aree geografiche più performanti.
