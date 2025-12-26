# PM Workspace

> Repository metodologica per la gestione progetti Net7

## Scopo

Questa repository contiene:
- **Metodologia** di gestione progetti (processi, definizioni, convenzioni)
- **Template** per tutti i documenti di progetto
- **Checklist** operative
- **Istruzioni per Claude Code** (`CLAUDE.md`)

I **dati reali dei progetti** vivono nella cartella `projects/` che è **esclusa da Git** per privacy.

---

## Modalità di Utilizzo

Questo workspace supporta **due modalità** con Claude Code:

### PM Mode (default)
Per gestire progetti reali. Si attiva automaticamente quando parli di progetti specifici.

### Develop Mode
Per lavorare sulla struttura del workspace stesso. Attiva con `modalità develop`.

Vedi `CLAUDE.md` per i dettagli.

---

## 📁 Struttura

```
pm-workspace/
├── CLAUDE.md                 # Istruzioni per l'agente AI (snello)
├── BACKLOG.md                # Miglioramenti futuri del workspace
├── README.md                 # Questo file
│
├── methodology/              # Come lavoriamo
│   ├── ai-guidelines.md      # Linee guida AI dettagliate
│   ├── process-guide.md      # Processo gate-based
│   ├── definitions.md        # DoR, DoD, severity, SLA
│   ├── gitlab-conventions.md # Label, board, milestone
│   └── communication-style.md
│
├── templates/                # Template documenti
│   ├── project-brief.md
│   ├── gate-G1-wireframe.md
│   ├── gate-G2-mockup.md
│   ├── gate-G3-uat.md
│   ├── gate-G4-golive.md
│   ├── change-request.md
│   ├── sal.md
│   ├── uat-plan.md
│   ├── uat-checklist.md
│   ├── buglist.md
│   ├── raid-log.md
│   ├── decision-log.md
│   ├── actions-log.md
│   ├── golive-plan.md
│   ├── rollback-plan.md
│   ├── meeting-notes.md
│   └── project-context.md
│
├── checklists/               # Checklist operative
│   ├── project-kickoff.md
│   ├── pre-uat.md
│   ├── pre-golive.md
│   └── project-closure.md
│
├── examples/                 # Esempi (anonimizzati)
│
└── projects/                 # ⚠️ GITIGNORED
    └── [nome-progetto]/      # Dati reali (locali)
```

---

## 🚀 Quick Start

### Nuovo Progetto

1. Crea directory in `projects/`:
   ```bash
   mkdir -p projects/nome-cliente-progetto/{gates,changes,sal,uat,golive,comms,context}
   ```

2. Copia i template base:
   ```bash
   cp templates/project-context.md projects/nome-cliente-progetto/.project-context.md
   cp templates/project-brief.md projects/nome-cliente-progetto/brief.md
   cp templates/raid-log.md projects/nome-cliente-progetto/raid.md
   cp templates/actions-log.md projects/nome-cliente-progetto/actions.md
   cp templates/decision-log.md projects/nome-cliente-progetto/decisions.md
   ```

3. Compila `.project-context.md` con i metadata

4. Procedi con il kickoff seguendo `checklists/project-kickoff.md`

### Usare con Claude Code

1. Apri la repo in Claude Code
2. Claude leggerà automaticamente `CLAUDE.md`
3. Usa comandi come:
   - "Crea progetto nome-cliente"
   - "Apri progetto nome-cliente"
   - "Genera SAL per periodo X-Y"
   - "Apri CR per nuova funzionalità"

---

## 📋 Processo Gate-Based

| Gate | Cosa approva | Deliverable |
|------|--------------|-------------|
| **G1** | Wireframe/Scope | Perimetro + struttura |
| **G2** | UI/Mockup | Design grafico |
| **G3** | UAT/Staging | Test utente |
| **G4** | Go-live | Produzione |

Ogni gate richiede approvazione scritta del cliente prima di procedere.

---

## 📚 Documenti Principali

| Documento | Quando | Template |
|-----------|--------|----------|
| Project Brief | Avvio | `templates/project-brief.md` |
| SAL | Periodico | `templates/sal.md` |
| Change Request | Ogni modifica scope | `templates/change-request.md` |
| UAT Plan | Pre-test | `templates/uat-plan.md` |
| Go-live Plan | Pre-rilascio | `templates/golive-plan.md` |

---

## 🔧 Manutenzione

- **Aggiorna i template** quando trovi pattern migliori
- **Aggiungi esempi** anonimizzati per riferimento
- **Rivedi la metodologia** periodicamente

---

## 📝 Note

- I file in `projects/` sono **locali** e non vanno mai committati
- La metodologia è allineata a **ISO 9001:2015**
- Per dubbi, consulta `methodology/process-guide.md`

---

*Net7 — Sistema Qualità ISO 9001:2015*
