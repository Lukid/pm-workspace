---
name: sync
description: Sincronizza azioni e rischi del workspace con issue GitLab
arguments:
  - name: progetto
    description: Nome del progetto
    required: false
  - name: opzioni
    description: "Opzioni: 'solo azioni', 'solo rischi', 'dry-run'"
    required: false
---

# Skill: Sincronizza GitLab

Crea issue GitLab da azioni e rischi non ancora sincronizzati nel workspace.

## Istruzioni

### 1. Identifica il progetto

Se `$ARGUMENTS` contiene un nome progetto, usa quello.
Altrimenti chiedi all'utente.

### 2. Verifica prerequisiti

Leggi `.project-context.md` e verifica che il campo `gitlab_project` sia compilato.
Se mancante, avvisa l'utente e interrompi.

### 3. Carica i file da sincronizzare

- `actions.md` — azioni senza link GitLab (colonna Issue GitLab vuota o assente)
- `raid.md` — rischi con priorità 🔴 o 🟡 senza link GitLab

### 4. Opzioni

Analizza `$ARGUMENTS` per opzioni:
- `solo azioni` → sincronizza solo actions.md
- `solo rischi` → sincronizza solo raid.md
- `dry-run` → mostra cosa verrebbe fatto senza creare issue

### 5. Mapping priorità → severity

| Priorità Workspace | Severity GitLab | Label |
|-------------------|-----------------|-------|
| 🔴 Alta | P0 (critical) | `priority::critical` + `urgency::immediate` |
| 🟡 Media | P1 (high) | `priority::high` + `urgency::short-term` |
| 🟢 Bassa | P2 (medium) | `priority::medium` + `urgency::normal` |

### 6. Mapping tipo

| Origine | Type GitLab |
|---------|-------------|
| Azione | `task` |
| Rischio 🔴/🟡 | `incident` |
| Rischio 🟢 | `bug` |

### 7. Crea le issue

Per ogni elemento da sincronizzare, usa il tool MCP `create_issue`:

```
create_issue(
  project: "[valore gitlab_project]",
  type: "[tipo]",
  title: "[titolo]",
  severity: "[P0/P1/P2]",
  use_template: "yes",
  area: "[frontend/backend/devops/data se determinabile]"
)
```

### 8. Aggiorna i file workspace

Dopo la creazione, aggiorna la colonna "Issue GitLab" nei file con il link all'issue creata.

Se il file non ha la colonna "Issue GitLab", aggiungi una colonna "Note" con il riferimento.

### 9. Output

```
Sincronizzazione completata: [progetto]

Azioni sincronizzate: [N]
Rischi sincronizzati: [N]
Issue create: [N]

Dettaglio:
- A-001: [titolo] → GitLab #123
- R-001: [titolo] → GitLab #124
```

Se dry-run:
```
DRY-RUN: nessuna issue creata

Verrebbero create [N] issue:
- A-001: [titolo] → task, P1
- R-001: [titolo] → incident, P0
```

## Requisiti

- Il campo `gitlab_project` deve essere compilato in `.project-context.md`
- Il MCP server `gitlab-net7` deve essere attivo
- Le label devono esistere sul progetto GitLab
