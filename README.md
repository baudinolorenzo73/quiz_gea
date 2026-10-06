# Simulatore GEA PWA — versione 4.0

Banca incorporata: **358 domande chiuse** e **100 domande aperte**.

## Pubblicazione su GitHub Pages

1. Crea un repository GitHub oppure apri quello destinato al simulatore.
2. Carica **il contenuto di questa cartella nella radice del repository**: `index.html`, `manifest.webmanifest`, `sw.js` e la cartella `icons`.
3. In GitHub apri **Settings → Pages**.
4. In **Build and deployment** scegli **Deploy from a branch**.
5. Seleziona il branch `main`, cartella `/ (root)`, quindi **Save**.
6. Apri l’indirizzo fornito da GitHub Pages. In Chrome/Android comparirà il pulsante **Installa** quando il browser rende disponibile l’installazione.

La PWA richiede HTTPS o `localhost`; aprendo `index.html` direttamente il simulatore funziona, ma l’installazione e il service worker non si attivano.

## Aggiornamenti

Quando modifichi i file, cambia `CACHE_NAME` in `sw.js` (per esempio `simulatore-gea-v4.0.1`) per forzare il rinnovo della cache sui dispositivi.
