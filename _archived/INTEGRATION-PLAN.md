# Integration Plan: MCP + Subagents + OpenSpec

**Obiettivo**: Potenziare il PM Workspace con automazione GitLab, OpenSpec integration e architettura subagent.

**Filosofia**: Mantenere la semplicità del workspace attuale, aggiungere automazione dove serve veramente.

---

## 🎯 Visione Finale

```
PM Workspace
├── Progetti tradizionali (PA, consulting)
│   └── Gestiti con workflow attuale (SAL, gate, CR)
│
├── Progetti software (dev-heavy)
│   ├── Workflow tradizionale (gate, CR)
│   ├── OpenSpec (specs + changes)
│   └── GitLab sync (issue, MR, branch)
│
└── Automation Layer
    ├── GitLab MCP (issue/MR automation)
    ├── OpenSpec MCP (spec-driven development)
    └── Workspace MCP (comandi custom PM)
```

---

## 📋 Roadmap Completa

### **FASE 0: Setup MCP Server Esistente** ⚡ START HERE
**Status**: In progress
**Durata stimata**: 1-2 sessioni

#### Obiettivi
- [ ] Analizzare MCP server n8n esistente
- [ ] Documentare funzionalità attuali
- [ ] Identificare gap vs. requirements
- [ ] Sistemare/completare implementazione
- [ ] Integrare con workspace (test su progetto pilota)

#### Deliverable
- `mcp-servers/gitlab-net7/README.md` - Documentazione
- `mcp-servers/gitlab-net7/config.json` - Configurazione
- Test su progetto reale

#### Note
- Verificare compatibilità con gitlab.netseven.it (self-hosted)
- Mappare severity/SLA/label secondo `methodology/gitlab-workflow.md`
- Testare integrazione con `actions.md` e `raid.md`

---

### **FASE 1: GitLab MCP Enhancement**
**Status**: Not started
**Depends on**: Fase 0
**Durata stimata**: 2-3 sessioni

#### Obiettivi
- [ ] Estendere MCP con funzionalità avanzate
- [ ] CRUD completo issue (create, read, update, close)
- [ ] Branch automation secondo `gitlab-setup.md`
- [ ] Merge Request automation
- [ ] Sync bidirezionale workspace ↔ GitLab

#### Features Specifiche

**1. Issue Management**
```yaml
create_issue:
  input:
    project_name: string
    title: string
    description: string
    severity: P0|P1|P2|P3  # Auto-map label + SLA
    assignee: string
    milestone: string
  output:
    issue_url: string
    issue_iid: number
  side_effects:
    - Crea issue su GitLab
    - Aggiorna projects/[nome]/actions.md
    - Se severity P0/P1 → aggiorna raid.md
```

**2. Branch Management**
```yaml
create_branch:
  input:
    issue_iid: number
    branch_type: feature|bugfix|hotfix
  output:
    branch_name: string  # Es: feature/123-issue-title
  validation:
    - Rispetta convenzioni gitlab-setup.md
    - Controlla che issue esista
```

**3. Merge Request**
```yaml
create_mr:
  input:
    source_branch: string
    target_branch: string
    issue_iid: number
  output:
    mr_url: string
  validation:
    - Controlla che issue sia resolved
    - Aggiunge template MR secondo metodologia
```

**4. Sync Commands**
```yaml
sync_project:
  input:
    project_name: string
    direction: gitlab_to_workspace | workspace_to_gitlab | both
  actions:
    - Legge actions.md
    - Confronta con issue GitLab
    - Sincronizza stato/assignee/deadline
```

#### Deliverable
- MCP server completo con tutte le features
- Test suite
- Documentazione API
- Esempi d'uso

---

### **FASE 2: OpenSpec Integration**
**Status**: Not started
**Depends on**: Fase 1
**Durata stimata**: 3-4 sessioni

#### Obiettivi
- [ ] Installare OpenSpec globalmente
- [ ] Creare template progetto software
- [ ] Integrare workflow CR → OpenSpec change
- [ ] Sincronizzare gate con OpenSpec phases
- [ ] Documentare workflow ibrido

#### Struttura Progetto Software

```
projects/my-software-project/
├── .project-context.md         # Come sempre
├── brief.md                    # Project brief tradizionale
├── gates/                      # Gate G1/G2/G3/G4
├── changes/                    # CR tradizionali
├── sal/                        # SAL periodici
├── raid.md                     # Risk/Issue tracking
├── actions.md                  # Action items
├── decisions.md                # Decision log
│
├── dev/                        # 🆕 Sezione sviluppo
│   ├── openspec/               # OpenSpec structure
│   │   ├── specs/              # Current truth
│   │   └── changes/            # Proposed changes
│   │       ├── feature-auth/
│   │       ├── bugfix-login/
│   │       └── CR-001-new-dashboard/
│   │
│   └── gitlab-sync.md          # Mapping OpenSpec ↔ GitLab
│
└── comms/                      # Comunicazioni
```

#### Workflow Integrato

**Scenario 1: Nuova Feature (con CR)**
```
1. Cliente chiede feature nuova
   ↓
2. PM: Genera CR → changes/CR-XXX.md
   ↓
3. Dev Agent: Crea OpenSpec change → dev/openspec/changes/CR-XXX/
   ├── proposal.md
   ├── tasks.md
   └── specs/
   ↓
4. Review interna (tech lead)
   ↓
5. Gate G1/G2 con cliente (approval)
   ↓
6. Dev Agent: Crea GitLab issues da tasks.md
   ↓
7. Sviluppo
   ↓
8. openspec archive → specs/ aggiornate
   ↓
9. Gate G3 (UAT)
```

**Scenario 2: Bug/Miglioramento Tecnico (no CR)**
```
1. Dev trova bug
   ↓
2. Dev Agent: OpenSpec change → bugfix-XXX/
   ↓
3. PM notificato (se impatta roadmap)
   ↓
4. GitLab issue automatico
   ↓
5. Fix + archive
```

#### Gate Mapping

| PM Gate | OpenSpec Phase | Cosa Succede |
|---------|----------------|--------------|
| **G1** (Scope) | Draft → Review | Approval proposal.md + specs/ |
| **G2** (Design) | Review → Implement | Approval design.md (se presente) |
| **G3** (UAT) | Implement → Archive | Testing + acceptance |
| **G4** (Go-live) | Post-archive | Deploy su prod |

#### MCP Commands per OpenSpec

```yaml
openspec_proposal:
  input:
    project_name: string
    change_name: string
    description: string
    linked_cr: string  # Optional: CR-XXX
  output:
    change_path: string
  actions:
    - openspec init (se necessario)
    - Crea change folder
    - Genera proposal.md
    - Se linked_cr → copia context da changes/CR-XXX.md

openspec_create_issues:
  input:
    project_name: string
    change_name: string
  output:
    issue_urls: array
  actions:
    - Legge tasks.md
    - Crea issue GitLab per ogni task
    - Aggiorna tasks.md con link issue

openspec_archive:
  input:
    project_name: string
    change_name: string
  output:
    archived: boolean
  actions:
    - openspec archive
    - Chiude issue GitLab associate
    - Aggiorna decisions.md
```

#### Deliverable
- Template `templates/software-project/`
- Documentazione workflow ibrido
- Guide per Dev Agent
- MCP commands per OpenSpec
- Tutorial + esempi

---

### **FASE 3: Workspace MCP (Custom Commands)**
**Status**: Not started
**Depends on**: Fase 1
**Durata stimata**: 2-3 sessioni

#### Obiettivi
- [ ] MCP server per comandi PM custom
- [ ] Automazione generazione documenti
- [ ] Template rendering avanzato
- [ ] Validation automatica

#### Features

**1. Document Generation**
```yaml
generate_sal:
  input:
    project_name: string
    period: string  # "2024-01-01 to 2024-01-31"
    custom_notes: string
  output:
    sal_path: string
  actions:
    - Legge actions.md, decisions.md, raid.md
    - Analizza periodo
    - Genera SAL da template
    - Aggiunge metriche (velocity, issue chiuse, etc.)

generate_gate:
  input:
    project_name: string
    gate_number: G1|G2|G3|G4
    deliverables: array
  output:
    gate_path: string
  actions:
    - Template gate appropriato
    - Checklist automatica
    - SLA da definitions.md

generate_cr:
  input:
    project_name: string
    description: string
    impact: high|medium|low
  output:
    cr_path: string
    cr_number: string
  actions:
    - Auto-increment CR number
    - Template CR
    - Se impact=high → aggiorna raid.md automaticamente
```

**2. Project Management**
```yaml
create_project:
  input:
    name: string
    type: standard|software|consulting
    client: string
  output:
    project_path: string
  actions:
    - Crea directory structure
    - Template appropriato (standard vs software)
    - Se software → openspec init
    - .project-context.md con metadata

archive_project:
  input:
    name: string
  output:
    archived_path: string
  validation:
    - Controlla gate G4 completato
    - Controlla azioni aperte
    - Controlla issue GitLab aperte

project_health_check:
  input:
    project_name: string
  output:
    report: object
  metrics:
    - Azioni overdue
    - Issue aperte per severity
    - SLA a rischio
    - Gate mancanti
    - CR pending
```

**3. Tracking Automation**
```yaml
add_action:
  input:
    project_name: string
    description: string
    assignee: string
    due_date: date
    create_gitlab_issue: boolean
  output:
    action_id: string
    gitlab_issue_url: string  # Se richiesto
  actions:
    - Aggiorna actions.md
    - Se create_gitlab_issue=true → usa GitLab MCP

add_risk:
  input:
    project_name: string
    description: string
    severity: P0|P1|P2|P3
    mitigation: string
  output:
    risk_id: string
  actions:
    - Aggiorna raid.md
    - Se P0/P1 → crea issue GitLab automatico
    - Notifica in comms/

add_decision:
  input:
    project_name: string
    decision: string
    context: string
    stakeholders: array
  output:
    decision_id: string
  actions:
    - Aggiorna decisions.md
    - Timestamp + metadata
```

**4. Communication Helpers**
```yaml
draft_email:
  input:
    project_name: string
    purpose: sal|gate_request|cr_notification|escalation
    recipient: client|team|stakeholder
    custom_context: string
  output:
    email_draft: string
  actions:
    - Usa communication-style.md
    - Template appropriato
    - Context da progetto
    - Salva in comms/

suggest_response:
  input:
    project_name: string
    situation: string
  output:
    suggestions: array
  actions:
    - Cerca casi simili in decisions.md
    - Consulta methodology/
    - Opzioni con pro/cons
```

#### Deliverable
- Workspace MCP server completo
- Documentazione comandi
- Test suite
- Aggiornamento CLAUDE.md con nuovi comandi

---

### **FASE 4: Subagent Architecture**
**Status**: Not started
**Depends on**: Fase 0, 1, 3
**Durata stimata**: 3-4 sessioni

#### Obiettivi
- [ ] Refactor modalità PM/Develop → Subagent
- [ ] PM Agent (documenti, comunicazione, gestione)
- [ ] Dev Agent (OpenSpec, GitLab, codice)
- [ ] Orchestration logic

#### Architecture

```
User Request
     ↓
Orchestrator (main Claude)
     ↓
     ├─→ PM Agent
     │   ├── Accesso: methodology/, templates/
     │   ├── MCP: Workspace MCP
     │   ├── Specializzazione: SAL, gate, CR, comms
     │   └── Output: Documenti, email, consigli
     │
     ├─→ Dev Agent
     │   ├── Accesso: projects/*/dev/, openspec/
     │   ├── MCP: GitLab MCP + OpenSpec MCP
     │   ├── Specializzazione: spec, issue, branch, MR
     │   └── Output: Issue, branch, proposal, tasks
     │
     └─→ Doc Agent (opzionale, Fase 5)
         ├── Accesso: tutti i template
         ├── MCP: Workspace MCP
         ├── Specializzazione: generazione documento
         └── Output: Documenti conformi
```

#### Routing Logic

```yaml
# Esempi di routing automatico

"Genera SAL per progetto X"
  → PM Agent (workspace MCP)

"Crea issue per bug login"
  → Dev Agent (GitLab MCP)

"Apri CR per nuova feature dashboard"
  → PM Agent crea CR
  → Se progetto software → trigger Dev Agent per OpenSpec proposal

"Status progetto Y"
  → PM Agent (analisi documenti)
  → Se progetto software → + Dev Agent (issue GitLab, OpenSpec changes)

"Cosa dico al cliente per ritardo?"
  → PM Agent (communication helper)
```

#### Subagent Specs

**PM Agent**
```yaml
name: pm-agent
specialization: Project management, documentation, communication
tools:
  - Read, Write, Edit (filesystem)
  - Workspace MCP (custom commands)
  - WebSearch (per ricerche metodologiche)
capabilities:
  - Generare SAL, gate, CR, brief
  - Gestire actions, decisions, RAID
  - Bozze email/comunicazione
  - Consigli metodologici
  - Health check progetti
restrictions:
  - No accesso a dev/ folder
  - No modifica codice
  - No GitLab direct access (usa Workspace MCP che wrappa)
```

**Dev Agent**
```yaml
name: dev-agent
specialization: Software development workflow, OpenSpec, GitLab
tools:
  - Read, Write, Edit (filesystem)
  - GitLab MCP
  - OpenSpec MCP (se implementato)
  - Bash (per openspec CLI)
capabilities:
  - OpenSpec proposal/tasks/archive
  - CRUD GitLab issue/branch/MR
  - Sync workspace ↔ GitLab
  - Analisi specs e tasks
restrictions:
  - No generazione SAL/gate (delega a PM Agent)
  - No comunicazione cliente diretta
  - Lavora solo su progetti software
```

**Orchestrator**
```yaml
name: orchestrator
role: Router e coordinatore
responsibilities:
  - Capire intent user
  - Routing a agent appropriato
  - Coordinare multi-agent (es: CR → PM + Dev)
  - Aggregare risultati
  - Context switching (PM mode / Develop mode)
capabilities:
  - Task decomposition
  - Agent selection
  - Result aggregation
```

#### Deliverable
- Subagent definitions (`subagents/pm-agent.md`, `dev-agent.md`)
- Orchestration logic
- Routing rules
- Test multi-agent scenarios
- Aggiornamento CLAUDE.md

---

### **FASE 5: Advanced Features** (Opzionale)
**Status**: Future
**Durata stimata**: TBD

#### Possibili Estensioni

1. **Analytics & Metrics**
   - Dashboard progetti (velocity, SLA compliance)
   - Trend analysis (CR frequency, gate approval time)
   - Export per reportistica ISO 9001

2. **AI-Powered Insights**
   - Predizione ritardi (ML su azioni/issue)
   - Suggerimenti automatici (similar decisions)
   - Risk detection automatica

3. **Integration Esterni**
   - Calendar sync (deadline → Google Calendar)
   - Slack/Teams notifications
   - Email automation (invio SAL automatico)

4. **Doc Agent** (generazione documento avanzata)
   - Multi-template rendering
   - PDF generation
   - Versioning automatico

5. **OpenSpec MCP** (se non esiste già)
   - Wrapper MCP per openspec CLI
   - Comandi nativi invece di Bash

---

## 🎯 Success Metrics

### Fase 0-1 (GitLab MCP)
- [ ] Creazione issue in <30 sec vs. manuale
- [ ] Zero errori su label/severity mapping
- [ ] Sync workspace ↔ GitLab al 100%

### Fase 2 (OpenSpec)
- [ ] Almeno 1 progetto pilota completo
- [ ] Workflow CR → OpenSpec → GitLab funzionante
- [ ] Dev team adoption >70%

### Fase 3-4 (Workspace MCP + Subagents)
- [ ] Generazione SAL automatica in <1 min
- [ ] Riduzione tempo admin del 40%
- [ ] Zero context loss su switch agent

### Generale
- [ ] Documentazione completa e mantenuta
- [ ] Zero breaking changes su progetti esistenti
- [ ] Backward compatibility al 100%

---

## 📚 Riferimenti

- [OpenSpec GitHub](https://github.com/Fission-AI/OpenSpec)
- [methodology/gitlab-workflow.md](methodology/gitlab-workflow.md)
- [methodology/gitlab-setup.md](methodology/gitlab-setup.md)
- [BACKLOG.md](BACKLOG.md)

---

## 🔄 Maintenance Plan

- **Weekly**: Review issue GitLab create da MCP
- **Biweekly**: Update MCP se cambiano workflow
- **Monthly**: Review subagent performance
- **Quarterly**: Revisione generale architettura

---

*Piano creato: Gennaio 2026*
*Prossimo step: Analisi MCP n8n esistente*
