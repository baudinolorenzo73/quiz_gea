# Simulatore GEA PWA — versione 5.5

Banca JSON esterna inclusa nel pacchetto: **374 domande chiuse** e **107 domande aperte** valide dopo il controllo automatico dei doppioni.

## Pubblicazione su GitHub Pages

1. Crea un repository GitHub oppure apri quello destinato al simulatore.
2. Carica **il contenuto di questa cartella nella radice del repository**: `index.html`, `manifest.webmanifest`, `sw.js` e le cartelle `icons` e `data`.
3. In GitHub apri **Settings → Pages**.
4. In **Build and deployment** scegli **Deploy from a branch**.
5. Seleziona il branch `main`, cartella `/ (root)`, quindi **Save**.
6. Apri l’indirizzo fornito da GitHub Pages. In Chrome/Android sono disponibili i pulsanti **Installa** e **Aggiorna**. Installa aggiunge la PWA al dispositivo; Aggiorna controlla e ricarica la versione pubblicata più recente.

La PWA richiede HTTPS o `localhost`; aprendo `index.html` direttamente il simulatore funziona, ma l’installazione e il service worker non si attivano.

## Aggiornamenti

Quando modifichi i file, cambia `CACHE_NAME` in `sw.js` (per esempio `simulatore-gea-v5.5.1`) per forzare il rinnovo della cache sui dispositivi.

## Banca JSON esterna

Le domande sono nel file `data/domande.json`, che normalmente viene pubblicato insieme agli altri file. Se manca, l’app chiede l’indirizzo HTTPS del JSON su GitHub e può usarlo online in sola lettura. È accettato sia l’indirizzo `raw.githubusercontent.com` sia quello GitHub con `/blob/`, che viene convertito automaticamente.

Dopo il caricamento online, **Salva offline e scarica JSON** conserva una copia operativa nella memoria della PWA, abilita l’editor e scarica anche un backup. Il browser sceglie la destinazione del backup secondo le proprie impostazioni. La copia operativa non dipende dalla posizione del file scaricato.

## Modalità del test

È possibile scegliere **Completo**, **Solo chiuse** o **Solo aperte**, il numero di domande e l’estrazione **proporzionale alle ore**, **RND** oppure **per argomento**. Ogni domanda può essere lasciata vuota; i pulsanti **Precedente** e **Successiva** consentono di tornare indietro e modificare le risposte prima della conclusione.

Tutte le opzioni secondarie sono raccolte in **Configurazione del test**. Ogni domanda mostra inoltre il proprio numero nella banca, per esempio `25/374`; lo stesso riferimento appare nella correzione e nell’editor. Nell’editor è possibile cercare direttamente il numero `25` oltre al testo.

La versione 5.5 distingue le domande **sicure** dalle **quasi sicure**. Quando le prioritarie sono abilitate, la domanda sicura di sintesi sull'ecologia viene sempre inserita nel test aperto; le altre completano il limite configurato di otto prioritarie.

## Banca dati modificabile

In **Banca dati, editor e importazione** puoi aggiungere o correggere domande a mano, importare JSON e scaricare un backup completo. Il file esportato può sostituire `data/domande.json` nel repository: in questo modo le modifiche diventano permanenti per tutti. Le modifiche non ancora pubblicate restano nel browser; il backup è consigliato prima di cambiare dispositivo, browser o cancellare i dati del sito.

## Percentuali e test mirato

La schermata iniziale mostra percentuale di risposte corrette, risposte date e quota da recuperare, oltre al dettaglio per argomento. Da qui è possibile avviare un test mirato sugli errori oppure azzerare percentuali e storico locale.

## Controllo delle ripetizioni

In **Configurazione del test** si può scegliere di evitare le domande già utilizzate nelle ultime 0–8 sessioni; il valore predefinito è 5. La sessione viene registrata appena le domande sono estratte, quindi anche un test interrotto viene conteggiato. Il controllo confronta sia l’identificativo sia il testo normalizzato, così intercetta anche un eventuale doppione salvato con un altro ID. Se non rimangono abbastanza quesiti, riutilizza solo quelli strettamente necessari partendo dai meno recenti. Il test mirato può riproporre intenzionalmente le domande sbagliate. Il pulsante **Azzera memoria ripetizioni** non modifica percentuali e risultati.
