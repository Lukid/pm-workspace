# Convenzioni GitLab

Guida alla configurazione tecnica di GitLab per i progetti Net7.

> Questo documento è complementare a [gitlab-workflow.md](gitlab-workflow.md), che definisce il processo operativo completo.

---

## 1. Struttura Repository

### Modello organizzativo

Il GitLab è organizzato **per tipologia applicativa**, non per cliente.

**Group di primo livello** = tecnologia/framework:
- `laravel/`
- `drupal/`
- `wordpress/`

**Project** = applicazione specifica. Se l'architettura lo richiede:
- `nome-app-frontend`
- `nome-app-backend`

### Naming Project
```
[cliente]-[progetto]
```
Esempi: `anci-portale-cittadino`, `comune-pisa-sito-istituzionale`

### Branch principali

| Branch | Scopo | Chi può pushare |
|--------|-------|-----------------|
| `main` | Produzione | Solo via MR |
| `develop` | Sviluppo integrato | Solo via MR |
| `staging` | Ambiente di test | Solo via MR |

### Branch di lavoro

```
[tipo]/[issue-id]-[descrizione-breve]
```

| Tipo | Quando |
|------|--------|
| `feature/` | Nuova funzionalità |
| `bugfix/` | Correzione bug |
| `hotfix/` | Fix urgente produzione |
| `refactor/` | Refactoring tecnico |
| `docs/` | Documentazione |

Esempi:
- `feature/123-login-spid`
- `bugfix/456-menu-mobile`
- `hotfix/789-crash-checkout`

---

## 2. Labels

Creare a livello di **Gruppo** per riutilizzarle su tutti i progetti.

> **Formato**: `categoria::valore` (lowercase con doppio due punti)

### Type (obbligatoria)
```
type::task          #95a5a6
type::feature       #7f8c8d
type::bug           #e74c3c
type::incident      #c0392b
```

### Priority (obbligatoria)
```
priority::critical  #c0392b   # Blocco business / produzione giù
priority::high      #e74c3c   # Molto importante (rischio alto)
priority::medium    #f39c12   # Normale
priority::low       #27ae60   # Bassa / nice-to-have
```

### Urgency (obbligatoria)
```
urgency::immediate  #c0392b   # Intervento immediato (incident/hotfix)
urgency::short-term #e74c3c   # Presa in carico entro 1 giorno lavorativo
urgency::normal     #f39c12   # Presa in carico entro 3 giorni lavorativi
urgency::planned    #27ae60   # Pianificabile senza impatti immediati
```

### Impact (consigliata)
```
impact::high        #c0392b
impact::medium      #f39c12
impact::low         #27ae60
```

### Status — solo per eccezioni (NON sono colonne)
```
status::blocked       #d9534f   # Impedimento esterno o dipendenza
status::waiting-input #f0ad4e   # Attesa info dal richiedente
```

### Area (consigliata)
```
area::frontend      #3498db
area::backend       #9b59b6
area::devops        #e67e22
area::data          #1abc9c
```

### Scope — gestione contrattuale
```
scope::extra        #8e44ad
scope::garanzia     #2c3e50
```

### Gate — tracciamento approvazioni
```
gate::g1            #3498db
gate::g2            #9b59b6
gate::g3            #e67e22
gate::g4            #27ae60
```

---

## 3. Issue Board

### Board "Delivery" (default)

Colonne basate sugli **8 stati** del workflow:

```
| Backlog | Triage | Ready | In progress | In review | QA/Validation | Ready to deploy | Done |
```

| Colonna | Significato |
|---------|-------------|
| Backlog | Idee/richieste raccolte, non pronte |
| Triage | Classificazione: tipo, impatto, urgenza, info mancanti |
| Ready | Requisiti completi, pronto per essere preso in carico |
| In progress | Lavorazione attiva (deve avere assignee) |
| In review | MR aperta, code review in corso |
| QA/Validation | Test funzionali / regressione / UAT |
| Ready to deploy | Approvato, in attesa di rilascio |
| Done | Rilasciato/chiuso |

### Board alternativi

| Board | Scopo | Filtro |
|-------|-------|--------|
| **Triage** | Issue da classificare o bloccate | `status::waiting-input` + `status::blocked` |
| **Incident & Hotfix** | Emergenze | `type::incident` OR `urgency::immediate` |
| **Per area** | Focus per team | `area::*` |

---

## 4. Milestones

### Naming convention
```
[Fase/Sprint] - [Nome descrittivo] (vX.Y)
```

Esempi:
- `Fase 1 - MVP (v1.0)`
- `Sprint 1 - Setup e Login`
- `Hotfix (v1.0.1)`
- `Maintenance Q1`

### Date
- **Start Date**: inizio lavori
- **Due Date**: deadline (allineata a SAL o gate)

---

## 5. Issue Templates

### Template Task/Feature

Creare file `.gitlab/issue_templates/Feature.md`:

```markdown
## Contesto
<!-- Perché esiste questa richiesta -->

## Obiettivo
<!-- Cosa deve cambiare -->

## Criteri di accettazione
- [ ] Dato X, quando Y, allora Z
- [ ] ...

## Impatto
<!-- Utenti/aree coinvolte -->

## Note tecniche / dipendenze
<!-- Considerazioni per lo sviluppo -->

## Checklist
- [ ] ...

/label ~"type::feature"
```

### Template Bug/Incident

Creare file `.gitlab/issue_templates/Bug.md`:

```markdown
## Ambiente
<!-- prod/stage -->

## Descrizione del problema
<!-- Cosa succede -->

## Passi per riprodurre
1.
2.
3.

## Comportamento atteso vs reale
- **Atteso**:
- **Reale**:

## Impatto
<!-- Utenti/aree coinvolte -->

## Log/screenshot/link
<!-- Allegati -->

## Workaround
<!-- Se disponibile -->

/label ~"type::bug"
```

### Template Change Request

Creare file `.gitlab/issue_templates/ChangeRequest.md`:

```markdown
## CR-XXX: [Titolo]

**Richiesto da**:
**Data richiesta**:
**Riferimento**: <!-- email, call, documento -->

## Descrizione richiesta
<!-- Cosa viene richiesto dal cliente -->

## Motivazione
<!-- Perché serve questa modifica -->

## Analisi impatto

### Effort stimato
- Ore sviluppo:
- Ore design:
- Ore test:
- **Totale**:

### Impatto economico
- Costo extra:

### Impatto timeline
- Ritardo previsto:
- Nuova data consegna:

### Rischi
<!-- Rischi introdotti dalla modifica -->

## Decisione
- [ ] Approvata
- [ ] Rifiutata
- [ ] In valutazione

**Data decisione**:
**Approvato da**:

/label ~"type::feature" ~"scope::extra"
```

---

## 6. Merge Request

### Naming
```
[Issue ID] - [Descrizione breve]
```
Esempio: `#123 - Implementazione login SPID`

### Template MR

Creare file `.gitlab/merge_request_templates/Default.md`:

```markdown
## Descrizione
<!-- Cosa fa questa MR -->

## Issue collegata
Closes #XXX

## Tipo di modifica
- [ ] Feature
- [ ] Bug fix
- [ ] Refactoring
- [ ] Documentazione

## Checklist
- [ ] Codice testato localmente
- [ ] Nessun warning/errore in console
- [ ] Responsive verificato (se frontend)
- [ ] Documentazione aggiornata (se necessario)

## Screenshot (se UI)
<!-- Prima / Dopo -->

## Note per il reviewer
<!-- Punti di attenzione -->
```

### Regole MR

1. **Sempre da branch a develop** (mai push diretto)
2. **Almeno 1 approvazione** prima di merge
3. **Issue collegata** obbligatoria (`Closes #ID`)
4. **Pipeline green** (se CI/CD attiva)

---

## 7. Commit Messages

### Formato
```
[tipo]: [descrizione breve]

[corpo opzionale - cosa e perché]

[footer - riferimenti issue]
```

### Tipi

| Tipo | Quando |
|------|--------|
| `feat` | Nuova funzionalità |
| `fix` | Bug fix |
| `refactor` | Refactoring (no nuova feature, no fix) |
| `style` | Formattazione, spazi |
| `docs` | Documentazione |
| `test` | Aggiunta/modifica test |
| `chore` | Maintenance, dipendenze |

### Esempi

```
feat: aggiunto login con SPID

Implementata integrazione con identity provider SPID.
Supportati tutti i provider certificati AgID.

Closes #123
```

```
fix: corretto crash su menu mobile

Il menu non si apriva su iPhone < iOS 15.
Aggiunto polyfill per IntersectionObserver.

Fixes #456
```

---

## 8. Time Tracking

### Stimare
```
/estimate 4h
/estimate 2d
```

### Registrare tempo speso
```
/spend 2h
/spend 30m
```

### Best practice
- Stimare **prima** di iniziare (in fase Ready)
- Registrare tempo **ogni giorno** o a fine task

---

## 9. Quick Actions Utili

| Comando | Effetto |
|---------|---------|
| `/assign @username` | Assegna issue |
| `/unassign` | Rimuove assegnazione |
| `/label ~"label"` | Aggiunge label |
| `/unlabel ~"label"` | Rimuove label |
| `/milestone %"Nome"` | Assegna a milestone |
| `/due YYYY-MM-DD` | Imposta scadenza |
| `/estimate Xh` | Stima tempo |
| `/spend Xh` | Registra tempo |
| `/close` | Chiude issue |
| `/reopen` | Riapre issue |

---

## 10. Setup Nuovo Progetto

### Checklist

1. [ ] Creare repository nel Group corretto (per tecnologia)
2. [ ] Proteggere branch `main` e `develop`
3. [ ] Verificare label a livello gruppo (o crearle)
4. [ ] Creare milestones iniziali
5. [ ] Configurare Board "Delivery" con 8 colonne
6. [ ] Creare Board alternativi (Triage, Incident)
7. [ ] Aggiungere Issue templates
8. [ ] Aggiungere MR template
9. [ ] Invitare membri del team con ruoli appropriati

### Ruoli suggeriti

| Ruolo GitLab | Chi | Permessi chiave |
|--------------|-----|-----------------|
| Maintainer | PM, Tech Lead | Merge in main, gestione settings |
| Developer | Dev | Push branch, MR, issue |
| Reporter | Cliente (se accesso) | Solo lettura, commenti |

---

*Questo documento è parte del Sistema Qualità Net7 — ISO 9001:2015*
