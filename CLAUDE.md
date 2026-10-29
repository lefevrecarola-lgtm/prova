# Trama — planner personale

**Inizio sessione:** leggi lo stato del progetto qui sotto (`PROGETTO.md`): obiettivi, decisioni,
cose aperte. **Fine sessione o dopo ogni decisione:** aggiorna `PROGETTO.md` (stato, "Aperto",
diario) e fai commit + push.

@PROGETTO.md

App di calendario a file singolo (`index.html`, HTML/CSS/JS vanilla) pubblicata come Artifact
privato su claude.ai con database integrato.

- **App pubblicata:** https://claude.ai/artifact/KkP46gwjDHCxveCk94H2Hz
- **Ripubblicare dopo una modifica:** Artifact tool, `file_path: index.html`, `url` qui sopra
  (senza `capabilities` per mantenere quelle già salvate: `db` con regola root
  `read: interact, write: admin` e `sample`).

## Quando l'utente chiede di fissare un appuntamento o ricordare qualcosa

Usa il tool `ArtifactData` con `url` = l'app qui sopra. Non serve ripubblicare: la pagina
è in ascolto in tempo reale e mostra subito le modifiche su telefono e computer.

1. Leggi i calendari: `action: list`, `collection: calendars` → scegli il `calendarId` adatto.
2. Crea la voce: `action: set`, `collection: events`, `doc_id` nuovo (es. `c` + timestamp base36),
   senza `if_version`.
3. Per spostare/modificare: prima `get` o `query`, poi `update` con l'`if_version` letto.
4. Per spuntare un promemoria: `update` con `{ "done": true }`.

Le date sono **ora locale (Europe/Rome)** come stringhe, confrontabili lessicograficamente.

### `calendars/{id}`
| campo | tipo | note |
|---|---|---|
| `name` | string | nome mostrato |
| `color` | string | uno di `#4f5bd5 #0e9a87 #e2700b #d03a8c #3f9b3c #8a4ad3 #1b87cf #cf3a3f #b98f00 #6c6c78` |
| `order` | number | ordine nel pannello |

### `events/{id}`
| campo | tipo | note |
|---|---|---|
| `title` | string | |
| `type` | `"event"` \| `"task"` | `task` = promemoria con spunta |
| `calendarId` | string | id di un documento in `calendars` |
| `allDay` | boolean | |
| `start` | string | `YYYY-MM-DDTHH:MM`, oppure `YYYY-MM-DD` se `allDay` |
| `end` | string? | evento a orario: `YYYY-MM-DDTHH:MM`; tutto il giorno: data **esclusiva** (giorno dopo l'ultimo). Assente per i task |
| `done` | boolean | sempre presente (anche `false`): la lista "Da fare" filtra su `done == false` |
| `location`, `notes` | string | facoltativi |
| `createdBy` | `"app"` \| `"claude"` | metti `"claude"` per le voci create da te |
| `updatedAt` | string | ISO timestamp |

Esempio evento: `{"title":"Dentista","type":"event","calendarId":"personale","allDay":false,"start":"2026-11-03T15:00","end":"2026-11-03T16:00","done":false,"location":"Via Roma 12","notes":"","createdBy":"claude"}`

Esempio promemoria: `{"title":"Pagare l'affitto","type":"task","calendarId":"personale","allDay":true,"start":"2026-11-01","done":false,"createdBy":"claude"}`

## Sviluppo

- Fuori da claude.ai (`window.claude` assente) la pagina usa un database in memoria con
  dati "Esempio ·": utile per provare il layout aprendo il file in locale.
- Il design segue lo stile UI di Adobe Spectrum (Source Sans 3, pulsanti a pillola,
  neutri freddi, titoli molto pesanti) senza usarne colori o marchio.
