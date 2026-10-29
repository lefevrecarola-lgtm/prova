# Stato del progetto

> File di memoria tra una sessione e l'altra. **Leggilo all'inizio di ogni sessione e aggiornalo
> alla fine** (o quando si decide qualcosa): stato, decisioni, cose aperte, diario.
> Scrivi in italiano: l'utente parla italiano.

Ultimo aggiornamento: 2026-10-29

## Obiettivo

Un'applicazione di planning personale, alternativa "mia" a Google Calendar, usabile da computer e
da telefono e collegata a Claude: l'utente vuole poter dire a Claude "fissami un appuntamento" o
"ricordami una cosa" e trovarla nel calendario. È anche un esperimento per **testare le
potenzialità di Claude Code**: l'utente sa che esistono MCP per Google Calendar ma vuole un
calendario suo.

### Cosa non piace all'utente di Google Calendar (requisiti di partenza)
1. Layout "accartocciato": eventi alla stessa ora sovrapposti, titoli lunghi troncati.
2. Vuole usarlo da computer e telefono **e** collegarlo a Claude.
3. Dal telefono, su Google Calendar, non si possono creare calendari interni: qui sì.
4. La grafica non gli piace. Gli piace lo **stile UI di Adobe** (scelte di layout, font, palette),
   non il marchio né i colori Adobe in sé.

Indicazione generale dell'utente: usare liberamente skill, HTML/JS/CSS o altro per avere una
grafica moderna e bella.

## Stato attuale

- **App online:** https://claude.ai/artifact/KkP46gwjDHCxveCk94H2Hz (Artifact privato, solo
  l'utente lo vede; serve essere loggati su claude.ai).
- **Codice:** `index.html` (file unico, vanilla JS), branch `claude/kind-euler-f1h5ij` del repo
  `lefevrecarola-lgtm/prova`.
- **Database:** contiene i calendari `personale` e `lavoro`; nessun evento reale ancora.
- **Nome provvisorio:** "Trama". **All'utente non piace** → da cambiare (vedi "Aperto").

### Funzioni presenti
- Viste **Agenda** (14 giorni), **Settimana**, **Mese**; navigazione e mini-calendario laterale.
- Layout "a flusso": schede ad altezza libera, titoli sempre interi, sovrapposizioni raggruppate
  ("Insieme · N"), buchi liberi ("libero · 2 h"), linea dell'ora attuale.
- Mese: tutti i titoli visibili su desktop; su telefono pallini + elenco del giorno scelto.
- Calendari: crea / rinomina / ricolora / nascondi / elimina (anche da telefono).
- Eventi e **promemoria** (task con spunta) + lista "Da fare" con ritardi in rosso.
- Barra **"Chiedi a Claude"** nella pagina (capability `sample`): testo libero → voci create.
- Tema chiaro e scuro; responsive con pannello a cassetto e pulsante "+" su telefono.

## Decisioni prese (e perché)

| Decisione | Motivo |
|---|---|
| Pubblicare come **Artifact claude.ai con capability `db`** invece di un sito + backend proprio | Si apre da telefono e computer senza hosting, è privato, e Claude può leggere/scrivere i dati con il tool `ArtifactData` da qualsiasi sessione Claude Code |
| **Un documento per evento** in `events/`, date come stringhe locali `YYYY-MM-DDTHH:MM` | Semplice da scrivere per Claude, confrontabile come testo, niente fusi orari (si assume Europe/Rome) |
| Viste **a flusso** al posto della griglia oraria | È il problema n.1 dell'utente con Google Calendar |
| Stile ispirato ad **Adobe Spectrum**: Source Sans 3 (font open source di Adobe), pulsanti a pillola, titoli 800–900, neutri freddi, accento indaco proprio | Richiesta dell'utente, senza copiare colori o marchio |
| Regole db: lettura `interact`, scrittura `admin` | Solo il proprietario (ed eventuali editor) modifica |
| Fuori da claude.ai la pagina usa un **db in memoria con dati "Esempio ·"** | Per provare il layout in locale / nelle anteprime |

Schema dati e istruzioni operative per scrivere nel planner: vedi `CLAUDE.md`.

## Aperto / da decidere

- [ ] **Nuovo nome** dell'app (proposti: Agenda, Diario, Orbita, Sett; l'utente non ha ancora scelto).
      Quando si decide: cambiare `<title>`, il marchio nella pagina, README, CLAUDE.md e ripubblicare
      **sullo stesso URL**.
- [ ] Fissare l'artifact nella barra laterale di claude.ai (offerto, nessuna risposta ancora).
- [ ] L'utente non ha ancora provato l'app dentro claude.ai: chiedere feedback su ciò che non va.

## Idee per i prossimi passi (non ancora richieste)

- Eventi ricorrenti.
- Notifiche / riepilogo quotidiano (es. attività pianificata che manda un riassunto).
- Importazione da Google Calendar (file .ics).
- Vista Giorno.
- Trascinamento per spostare gli eventi.

## Limiti noti

- Nessuna notifica: i promemoria si vedono solo aprendo l'app.
- Orari solo in ora locale italiana.
- Scrivere nel planner "da conversazione" funziona dalle sessioni **Claude Code**
  (tool `ArtifactData`); nelle chat normali di claude.ai probabilmente no.
- La barra "Chiedi a Claude" crea voci ma non modifica né cancella quelle esistenti.

## Diario

- **2026-10-29** — Prima sessione. Raccolti i requisiti, costruita e pubblicata l'app, creati i
  calendari Personale e Lavoro, testata lettura/scrittura dal tool. Spiegato all'utente dove trova
  il link e come funziona il collegamento con Claude. All'utente non piace il nome "Trama".
  Creato questo file come memoria tra sessioni.
