# DeviL per Claude Code (server MCP)

**Il tuo miglior commerciale è il codice che hai già scritto.**

[DeviL](https://devil.vibecanyon.com) analizza i software che hai già sviluppato, trova PMI italiane che potrebbero averne bisogno e ti aiuta a trasformare il tuo codice in nuove opportunità commerciali. Questo repository spiega come collegarlo al tuo **Claude Code** come server MCP, con esempi pronti da usare.

> Il server è remoto e gestito da DeviL: non c'è niente da installare. Ti servono un account DeviL (beta su invito) e un token.

## Collegarlo in un minuto

1. In DeviL apri **Impostazioni → Claude Code e API** e crea un token (inizia con `cbs_`).
2. Nel terminale:

```bash
claude mcp add --transport http --scope user devil https://devil.vibecanyon.com/api/mcp --header "Authorization: Bearer cbs_IL_TUO_TOKEN"
```

3. Apri Claude Code e scrivi: *«Usa DeviL: dammi la panoramica»*.

La guida passo passo, con le schermate, è su <https://devil.vibecanyon.com/guida/claude-code>.

## Cosa può fare il tuo Claude Code

- **Leggere i tuoi repository** sul tuo computer e salvarne la scheda in DeviL. Il codice non lascia la tua macchina: arriva solo la scheda (cosa fa, per chi, funzioni, settori).
- **Cercare aziende** italiane per zona e settore, con i segnali osservati e la prova di dove sono stati trovati.
- **Analizzarle** con ricerca in rete, citando le fonti e verificando le date.
- **Preparare il primo contatto** nel canale consentito: lettera, telefonata, LinkedIn. Email e WhatsApp solo con consenso o rapporto in essere: DeviL blocca il resto.
- **Lavorare la coda da solo** con `/loop`, mentre fai altro.
- Con il livello Build, **costruire il software** richiesto a tappe, con la demo.

Ogni azienda arriva con **tre indici separati**: *Opportunità* (quanto è probabile il problema), *Adatta a te* (quanto un tuo software lo risolve) e *Affidabilità* (quanto sono solide le prove). Un indizio non è un bisogno: con prove deboli l'azienda è «da verificare», non «pronta».

## Strumenti

| Strumento | Da livello | Cosa fa |
|---|---|---|
| `panoramica` | Base | Situazione dell’organizzazione su DeviL: piano e limiti, zona, numeri (aziende, analizzate, bozze pronte, in coda) e le prossime 10 mosse consigliate. |
| `cerca_aziende` | Base | Cerca fra le aziende dell’organizzazione con filtri (testo, provincia, settore, priorità minima (0-100), distanza, solo con bozze pronte, analizzate o no). |
| `scheda_azienda` | Base | Dossier completo di un’azienda in Markdown: dati, persone e canali ammessi, segnali, dati pubblici (ANAC, archive.org), date dei contenuti, testo del sito. |
| `dossier_da_lavorare` | Base | Scarica i dossier delle aziende messe in coda per Claude (più, se top > 0, le migliori non ancora analizzate) con il README: regole di scrittura, catalogo, verifica delle date, ricerca in rete e formato dei risultati. |
| `invia_risultati` | Base | Invia analisi e bozze per una o più aziende (stesso formato di results.json descritto nel README dei dossier: { "version": 1, "items": [...] }). |
| `metti_in_coda` | Base | Mette un’azienda in coda per Claude, con canale e indicazioni facoltative (es. "proponi l’app rapportini"). |
| `azienda_crea` | Base | Aggiunge un’azienda a mano (es. una segnalazione, un contatto di una fiera): stessi controlli del portale. |
| `avvia_ricerca` | Base | Avvia la ricerca di nuove aziende in una o più province (sigle, max 8). |
| `offerte_elenco` | Search | «Le mie offerte»: servizi, prodotti e cataloghi che l’organizzazione vende, con quante aziende sono adatte a ognuna. |
| `offerte_salva` | Search | Crea o aggiorna un’offerta in «Le mie offerte» (con id = aggiornamento). |
| `abbinamenti` | Dev | Abbinamenti fra i progetti del portfolio e le aziende analizzate: per un progetto (slug) le aziende con aderenza e livello (pronto, da adattare, da scalare); senza slug i 5 colpi più facili e la classifica dei progetti per opportunità individuate. |
| `formato_schede` | Dev | Formato delle schede progetto e valori ammessi (settori, tipi di software, temi, stati) con un esempio: leggilo prima di portfolio_salva. |
| `portfolio_elenco` | Dev | Le schede dei progetti già caricate (anche le bozze): leggile prima di inviarne di nuove, per non duplicarle (stesso slug = aggiornamento). |
| `portfolio_salva` | Dev | Inserisce o aggiorna (per slug) fino a 50 schede progetto lette dai repo locali. |
| `cantieri_da_lavorare` | Build | Cantieri di sviluppo messi in coda dall’utente su DeviL (un software da costruire a tappe). |
| `aggiorna_cantiere` | Build | Aggiorna su DeviL un cantiere di sviluppo: avanzamento, cosa è stato fatto, prossima tappa, cartella, ultimo commit ed eventuale domanda per l’utente. |
| `pubblica_demo` | Build | Mette online sullo spazio demo di DeviL la demo statica di un cantiere, per mostrarla all’utente e ai suoi clienti. |

Descrizioni complete e parametri: [docs/strumenti.md](docs/strumenti.md). I livelli sono cumulativi: Base 39 €, Search 89 €, Dev 149 €, Build 299 € al mese (prezzi finali). Dettagli su <https://devil.vibecanyon.com/prezzi>.

## Esempi

- [examples/comandi.md](examples/comandi.md): richieste tipiche da scrivere a Claude Code.
- [examples/CLAUDE.md](examples/CLAUDE.md): un CLAUDE.md di esempio per lavorare con DeviL nei tuoi progetti.
- [docs/scheda-progetto.md](docs/scheda-progetto.md): il formato della scheda che Claude Code salva per ogni tuo progetto.

## Sicurezza

- Il token si crea e si revoca da DeviL; DeviL ne conserva solo l'impronta (SHA-256).
- Ogni token dà accesso solo agli strumenti del tuo livello e ai dati della tua organizzazione.
- Il codice dei tuoi repository non viene trasmesso.
- Dettagli: <https://devil.vibecanyon.com/sicurezza>.

## English summary

DeviL is an Italian B2B SaaS that matches the software you have already built with Italian SMEs that may need it, using public data only (company websites, ANAC open data, archive.org). This repository documents its **remote MCP server** for Claude Code: add it with the command above using a token from *Impostazioni → Claude Code e API*. Tools and examples are in Italian. Each company comes with three separate indices (opportunity, fit, evidence confidence), and outreach is limited to channels allowed by Italian direct-marketing rules.

## Licenza

Gli esempi e la documentazione di questo repository sono rilasciati con licenza MIT (vedi [LICENSE](LICENSE)). Il servizio DeviL, il suo codice e il nome e il logo «DeviL» non sono coperti da questa licenza.

Un progetto di Luca Porro · <devil@vibecanyon.com>
