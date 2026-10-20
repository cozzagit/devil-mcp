# Sicurezza

## Segnalare una vulnerabilità

Se trovi un problema di sicurezza nel servizio DeviL o nel server MCP, **non aprire una issue pubblica**. Scrivi a **devil@vibecanyon.com** con oggetto «Sicurezza», indicando:

- cosa hai trovato e dove (indirizzo, strumento MCP, parametri);
- come riprodurlo;
- l'impatto che ti aspetti.

Rispondo entro 72 ore e ti tengo aggiornato fino alla correzione. Ti chiedo di non accedere ai dati di altri e di aspettare la correzione prima di rendere pubblica la segnalazione.

## Come è protetto il collegamento

- Il token si crea e si revoca da DeviL (Impostazioni → Claude Code e API); DeviL ne conserva solo l'impronta (SHA-256).
- Ogni token dà accesso solo agli strumenti del livello dell'organizzazione e ai suoi dati.
- Il codice dei repository resta sul tuo computer: al server arriva solo la scheda del progetto.
- Tutto il traffico passa in HTTPS; server e database sono in Italia.

Pagina completa: <https://devil.vibecanyon.com/sicurezza>.

## Il tuo token

Tienilo come una password: non metterlo in repository, issue o screenshot. Se pensi che sia stato esposto, revocalo da DeviL e creane uno nuovo.
