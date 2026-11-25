# turni iDEAli · Guida passo passo

Sito per raccogliere, in forma anonima, i turni che i colleghi con diritto all'aspettativa potrebbero lavorare al posto dell'aspettativa.

- **index.html**: il sito per i colleghi (telefono e computer).
- **admin.html**: l'area di gestione (computer e telefono), protetta da accesso.
- **config.js**: i dati del progetto Firebase.
- **regole-firestore.txt**: le regole di sicurezza da pubblicare su Firebase.
- **hero.webp, esterno.webp**: le foto del pronto soccorso.
- **turni-iDEAli-Registro.xlsx**: il Registro da tenere solo sul computer della coordinatrice.

Servono circa 30-40 minuti la prima volta. I nomi dei menu di GitHub e Firebase possono cambiare leggermente nel tempo: se non trovi una voce identica, cerca quella con il significato più vicino.

---

## 0. Prima di tutto: prova senza Firebase

Finché in **config.js** c'è scritto `INCOLLA_QUI`, il sito funziona in **modalità prova**: tutto resta nel browser che stai usando e non va su internet.

1. Pubblica i file su GitHub come al punto 1.
2. Apri **admin.html**, entra con qualsiasi email e password, fai la configurazione iniziale e genera qualche codice.
3. Nello stesso browser apri **index.html** e prova a inviare le disponibilità con uno di quei codici.
4. In Impostazioni della gestione ci sono «Dati di prova» e «Azzera la prova».

Quando sei pronto, passa ai punti 2-4 per collegare Firebase.

---

## 1. Pubblicare il sito su GitHub Pages

1. Su github.com crea un nuovo repository chiamato `turni-dea-li` (pubblico; i dati non stanno nel repository ma su Firebase).
2. Nel repository: **Add file > Upload files**. Trascina **tutti** i file di questa cartella (tranne questo LEGGIMI, se preferisci, e il Registro Excel: **il Registro non va mai caricato su GitHub**). Conferma con **Commit changes**.
3. Vai in **Settings > Pages**. In «Build and deployment» scegli **Deploy from a branch**, ramo **main**, cartella **/ (root)**, poi **Save**.
4. Dopo uno o due minuti il sito è online a un indirizzo del tipo:
   - colleghi: `https://TUONOME.github.io/turni-dea-li/`
   - gestione: `https://TUONOME.github.io/turni-dea-li/admin.html`

---

## 2. Creare il progetto Firebase (piano gratuito Spark)

1. Vai su console.firebase.google.com e crea un **nuovo progetto** (per esempio `turni-dea-li`). Google Analytics non serve.
2. **Firestore Database > Crea database.** Scegli la modalità **produzione** e una posizione in Europa (le posizioni «eur3» o «europe-west…»). La posizione non si può cambiare dopo.
3. **Authentication > Inizia > Email/password**: attivalo (solo il primo interruttore, non il «link via email»).
4. **Authentication > Utenti > Aggiungi utente**: crea l'account della gestione con l'email della coordinatrice e una password robusta. Se serve, crea un secondo account per te.
5. Nella tabella degli utenti copia l'**UID** di ciascun account (colonna «UID utente»): ti serve al punto 4.
6. **Authentication > Impostazioni > Domini autorizzati**: aggiungi `TUONOME.github.io`. Se l'accesso alla gestione dovesse dare un errore di dominio, il motivo è questo.

---

## 3. Collegare il sito a Firebase (config.js)

1. **Impostazioni progetto** (ingranaggio) **> Le tue app > icona `</>`** (app web). Dai un nome, non serve Firebase Hosting.
2. Firebase mostra un blocco `firebaseConfig` con `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`.
3. Apri **config.js** e sostituisci ogni `INCOLLA_QUI…` con il valore corrispondente. Lascia le virgolette.
4. Carica di nuovo **config.js** su GitHub (Add file > Upload files, sovrascrive il precedente).

Questi valori non sono segreti: la protezione dei dati la fanno le regole del punto 4.

---

## 4. Pubblicare le regole di sicurezza

1. Apri **regole-firestore.txt**.
2. Sostituisci `UID_GESTIONE_1` con l'UID dell'account della coordinatrice. Se hai un secondo account, sostituisci `UID_GESTIONE_2`; altrimenti lascialo com'è.
3. In Firebase: **Firestore Database > Regole**. Cancella tutto, incolla il contenuto del file, premi **Pubblica**.

Cosa fanno le regole:
- i colleghi possono solo **scrivere** la propria risposta, con un codice valido e attivo, a raccolta aperta e prima della chiusura (ora del server);
- ogni risposta è controllata: figura uguale a quella del codice, giorni del mese giusto, solo turni M, P, N, massimo non superiore ai turni scelti, nota di 200 caratteri al massimo;
- **nessun collega può leggere** le risposte, nemmeno la propria; solo gli account della gestione leggono tutto;
- sul server ci sono solo le **impronte** dei codici, mai i codici in chiaro e mai i nomi.

---

## 5. Primo avvio della gestione

1. Apri **admin.html** ed entra con l'account della coordinatrice.
2. Compare **Configurazione iniziale**: scrivi il nome del reparto e il primo mese. Il sito crea le impostazioni e la prima raccolta.
3. In **Impostazioni** controlla orari dei turni, festivi (aggiungi il patrono toccando il giorno) e data di chiusura (di norma il 10 del mese precedente alle 23:59).

---

## 6. Codici e Registro

1. **Codici > Genera**: scegli quanti codici e la figura (INF o OSS).
2. **Subito**: «Scarica l'elenco». Il codice in chiaro si vede solo in questo momento.
3. Apri **turni-iDEAli-Registro.xlsx** sul computer. Nel foglio **Codici** incolla codice, impronta e figura (colonne A, B, C) e scrivi **cognome e nome** nella colonna D. Togli la riga di esempio.
4. **Stampa i bigliettini** e consegnali a mano, uno per persona.
5. Se un codice viene passato ad altri: **Codici > Sostituisci**. Il vecchio smette di funzionare; aggiorna il Registro con il nuovo.

Il Registro è l'unico file che collega i codici alle persone: tienilo in una cartella protetta e non caricarlo mai online.

---

## 7. Ogni mese

1. **Raccolte > Nuova**: crea il mese (puoi aprire fino a sei mesi prima). Festivi, tema e chiusura si impostano da soli.
2. **Da coprire**: per ogni giorno con turni scoperti scrivi quanti turni servono per figura. Lascia «?» se non lo sai ancora.
3. **Calendario**: a colpo d'occhio vedi dove le disponibilità bastano (verde), sono al limite (giallo) o mancano (rosso). Tocca un giorno per vedere chi si è offerto e in quale ordine.
4. **Esporta** (icona di download): scarica `turni-ideali-AAAA-MM.xlsx`, anonimo.
5. Nel Registro: apri il file scaricato, seleziona tutto, copia; nel foglio **Incolla qui** clicca A1 e incolla. «Risultati», «Per persona» e «Per giorno» si aggiornano con i nomi.
6. In alternativa, nella gestione **Carica il Registro**: vedi i nomi direttamente nella pagina, senza inviarli al server. Spariscono quando chiudi la pagina.

Il «totale anonimo» mostrato ai colleghi nella conferma si aggiorna ogni volta che la gestione apre quel mese.

---

## 8. Controlli da fare dopo la pubblicazione

Le regole non sono state provate su un Firebase reale (nell'ambiente di sviluppo non era disponibile l'emulatore). Bastano dieci minuti:

1. In una finestra anonima apri il sito dei colleghi e inserisci un codice inventato: deve essere **rifiutato**.
2. Con un codice vero invia delle disponibilità: deve comparire **«Disponibilità registrate»**.
3. In Firebase, **Firestore Database > Dati**: apri `raccolte > mese > risposte`. Il nome del documento deve essere una lunga sequenza di lettere e numeri (l'impronta), **non** il codice.
4. Nella gestione chiudi la raccolta e prova a inviare dal sito dei colleghi: deve essere **rifiutato** (se la pagina era già aperta, compare un messaggio di errore).
5. In **Firestore Database > Regole** c'è un simulatore (Rules Playground): simula una lettura (`get`) **non autenticata** di `raccolte/AAAA-MM/risposte/QUALSIASI`. Deve essere **negata**.
6. Se l'accesso alla gestione dice «Accesso non autorizzato», l'UID nelle regole non corrisponde: ricontrolla il punto 4.

Se uno di questi controlli non dà il risultato atteso, non distribuire i codici e scrivimi cosa vedi.

---

## 9. Aggiornamenti

Negli aggiornamenti ti mando solo i file cambiati e ti dico ogni volta se devi **ripubblicare le regole** di Firestore. Per sostituire un file su GitHub basta caricarlo di nuovo con lo stesso nome.

## Note tecniche

- Nessuna libreria esterna, tranne Firebase caricato dal sito ufficiale Google (versione indicata in config.js). I file Excel sono creati e letti direttamente dal sito.
- Funziona con le versioni recenti di Safari, Chrome, Edge e Firefox. La vibrazione funziona solo su Android: l'iPhone non la consente ai siti web.
- Le guide si riaprono dal pulsante «?». Suoni e vibrazione si spengono dall'altoparlante.
