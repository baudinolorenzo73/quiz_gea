# Simulatore GEA PWA — versione 4.4

Banca incorporata: **358 domande chiuse** e **100 domande aperte**.

## Pubblicazione su GitHub Pages

1. Crea un repository GitHub oppure apri quello destinato al simulatore.
2. Carica **il contenuto di questa cartella nella radice del repository**: `index.html`, `manifest.webmanifest`, `sw.js` e la cartella `icons`.
3. In GitHub apri **Settings → Pages**.
4. In **Build and deployment** scegli **Deploy from a branch**.
5. Seleziona il branch `main`, cartella `/ (root)`, quindi **Save**.
6. Apri l’indirizzo fornito da GitHub Pages. In Chrome/Android sono disponibili i pulsanti **Installa** e **Aggiorna**. Installa aggiunge la PWA al dispositivo; Aggiorna controlla e ricarica la versione pubblicata più recente.

La PWA richiede HTTPS o `localhost`; aprendo `index.html` direttamente il simulatore funziona, ma l’installazione e il service worker non si attivano.

## Aggiornamenti

Quando modifichi i file, cambia `CACHE_NAME` in `sw.js` (per esempio `simulatore-gea-v4.4.1`) per forzare il rinnovo della cache sui dispositivi.

## Modalità del test

È possibile scegliere **Completo**, **Solo chiuse** o **Solo aperte**. Ogni domanda può essere lasciata vuota; i pulsanti **Precedente** e **Successiva** consentono di tornare indietro e modificare le risposte prima della conclusione.

## Percentuali e test mirato

La schermata iniziale mostra percentuale di risposte corrette, risposte date e quota da recuperare, oltre al dettaglio per argomento. Da qui è possibile avviare un test mirato sugli errori oppure azzerare percentuali e storico locale.

## Controllo delle ripetizioni

In **Configurazione** si può scegliere di evitare le domande già utilizzate nelle ultime 0–8 sessioni; il valore predefinito è 5. Se non rimangono abbastanza quesiti, il simulatore riutilizza quelli necessari. Il test mirato può riproporre intenzionalmente le domande sbagliate. Il controllo usa gli identificativi registrati dalla versione 4.4 in poi.
