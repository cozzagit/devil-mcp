# Strumenti del server MCP di DeviL

Generato dalla definizione degli strumenti sul server. I livelli sono cumulativi: ogni livello comprende gli strumenti dei precedenti.


## Base


### `panoramica`

Situazione dell’organizzazione su DeviL: piano e limiti, zona, numeri (aziende, analizzate, bozze pronte, in coda) e le prossime 10 mosse consigliate. Usalo per primo.

_Nessun parametro._


### `cerca_aziende`

Cerca fra le aziende dell’organizzazione con filtri (testo, provincia, settore, priorità minima (0-100), distanza, solo con bozze pronte, analizzate o no). Restituisce id, dati essenziali e link alla scheda.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `testo` | string | no | Nome, città o parola chiave |
| `provincia` | string | no | Sigla, es. MI |
| `settore` | string | no | Etichetta del settore, es. "Edilizia e impianti" |
| `punteggio_min` | integer | no | 0–100 |
| `km_max` | integer | no | 1–500 |
| `solo_con_bozze` | boolean | no |  |
| `analizzate` | boolean | no | true = solo analizzate, false = solo da analizzare |
| `ordine` | string | no | valori: `score`, `distanza`, `valore`, `recenti` |
| `limite` | integer | no | 1–50 |


### `scheda_azienda`

Dossier completo di un’azienda in Markdown: dati, persone e canali ammessi, segnali, dati pubblici (ANAC, archive.org), date dei contenuti, testo del sito. Da leggere prima di analizzarla o scriverle.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `id` | string | sì | id dell’azienda (uuid) |


### `dossier_da_lavorare`

Scarica i dossier delle aziende messe in coda per Claude (più, se top > 0, le migliori non ancora analizzate) con il README: regole di scrittura, catalogo, verifica delle date, ricerca in rete e formato dei risultati. Poi analizza e invia con invia_risultati. Per lavorare solo la coda (es. con /loop, quando l’utente preme “Manda al mio Claude Code”) usa top: 0: se la coda è vuota non c’è niente da fare.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `top` | integer | no | 0–20 |


### `invia_risultati`

Invia analisi e bozze per una o più aziende (stesso formato di results.json descritto nel README dei dossier: { "version": 1, "items": [...] }). Le bozze in canali non consentiti vengono scartate e segnalate.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `risultati` | object | sì | Oggetto results.json completo |


### `metti_in_coda`

Mette un’azienda in coda per Claude, con canale e indicazioni facoltative (es. "proponi l’app rapportini"). Poi la trovi in dossier_da_lavorare.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `id` | string | sì | id dell’azienda |
| `canale` | string | no | valori: `letter`, `phone`, `linkedin`, `email`, `whatsapp` |
| `indicazioni` | string | no |  |


### `azienda_crea`

Aggiunge un’azienda a mano (es. una segnalazione, un contatto di una fiera): stessi controlli del portale. Se esiste già (stessa P.IVA, stesso sito o stesso nome nello stesso comune) restituisce l’id di quella esistente. Con il sito, DeviL lo legge e calcola il punteggio.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `ragione_sociale` | string | sì |  |
| `partita_iva` | string | no |  |
| `sito` | string | no |  |
| `email` | string | no |  |
| `telefono` | string | no |  |
| `comune` | string | no |  |
| `provincia` | string | no | sigla, es. CO |
| `settore` | string | no |  |
| `referente` | string | no | nome e cognome, se noto e pubblico |
| `ruolo_referente` | string | no |  |
| `rapporto` | string | no | base giuridica col referente: none (nessun rapporto), legitimate_interest (conosciuto), contract (cliente) · valori: `none`, `legitimate_interest`, `contract` |


### `avvia_ricerca`

Avvia la ricerca di nuove aziende in una o più province (sigle, max 8). Procede a tappe distanziate; una ricerca alla volta per organizzazione.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `province` | array di string | sì |  |


## Search


### `offerte_elenco`

«Le mie offerte»: servizi, prodotti e cataloghi che l’organizzazione vende, con quante aziende sono adatte a ognuna. Leggile prima di offerte_salva, per non duplicarle.

_Nessun parametro._


### `offerte_salva`

Crea o aggiorna un’offerta in «Le mie offerte» (con id = aggiornamento). Settori: le chiavi elencate nel campo settori; parole chiave = parole che indicano il bisogno. Dopo il salvataggio DeviL calcola le aziende adatte.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `id` | string | no | id per aggiornare un’offerta esistente |
| `nome` | string | sì |  |
| `tipo` | string | no | valori: `servizio`, `prodotto`, `catalogo`, `software` |
| `in_una_riga` | string | no |  |
| `problema_risolto` | string | no |  |
| `per_chi` | string | no |  |
| `prezzo_da` | number | no |  |
| `parole_chiave` | array di string | no |  |
| `settori` | array di string | no | chiavi: industria, edilizia, studi_tecnici, logistica, servizi_prof, sanita, ospitalita, auto, commercio, artigianato, it |
| `ateco` | array di string | no |  |
| `province` | array di string | no |  |


## Dev


### `abbinamenti`

Abbinamenti fra i progetti del portfolio e le aziende analizzate: per un progetto (slug) le aziende con aderenza e livello (pronto, da adattare, da scalare); senza slug i 5 colpi più facili e la classifica dei progetti per opportunità individuate.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `slug` | string | no | slug del progetto (facoltativo) |


### `formato_schede`

Formato delle schede progetto e valori ammessi (settori, tipi di software, temi, stati) con un esempio: leggilo prima di portfolio_salva.

_Nessun parametro._


### `portfolio_elenco`

Le schede dei progetti già caricate (anche le bozze): leggile prima di inviarne di nuove, per non duplicarle (stesso slug = aggiornamento).

_Nessun parametro._


### `portfolio_salva`

Inserisce o aggiorna (per slug) fino a 50 schede progetto lette dai repo locali. Formato e valori ammessi: strumento formato_schede. Solo fatti trovati nei file, niente segreti né codice.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `schede` | array di object | sì |  |


## Build


### `cantieri_da_lavorare`

Cantieri di sviluppo messi in coda dall’utente su DeviL (un software da costruire a tappe). Ne prende al massimo uno per volta: se è nuovo restituisce il brief da salvare come CLAUDE.md in una nuova cartella sotto la cartella base, se è da proseguire restituisce cartella, indicazioni dell’utente e tappa successiva. Restituisce anche i cantieri attivi da allineare: per ognuno controlla nel git della sua cartella i commit dopo l’ultimo allineato e, se ce ne sono, riportali con aggiorna_cantiere (esterno: true).

_Nessun parametro._


### `aggiorna_cantiere`

Aggiorna su DeviL un cantiere di sviluppo: avanzamento, cosa è stato fatto, prossima tappa, cartella, ultimo commit ed eventuale domanda per l’utente. Usalo alla fine di ogni tappa, quando chiudi un pezzo di lavoro in una sessione manuale nella cartella del cantiere, o per riportare commit fatti fuori dal portale (esterno: true). Se l’utente ha scelto «Sul mio server» e hai messo online la demo lì (dopo il suo sì), passa demo_url e demo_accesso (credenziali di prova e istruzioni): l’utente li ritrova nel portale con il pulsante per aprirla. Con «Solo sul mio PC» usa solo demo_accesso per spiegare come avviarla in locale.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `id` | string | sì | id del cantiere (nel CLAUDE.md della cartella) |
| `avanzamento` | integer | no | percentuale sul piano complessivo · 0–100 |
| `fatto` | string | sì | cosa è stato fatto, 3-6 righe |
| `prossima_tappa` | string | no |  |
| `cartella` | string | no | percorso completo della cartella |
| `ultimo_commit` | string | no |  |
| `domanda` | string | no | domanda per l’utente, se serve una sua decisione |
| `stato` | string | sì | valori: `in_corso`, `tappa_finita`, `completato` |
| `esterno` | boolean | no | true se è lavoro fatto fuori dal giro automatico |
| `commit` | array di object | no |  |
| `demo_url` | string | no | indirizzo https della demo se è un’app con server messa online (per le demo statiche usa pubblica_demo) |
| `demo_accesso` | string | no | come entrare nella demo, una cosa per riga, in questo formato (il portale lo mostra come tabella con copia e password nascosta): «Accesso: https://…/accedi», «Password per tutti: …», poi una riga per account «Ruolo: email (nome, nota)», infine «Note: …». Solo credenziali DI PROVA, mai reali o segreti del server. È l’unico posto per le credenziali: mai in fatto, prossima_tappa o domanda. |


### `pubblica_demo`

Mette online sullo spazio demo di DeviL la demo statica di un cantiere, per mostrarla all’utente e ai suoi clienti. Funziona solo se l’utente ha scelto lo spazio DeviL come destinazione, ha dato il consenso e ha premuto «Pubblica la demo» (la trovi tra le DEMO DA PUBBLICARE di cantieri_da_lavorare); altrimenti spiega cosa fare. Restituisce un link di caricamento monouso (30 minuti) e le istruzioni: build statica sotto il percorso base indicato, zip del contenuto della cartella di build, caricamento con curl. La demo va al cliente: prima di pubblicarla verifica la sezione «Qualità grafica» del CLAUDE.md con gli screenshot a 390 e 1440 px.

| Parametro | Tipo | Obbligatorio | Note |
|---|---|---|---|
| `id` | string | sì | id del cantiere |
