# Definizioni Operative

Questo documento raccoglie le definizioni standard usate nei progetti Net7.

---

## 1. Definition of Ready (DoR)

Una **attività è pronta** per essere presa in carico dal team se:

### Per Feature/User Story
- [ ] Requisito descritto in modo chiaro e comprensibile
- [ ] Criteri di accettazione definiti (quando possibile in formato Given-When-Then)
- [ ] Asset necessari disponibili (grafiche, testi, API doc, credenziali...)
- [ ] Dipendenze identificate e risolte (o pianificate)
- [ ] Effort stimato (ore o story point)
- [ ] Priorità assegnata
- [ ] Nessun bloccante noto

### Per Bug
- [ ] Descrizione del problema (cosa succede vs cosa dovrebbe succedere)
- [ ] Passi per riprodurre
- [ ] Ambiente dove si verifica (browser, device, staging/prod)
- [ ] Screenshot o video se utile
- [ ] Severity assegnata

---

## 2. Definition of Done (DoD)

Una **attività è completata** quando:

### Per Feature/User Story
- [ ] Codice scritto e committato su branch dedicato
- [ ] Code review superata (approvazione MR)
- [ ] Test funzionali passati (manuali o automatici)
- [ ] Merge in branch principale (develop/main)
- [ ] Deploy in ambiente staging
- [ ] Verifica funzionale su staging
- [ ] Documentazione aggiornata (se necessaria)
- [ ] Issue chiusa con commento di completamento

### Per Bug
- [ ] Fix implementato
- [ ] Test di regressione passato
- [ ] Verificato che il bug non si ripresenta
- [ ] Deploy in staging
- [ ] Issue chiusa con riferimento al commit/MR

### Per Design
- [ ] Mockup/wireframe completati
- [ ] Review interna superata
- [ ] Asset esportati nei formati richiesti
- [ ] Consegnati al team dev / caricati su repository

---

## 3. Severity dei Bug

| Severity | Definizione | Esempi | SLA Risoluzione |
|----------|-------------|--------|-----------------|
| **Blocker** | Impedisce l'uso del sistema o il go-live. Nessun workaround possibile. | Sistema non si avvia, crash all'apertura, perdita dati | Immediato (ore) |
| **Major** | Funzionalità core compromessa. Workaround difficile o assente. | Login non funziona, pagamento fallisce, form principale rotto | 24-48h lavorative |
| **Minor** | Problema presente ma esiste workaround ragionevole. | Bottone in posizione sbagliata ma cliccabile, filtro non funziona ma si può cercare manualmente | Prima del go-live (o backlog post go-live) |
| **Cosmetic** | Problema puramente estetico, non impatta l'uso. | Typo, colore leggermente diverso, spacing non perfetto | Backlog, bassa priorità |

### Note sulla severity
- La severity è proposta da chi segnala, ma **validata dal PM**
- In caso di dubbio, si scala verso l'alto (meglio trattare un Minor come Major che viceversa)
- Durante UAT, il cliente può proporre severity ma Net7 conferma

---

## 4. Priorità

| Priorità | Significato | Quando usare |
|----------|-------------|--------------|
| **Critical** | Da fare immediatamente, blocca tutto il resto | Hotfix produzione, deadline imminente |
| **High** | Da fare nello sprint corrente | Funzionalità core, bug major |
| **Medium** | Da fare presto ma non urgente | Funzionalità importanti, miglioramenti |
| **Low** | Da fare quando c'è tempo | Nice-to-have, ottimizzazioni |

### Priorità vs Severity
- **Severity** = quanto è grave il problema
- **Priorità** = quando va risolto

Un bug può essere Minor (severity) ma High (priorità) se il cliente lo nota sempre.

---

## 5. SLA Standard

### SLA Feedback Cliente

| Tipo documento | Tempo review | Tempo approvazione | Silenzio-assenso |
|----------------|--------------|--------------------|--------------------|
| Wireframe/Scope (G1) | 5 gg lavorativi | 3 gg lavorativi | Sì |
| Mockup UI (G2) | 5 gg lavorativi | 3 gg lavorativi | Sì |
| SAL | 5 gg lavorativi | - | Sì |
| UAT | 5 gg lavorativi | 3 gg lavorativi | Sì |
| Change Request | 5 gg lavorativi | 3 gg lavorativi | No* |

*Le CR richiedono approvazione esplicita perché impattano budget/tempi.

### SLA Risoluzione Bug (durante sviluppo)

| Severity | SLA |
|----------|-----|
| Blocker | Entro 4h lavorative |
| Major | Entro 24h lavorative |
| Minor | Entro fine sprint corrente |
| Cosmetic | Backlog |

### SLA Garanzia (post go-live)

| Severity | SLA risposta | SLA risoluzione |
|----------|--------------|-----------------|
| Blocker | 4h lavorative | 8h lavorative |
| Major | 8h lavorative | 24-48h lavorative |
| Minor | 2 gg lavorativi | Prossimo rilascio |
| Cosmetic | Best effort | Best effort |

---

## 6. Tipi di Attività

### Per GitLab Labels

| Tipo | Descrizione | Label |
|------|-------------|-------|
| **Feature** | Nuova funzionalità nel perimetro | `Type::Feature` |
| **Bug** | Errore rispetto a requisito | `Type::Bug` |
| **Task** | Attività tecnica (setup, refactor...) | `Type::Task` |
| **Design** | Attività di design/grafica | `Type::Design` |
| **Content** | Attività su contenuti | `Type::Content` |
| **Research** | Analisi, spike, PoC | `Type::Research` |
| **PM** | Gestione progetto, riunioni, doc | `Type::PM` |

### Classificazione Scope

| Tipo | Descrizione | Label |
|------|-------------|-------|
| **In Scope** | Nel perimetro contrattuale | (nessuna label speciale) |
| **Extra** | Fuori perimetro, approvato con CR | `Scope::Extra` |
| **Garanzia** | Bug post go-live in garanzia | `Scope::Garanzia` |

---

## 7. Stati del Workflow

### Board GitLab standard

| Stato | Significato | Chi agisce |
|-------|-------------|------------|
| **Backlog** | Da fare, non ancora pronto | PM |
| **Ready** | Pronto per essere preso (soddisfa DoR) | PM → Dev |
| **Doing** | In lavorazione | Dev |
| **Review** | In attesa di code review | Dev → Reviewer |
| **Staging** | Deployato in staging, da verificare | Dev → PM/QA |
| **UAT** | In test con cliente | PM → Cliente |
| **Done** | Completato (soddisfa DoD) | - |
| **Blocked** | Bloccato da dipendenza esterna | PM |

### Transizioni importanti

- `Ready → Doing`: Dev assegna a sé stesso
- `Doing → Review`: Dev apre MR
- `Review → Staging`: MR approvata e mergiata
- `Staging → Done`: Verificato funzionante
- Qualsiasi → `Blocked`: Aggiungere commento con motivo del blocco

---

## 8. Formati Standard

### Criteri di Accettazione (Given-When-Then)

```markdown
**DATO CHE** [contesto iniziale / precondizione]
**QUANDO** [azione dell'utente]
**ALLORA** [risultato atteso, verificabile]
```

Esempio:
```markdown
**DATO CHE** sono un utente registrato sulla pagina di login
**QUANDO** inserisco email e password corretti e clicco "Accedi"
**ALLORA** vengo reindirizzato alla dashboard e vedo il mio nome in alto a destra
```

### Descrizione Bug

```markdown
## Descrizione
[Cosa succede vs cosa dovrebbe succedere]

## Passi per riprodurre
1. [Passo 1]
2. [Passo 2]
3. ...

## Ambiente
- Browser: [es. Chrome 120]
- Device: [es. Desktop Windows / iPhone 14]
- URL: [link alla pagina]

## Screenshot/Video
[Allegare se utile]

## Severity proposta
[Blocker / Major / Minor / Cosmetic]
```

### Change Request (formato breve)

```markdown
## CR-XXX: [Titolo]

**Richiesto da**: [Nome]
**Data richiesta**: [Data]

### Descrizione
[Cosa viene richiesto]

### Motivazione
[Perché serve]

### Impatto
- **Effort**: [ore/giorni]
- **Costo**: [€]
- **Tempi**: [impatto su timeline]

### Decisione
[ ] Approvato | [ ] Rifiutato | [ ] In valutazione
```

---

## 9. Nomenclature

### Progetti (directory)

```
[cliente]-[nome-breve]
```
Esempi: `anci-portale-cittadino`, `comune-firenze-sito`, `privato-ecommerce-shoes`

### Branch Git

```
[tipo]/[issue-id]-[descrizione-breve]
```
Esempi: `feature/123-login-sso`, `bugfix/456-fix-header`, `hotfix/789-crash-checkout`

### Milestone GitLab

```
[Fase] - [Nome] (vMajor.Minor)
```
Esempi: `MVP - Lancio v1.0`, `Sprint 3 - Area Riservata`, `Hotfix v1.0.1`

### Issue GitLab

```
[Tipo] [Descrizione breve]
```
Esempi: `[Feature] Login con SPID`, `[Bug] Header non responsive su mobile`

### Documenti

```
[AAAA-MM-DD]-[tipo]-[descrizione].md
```
Esempi: `2025-01-15-SAL-gennaio.md`, `2025-01-20-CR-001-nuova-sezione.md`

---

*Questo documento è parte del Sistema Qualità Net7 — ISO 9001:2015*
