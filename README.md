# Trama

Planner personale, alternativa "mia" a Google Calendar.

**Apri l'app:** https://claude.ai/artifact/KkP46gwjDHCxveCk94H2Hz (da computer o dall'app Claude sul telefono)

## Cosa fa diversamente da Google Calendar

- **Niente impegni schiacciati.** Le viste Agenda e Settimana sono "a flusso": ogni impegno è una
  scheda che prende lo spazio che le serve e il titolo va sempre a capo per intero. Gli impegni
  che si sovrappongono vengono raggruppati sotto "Insieme · N" invece di essere stretti affiancati.
  Si vedono anche i buchi liberi ("libero · 2 h") e la linea dell'ora attuale.
- **Calendari interni da qualsiasi dispositivo.** Crea, rinomina, ricolora ed elimina calendari dal
  pannello laterale, anche da telefono.
- **Promemoria con spunta** e lista "Da fare" sempre visibile, con i ritardi evidenziati.
- **Claude dentro e fuori.**
  - Nella pagina c'è la barra "Chiedi a Claude": scrivi «dentista martedì alle 15» o
    «ricordami di pagare l'affitto il primo del mese» e la voce viene creata.
  - Da una sessione di Claude Code puoi dire «fissami…» o «ricordami…»: Claude scrive direttamente
    nel database del planner (istruzioni in `CLAUDE.md`).

## Struttura

- `index.html`: l'intera app (HTML, CSS e JS senza dipendenze, font Source Sans 3 / Source Code Pro).
- `CLAUDE.md`: schema dei dati e istruzioni per Claude.
