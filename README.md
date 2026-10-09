# Simulatore GEA PWA — versione 5.7

Banca JSON esterna inclusa nel pacchetto: **374 domande chiuse** e **107 domande aperte** valide dopo il controllo automatico dei doppioni.

## Pubblicazione su GitHub Pages

1. Crea un repository GitHub oppure apri quello destinato al simulatore.
2. Carica **il contenuto di questa cartella nella radice del repository**: `index.html`, `manifest.webmanifest`, `sw.js` e le cartelle `icons` e `data`.
3. In GitHub apri **Settings → Pages**.
4. In **Build and deployment** scegli **Deploy from a branch**.
5. Seleziona il branch `main`, cartella `/ (root)`, quindi **Save**.
6. Apri l’indirizzo fornito da GitHub Pages. In Chrome/Android sono disponibili i pulsanti **Installa** e **Aggiorna**. Installa aggiunge la PWA al dispositivo; Aggiorna controlla e ricarica la versione pubblicata più recente.

La PWA richiede HTTPS o `localhost`. Non aprire direttamente `index.html` con `file://`: il caricamento del JSON e la cache offline possono essere bloccati dal browser.

## Aggiornamenti

Quando modifichi i file, cambia `CACHE_NAME` in `sw.js` (per esempio `simulatore-gea-v5.6.1`) per forzare il rinnovo della cache sui dispositivi.

## Banca JSON esterna

Le domande sono nel file `data/domande.json`, che normalmente viene pubblicato insieme agli altri file. Se manca, l’app chiede l’indirizzo HTTPS del JSON su GitHub e può usarlo online in sola lettura. È accettato sia l’indirizzo `raw.githubusercontent.com` sia quello GitHub con `/blob/`, che viene convertito automaticamente.

Dopo il caricamento online, **Salva offline e scarica JSON** conserva una copia operativa nella memoria della PWA, abilita l’editor e scarica anche un backup. Il browser sceglie la destinazione del backup secondo le proprie impostazioni. La copia operativa non dipende dalla posizione del file scaricato.

## Modalità del test

È possibile scegliere **Completo**, **Solo chiuse** o **Solo aperte**, il numero di domande e l’estrazione **proporzionale alle ore**, **RND** oppure **per argomento**. Ogni domanda può essere lasciata vuota; i pulsanti **Precedente** e **Successiva** consentono di tornare indietro e modificare le risposte prima della conclusione.

Tutte le opzioni secondarie sono raccolte in **Configurazione del test**. Ogni domanda mostra inoltre il proprio numero nella banca, per esempio `25/374`; lo stesso riferimento appare nella correzione e nell’editor. Nell’editor è possibile cercare direttamente il numero `25` oltre al testo.

La versione 5.6 distingue le domande **sicure** dalle **quasi sicure**. Quando le prioritarie sono abilitate, la domanda sicura di sintesi sull'ecologia viene sempre inserita nel test aperto; le altre completano il limite configurato di otto prioritarie.

## Banca dati modificabile

In **Banca dati, editor e importazione** puoi aggiungere o correggere domande a mano, importare JSON e scaricare un backup completo. Il file esportato può sostituire `data/domande.json` nel repository: in questo modo le modifiche diventano permanenti per tutti. Le modifiche non ancora pubblicate restano nel browser; il backup è consigliato prima di cambiare dispositivo, browser o cancellare i dati del sito.

## Percentuali e test mirato

La schermata iniziale mostra percentuale di risposte corrette, risposte date e quota da recuperare, oltre al dettaglio per argomento. Da qui è possibile avviare un test mirato sugli errori oppure azzerare percentuali e storico locale.

## Controllo delle ripetizioni

In **Configurazione del test** si può scegliere di evitare le domande già utilizzate nelle ultime 0–8 sessioni; il valore predefinito è 5. La sessione viene registrata appena le domande sono estratte, quindi anche un test interrotto viene conteggiato. Il controllo confronta sia l’identificativo sia il testo normalizzato, così intercetta anche un eventuale doppione salvato con un altro ID. Se non rimangono abbastanza quesiti, riutilizza solo quelli strettamente necessari partendo dai meno recenti. Il test mirato può riproporre intenzionalmente le domande sbagliate. Il pulsante **Azzera memoria ripetizioni** non modifica percentuali e risultati.

## Novità 5.6 — 9 ottobre 2026

- DB normalizzato: 374 chiuse + 107 aperte = 481 quesiti; conservati gli ID e l'ordine precedente. I record grezzi che la versione 5.5 già escludeva non fanno più parte del JSON operativo; l'archivio precedente resta recuperabile dalla cronologia.
- Versione DB indipendente dalla versione app: 2026.10.09-1, con data aggiornamento.
- Copia offline prioritaria all'avvio. Il pulsante Aggiorna banca dati scarica dal JSON GitHub configurato, oppure dal JSON del progetto, mantenendo le modifiche locali.
- In caso di errore di rete o JSON non valido, la banca già caricata non viene svuotata.
- Aggiornamento PWA: vengono eliminate soltanto le vecchie cache del simulatore; la cache utente e le altre app non vengono cancellate.
- Il JSON è opzionale per l'installazione. Se manca, puoi configurare GitHub oppure importare un JSON completo dalla sezione banca dati.
- Pulsanti Configura JSON GitHub e Come pubblicare le modifiche: lettura pubblica senza token; modifica remota dal proprio account GitHub, non dalla PWA.
- Fonti: 213 chiuse e 71 aperte hanno almeno una pagina PDF. Le pagine mancanti non sono state ricostruite o inventate. Il frammento #page può non essere rispettato da tutti i visualizzatori Drive.

La normalizzazione è un controllo strutturale, non una verifica scientifica di tutte le risposte. Nessuna nuova domanda è stata aggiunta in questo aggiornamento.

Prima di aggiornare, esporta banca JSON e storico: le cache del browser possono essere eliminate dal sistema o dall'utente. Le correzioni locali sovrascrivono la versione pubblica della stessa domanda finché non sono pubblicate o rimosse; sono conservate in questo browser, non sincronizzate automaticamente.

Verifiche eseguite: sintassi JavaScript, JSON, risposta corretta unica, unicità ID, controllo doppioni con l'algoritmo dell'app; test automatici dei percorsi di caricamento e del service worker. Non eseguita una prova d'installazione su dispositivo Android reale.

## Novità 5.7 — ripresa di una sessione sospesa

Domande estratte, ordine delle opzioni, risposte chiuse, testo aperto, posizione, modalità e tempo residuo vengono salvati automaticamente in questo browser. Il salvataggio avviene a ogni risposta e navigazione, periodicamente durante il timer e quando si lascia la pagina.

Alla riapertura scegli **Riprendi test** oppure **Ricomincia con un nuovo test**. Riprendi non estrae nuove domande e non registra una nuova sessione nella memoria antiripetizione. Ricomincia chiede conferma prima di cancellare il test sospeso e torna alla configurazione; lo storico precedente resta disponibile. La schermata di correzione intermedia viene ripristinata. Al completamento il salvataggio provvisorio viene eliminato.

Il tempo va in pausa quando l'app passa in secondo piano o viene chiusa; riprende tornando al test. Anche le risposte aperte vengono conservate temporaneamente per questa funzione, indipendentemente dall'opzione per salvarle nello storico finale. Non viene inviato nulla online.

Il ripristino vale per lo stesso browser, dispositivo e indirizzo del sito. Non recupera test chiusi nelle versioni precedenti, che non salvavano la sessione. Cancellazione dati del browser o modalità privata possono impedire il recupero. Se il salvataggio fallisce, l'app mostra un avviso. In caso di arresto improvviso il timer può perdere gli ultimi cinque secondi di aggiornamento.

Verifiche 5.7: sintassi, validazione snapshot, ripresa di risposta chiusa e testo aperto, posizione, ordine opzioni, ID sessione, tempo in pausa, correzione intermedia e scarto di salvataggi corrotti. Prova browser automatica non eseguita: il browser di test non è installato nell'ambiente.
