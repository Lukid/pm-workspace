# Riferimento GitLab — Net7

Guida completa per la gestione operativa di GitLab. Unifica processo, workflow, configurazione e convenzioni.

---

## 1. Struttura Repository

### Organizzazione
GitLab è organizzato **per tipologia applicativa**, non per cliente.

- **Group** = tecnologia: `laravel/`, `drupal/`, `wordpress/`
- **Project** = applicazione: `[cliente]-[progetto]` (es. `anci-portale-cittadino`)
- Se necessario: separazione `nome-app-frontend` / `nome-app-backend`

### Branch

| Branch | Scopo | Push |
|--------|-------|------|
| `main` | Produzione | Solo via MR |
| `develop` | Sviluppo integrato | Solo via MR |
| `staging` | Ambiente di test | Solo via MR |

Branch di lavoro: `[tipo]/[issue-id]-[descrizione-breve]`
Tipi: `feature/`, `bugfix/`, `hotfix/`, `refactor/`, `docs/`

---

## 2. Workflow Issue (8 stati)

```
Backlog → Triage → Ready → In progress → In review → QA/Validation → Ready to deploy → Done
```

### Regole di transizione
- **Ready**: solo se ha criteri di accettazione, priorità, urgenza, dipendenze note
- **In progress**: deve avere assignee, WIP limit 2 per persona
- **Done**: merge completato + deploy effettuato + criteri accettazione soddisfatti

### Stati speciali (label, non colonne)
- `status::blocked` — impedimento esterno
- `status::waiting-input` — attesa info

---

## 3. Priorità e Urgenza

**Priorità** = ordine di esecuzione. **Urgenza** = tempo massimo di risposta.

### Label obbligatorie

| Label | Descrizione |
|-------|-------------|
| `priority::critical` | Blocco business / produzione giù |
| `priority::high` | Molto importante |
| `priority::medium` | Normale |
| `priority::low` | Nice-to-have |
| `urgency::immediate` | Intervento immediato |
| `urgency::short-term` | Entro 1 giorno lavorativo |
| `urgency::normal` | Entro 3 giorni lavorativi |
| `urgency::planned` | Pianificabile |

### Altre label

```
type::task | type::feature | type::bug | type::incident
impact::high | impact::medium | impact::low
area::frontend | area::backend | area::devops | area::data
scope::extra | scope::garanzia
gate::g1 | gate::g2 | gate::g3 | gate::g4
```

---

## 4. Scrittura Issue

### Titolo
Descrive **azione + oggetto + contesto**. Comprensibile senza leggere la descrizione.

### Descrizione obbligatoria
- **Contesto**: perché esiste la richiesta
- **Obiettivo**: cosa deve cambiare
- **Ambito**: incluso ed esplicitamente escluso

### Criteri di accettazione (obbligatori)
Formato: `Dato X, quando Y, allora Z`

Un'Issue non va in **Ready** senza criteri di accettazione.

### Dipendenze
Sempre esplicitate: `depends on #ID`, `blocked by #ID` + label `status::blocked`

---

## 5. Flussi operativi

### Feature/Task
1. Apertura + Triage (PM): template, labels, criteri accettazione
2. Ready → Assignee prende in carico (pull o push)
3. In progress → MR + In review → QA → Ready to deploy → Done

### Bug
1. Template bug (riproduzione + impatto)
2. Triage (severità, workaround)
3. Se urgente → hotfix, altrimenti milestone prossimo rilascio

### Incident / Hotfix
1. `type::incident` + `priority::critical` + `urgency::immediate`
2. Assegnazione rapida
3. Fix → Review rapida → Deploy → Chiusura con causa
4. Post-mortem se P0

---

## 6. Gestione post-rilascio

| Tipo | Priority | Urgency | Azione |
|------|----------|---------|--------|
| Bug non bloccante | high/medium | short-term/normal | Milestone prossimo rilascio |
| Incident | critical | immediate | Fix immediato |
| Manutenzione | medium/low | planned | Milestone maintenance |

---

## 7. Board

| Board | Scopo |
|-------|-------|
| **Delivery** (default) | 8 colonne standard |
| **Triage** | Issue da classificare/bloccate |
| **Incident & Hotfix** | Emergenze |
| **Per area** | Focus team (frontend, backend, etc.) |

---

## 8. Convenzioni tecniche

### Commit messages
```
[tipo]: [descrizione breve]
```
Tipi: `feat`, `fix`, `refactor`, `style`, `docs`, `test`, `chore`

### Merge Request
- Sempre da branch a develop (mai push diretto)
- Almeno 1 approvazione
- Issue collegata: `Closes #ID`
- Pipeline green

### Milestones
Format: `[Fase/Sprint] - [Nome] (vX.Y)`

### Time tracking
```
/estimate 4h    /spend 2h
```

---

## 9. Issue Templates

### Feature (.gitlab/issue_templates/Feature.md)
```
## Contesto
## Obiettivo
## Criteri di accettazione
- [ ] Dato X, quando Y, allora Z
## Impatto
## Note tecniche / dipendenze
/label ~"type::feature"
```

### Bug (.gitlab/issue_templates/Bug.md)
```
## Ambiente
## Descrizione del problema
## Passi per riprodurre
## Comportamento atteso vs reale
## Impatto
## Workaround
/label ~"type::bug"
```

---

## 10. Setup nuovo progetto

1. [ ] Creare repository nel Group corretto
2. [ ] Proteggere branch `main` e `develop`
3. [ ] Verificare/creare label standard
4. [ ] Creare milestones iniziali
5. [ ] Configurare Board Delivery (8 colonne)
6. [ ] Aggiungere Issue + MR templates
7. [ ] Invitare team con ruoli (Maintainer/Developer/Reporter)

---

## 11. Definition of Done

Ogni Issue è "Done" solo se:
- [ ] Criteri di accettazione soddisfatti
- [ ] MR mergeata e pipeline verde
- [ ] Test aggiornati quando opportuno
- [ ] Documentazione aggiornata se cambia comportamento

---

*Documento parte del Sistema Qualità Net7 — ISO 9001:2015*
