# Convenzioni GitLab

Guida alla configurazione e utilizzo di GitLab per i progetti Net7.

---

## 1. Struttura Repository

### Naming
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
| `design/` | Asset grafici |
| `content/` | Contenuti |
| `refactor/` | Refactoring tecnico |
| `docs/` | Documentazione |

Esempi:
- `feature/123-login-spid`
- `bugfix/456-menu-mobile`
- `hotfix/789-crash-checkout`

---

## 2. Labels (Etichette)

### Setup iniziale

Creare queste label a livello di **Gruppo** per riutilizzarle su tutti i progetti:

#### Status (Stato)
```
Status::Backlog     #6699cc (blu chiaro)
Status::Ready       #428bca (blu)
Status::Doing       #f0ad4e (arancione)
Status::Review      #9b59b6 (viola)
Status::Staging     #3498db (azzurro)
Status::UAT         #e67e22 (arancione scuro)
Status::Done        #5cb85c (verde)
Status::Blocked     #d9534f (rosso)
```

#### Type (Tipo)
```
Type::Feature       #7f8c8d (grigio)
Type::Bug           #e74c3c (rosso)
Type::Task          #95a5a6 (grigio chiaro)
Type::Design        #9b59b6 (viola)
Type::Content       #1abc9c (turchese)
Type::Research      #f39c12 (giallo)
Type::PM            #34495e (grigio scuro)
```

#### Priority (Priorità)
```
Priority::Critical  #c0392b (rosso scuro)
Priority::High      #e74c3c (rosso)
Priority::Medium    #f39c12 (giallo)
Priority::Low       #27ae60 (verde)
```

#### Severity (per bug)
```
Severity::Blocker   #c0392b (rosso scuro)
Severity::Major     #e74c3c (rosso)
Severity::Minor     #f39c12 (giallo)
Severity::Cosmetic  #95a5a6 (grigio)
```

#### Scope
```
Scope::Extra        #8e44ad (viola scuro)
Scope::Garanzia     #2c3e50 (grigio scuro)
```

#### Gate
```
Gate::G1            #3498db (azzurro)
Gate::G2            #9b59b6 (viola)
Gate::G3            #e67e22 (arancione)
Gate::G4            #27ae60 (verde)
```

---

## 3. Issue Board

### Configurazione colonne

Creare board con colonne basate su label `Status::*`:

```
| Backlog | Ready | Doing | Review | Staging | UAT | Done |
```

### Board alternativi (opzionali)

- **By Priority**: colonne per priorità
- **By Type**: colonne per tipo attività
- **By Assignee**: raggruppato per persona

---

## 4. Milestones

### Naming convention

```
[Fase/Sprint] - [Nome descrittivo] (vX.Y)
```

Esempi:
- `Fase 1 - MVP (v1.0)`
- `Sprint 1 - Setup e Login`
- `Sprint 2 - Area Riservata`
- `Hotfix (v1.0.1)`
- `Fase 2 - Evolutive (v2.0)`

### Date

- **Start Date**: inizio lavori su quella milestone
- **Due Date**: deadline (allineata a SAL o gate)

### Milestone standard per progetto nuovo

1. `Fase 0 - Setup e Analisi`
2. `Fase 1 - MVP (v1.0)` → G1 (Wireframe)
3. `Fase 2 - Design` → G2 (Mockup)
4. `Fase 3 - Sviluppo Core`
5. `Fase 4 - UAT` → G3 (UAT)
6. `Fase 5 - Go-Live` → G4 (Accettazione)
7. `Garanzia`

---

## 5. Issue Templates

### Feature Template

Creare file `.gitlab/issue_templates/Feature.md`:

```markdown
## Descrizione
<!-- Cosa deve fare questa funzionalità -->

## User Story
**Come** [tipo utente]
**Voglio** [azione]
**In modo da** [beneficio]

## Criteri di Accettazione
- [ ] **DATO CHE** ... **QUANDO** ... **ALLORA** ...
- [ ] **DATO CHE** ... **QUANDO** ... **ALLORA** ...

## Asset necessari
<!-- Link a grafiche, documenti, API... -->

## Note tecniche
<!-- Considerazioni per lo sviluppo -->

## Stima
<!-- Ore o story point -->

/label ~"Type::Feature" ~"Status::Backlog"
```

### Bug Template

Creare file `.gitlab/issue_templates/Bug.md`:

```markdown
## Descrizione
**Cosa succede**: 
**Cosa dovrebbe succedere**: 

## Passi per riprodurre
1. 
2. 
3. 

## Ambiente
- **Browser**: 
- **Device**: 
- **URL**: 

## Screenshot/Video
<!-- Allegare se disponibile -->

## Severity
<!-- Blocker / Major / Minor / Cosmetic -->

/label ~"Type::Bug" ~"Status::Backlog"
```

### Change Request Template

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
- Costo extra: €

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

/label ~"Type::Feature" ~"Scope::Extra" ~"Status::Backlog"
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
<!-- Punti di attenzione, aree da verificare -->
```

### Regole MR

1. **Sempre da branch a develop** (mai push diretto)
2. **Almeno 1 approvazione** prima di merge
3. **Issue collegata** obbligatoria
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
| `style` | Formattazione, spazi, ecc. |
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

GitLab Free supporta time tracking base:

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

### Visualizzare

Il tempo stimato e speso appare nella sidebar dell'issue.

### Best practice

- Stimare **prima** di iniziare (in fase Ready)
- Registrare tempo **ogni giorno** (o a fine task)
- Il PM usa questi dati per confronto con OpenMemo

---

## 9. Quick Actions Utili

Da usare nei commenti o descrizioni:

| Comando | Effetto |
|---------|---------|
| `/assign @username` | Assegna issue |
| `/unassign` | Rimuove assegnazione |
| `/label ~"Label"` | Aggiunge label |
| `/unlabel ~"Label"` | Rimuove label |
| `/milestone %"Nome"` | Assegna a milestone |
| `/due YYYY-MM-DD` | Imposta scadenza |
| `/estimate Xh` | Stima tempo |
| `/spend Xh` | Registra tempo |
| `/close` | Chiude issue |
| `/reopen` | Riapre issue |
| `/move project/path` | Sposta issue |

---

## 10. Setup Nuovo Progetto

### Checklist

1. [ ] Creare repository con naming corretto
2. [ ] Proteggere branch `main` e `develop`
3. [ ] Creare label (o verificare che esistano a livello gruppo)
4. [ ] Creare milestones iniziali
5. [ ] Configurare issue board
6. [ ] Aggiungere issue templates
7. [ ] Aggiungere MR template
8. [ ] Creare prima issue di setup
9. [ ] Invitare membri del team con ruoli appropriati

### Ruoli suggeriti

| Ruolo GitLab | Chi | Permessi chiave |
|--------------|-----|-----------------|
| Maintainer | PM, Tech Lead | Merge in main, gestione settings |
| Developer | Dev, Designer | Push branch, MR, issue |
| Reporter | Cliente (se accesso) | Solo lettura, commenti |

---

*Questo documento è parte del Sistema Qualità Net7 — ISO 9001:2015*
