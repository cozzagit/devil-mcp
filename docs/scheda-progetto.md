# La scheda di un progetto

Per ogni tuo progetto Claude Code salva in DeviL una **scheda**: è l'unica cosa che lascia il tuo computer. DeviL la usa per abbinare il progetto alle aziende con un problema compatibile. Lo strumento `formato_schede` restituisce sempre la versione aggiornata di questo formato.

## Campi

| Campo | Valori |
|---|---|
| `slug` | minuscole, cifre e trattini, unico per progetto (es. "gestionale-officine") |
| `name` | nome commerciale |
| `folder` | cartella o repo di origine (facoltativo) |
| `status` | uno tra: `live`, `demo`, `in-sviluppo`, `fermo`, `sconosciuto` |
| `url` | URL pubblico se online, altrimenti null |
| `oneLiner` | cosa fa e per chi, 10-200 caratteri |
| `forWho` | chi lo usa (es. "officine auto 2-10 addetti") |
| `verticals` | uno o più tra: `industria`, `edilizia`, `studi_tecnici`, `logistica`, `servizi_prof`, `sanita`, `ospitalita`, `auto`, `commercio`, `artigianato`, `it` |
| `offerings` | uno o più tra: `gestionale-express`, `automazione-documenti-ai`, `portale-clienti`, `dashboard-kpi`, `integrazioni`, `assistente-ai-documenti`, `sito-web`, `iot-monitoraggio` |
| `themes` | uno o più tra: `rapportini`, `area_clienti`, `preventivatore`, `documenti`, `catalogo_ai`, `mezzi`, `cruscotti`, `sito` |
| `features` | 1-10 funzionalità concrete e verificabili (frasi brevi) |
| `highlights` | 0-6 punti di forza veri (es. "multi-tenant", "PDF professionali") |
| `stack` | tecnologie in breve |
| `reuseFor` | 0-6 software per aziende ricavabili riusando il progetto |
| `matchKeywords` | 6-15 radici minuscole DISTINTIVE (es. "cantier", "rapportin", "officin"): le parole troppo generiche come "sito" o "gestionale" contano poco; quelle sotto 3 lettere vengono scartate |
| `maturity` | 1-5 (1 prototipo, 3 usabile, 5 in produzione con clienti) |

## Esempio

```json
{
  "cards": [
    {
      "slug": "gestionale-officine",
      "name": "Gestionale officine",
      "folder": "officina-app",
      "status": "demo",
      "url": null,
      "oneLiner": "Gestionale per officine: accettazione da tablet, preventivi da listino e storico interventi",
      "forWho": "officine auto e moto 2-10 addetti",
      "verticals": [
        "auto"
      ],
      "offerings": [
        "gestionale-express"
      ],
      "themes": [
        "preventivatore"
      ],
      "features": [
        "Accettazione veicolo da tablet con foto",
        "Preventivi da listino ricambi",
        "Storico interventi per targa"
      ],
      "highlights": [
        "funziona anche offline"
      ],
      "stack": "Next.js, PostgreSQL",
      "reuseFor": [
        "gestionale per carrozzerie",
        "app accettazione per centri revisione"
      ],
      "matchKeywords": [
        "officin",
        "ricambi",
        "tagliand",
        "targa",
        "carrozzer",
        "revision"
      ],
      "maturity": 3
    }
  ]
}
```

## Regole

- Scrivi solo ciò che trovi nel codice o nei documenti: niente numeri o clienti inventati.
- Non inviare mai segreti (.env, chiavi, password) né codice sorgente: solo la scheda.
- Per aggiornare una scheda rimanda lo stesso slug.
