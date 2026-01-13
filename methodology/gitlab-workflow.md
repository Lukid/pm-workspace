# Vademecum GitLab per la gestione dei task di progetto

> Processo e workflow per la gestione operativa delle Issue in GitLab.

---

## 1. Obiettivo e principi

Questo documento è pensato per chi lavora su più progetti e ha bisogno di un sistema unico, ripetibile e verificabile per governare richieste, delivery e manutenzione.

### 1.1 Come leggere il workflow

- **Le colonne del Board rappresentano lo stato "reale" del lavoro**, non l'intenzione.
- Uno stato deve rispondere a una domanda semplice:
  - *È pronto da fare?* (*Ready*)
  - *È in lavorazione?* (*In progress*)
  - *È in attesa di review/QA/deploy?*
- Le eccezioni (bloccato, attesa info) non diventano nuove colonne: sono **etichette di condizione**. Questo evita board troppo lunghi e riduce l'ambiguità.

### 1.2 Perché separiamo priorità e urgenza

- **Priorità**: cosa facciamo prima rispetto al resto (governo del backlog).
- **Urgenza**: entro quando dobbiamo reagire/prendere in carico (SLA).

Esempio pratico:
- Un refactor importante può avere priorità alta ma urgenza bassa (lo pianifichi).
- Un incident può avere urgenza massima e priorità massima (si interrompe tutto).

### 1.3 Principi fondamentali

- Un task deve essere **tracciabile** (chi, cosa, quando, perché)
- Gli stati devono essere **pochi ma operativi** (evitare varianti inutili)
- Priorità = *ordine di esecuzione*; Urgenza = *tempo massimo di risposta*
- Ogni Issue deve avere un **owner** e un **criterio di completamento**

---

## 2. Modello organizzativo GitLab

### 2.1 Struttura dei Group

Il GitLab è organizzato **per tipologia applicativa**, non per cliente.

Struttura obbligatoria:
- **Group di primo livello** = tecnologia/framework
  - `laravel/`
  - `drupal/`
  - `wordpress/`

### 2.2 Struttura dei Project

All'interno di ogni Group:
- **Un Project per applicazione**
- Se l'architettura lo richiede, il progetto può essere **suddiviso ulteriormente**:
  - `nome-app-frontend`
  - `nome-app-backend`

Decisione: **i task di progetto vivono sempre nel Project più vicino al codice**.

Esempio:
- Task frontend → Project frontend
- Task API → Project backend
- Task trasversale → Project backend (come riferimento principale)

### 2.3 Regola sulla duplicazione delle Issue

- È **vietato duplicare Issue** tra Project diversi.
- Se un lavoro impatta più Project:
  - si crea **una Issue principale**
  - gli altri Project ricevono **Issue collegate** con riferimento esplicito (`relates to #ID`).

---

## 3. Stati di avanzamento

### 3.1 Stati standard (colonne Board)

Workflow unico per la maggior parte delle Issue:

1. **Backlog** — Idee/richieste raccolte, non pronte.
2. **Triage** — Classificazione: tipo, impatto, urgenza, info mancanti.
3. **Ready** — Requisiti completi, definito "cosa significa finito", pronto per essere preso in carico.
4. **In progress** — Lavorazione attiva.
5. **In review** — MR aperta, code review in corso.
6. **QA / Validation** — Test funzionali / regressione / UAT.
7. **Ready to deploy** — Approvato e in attesa di rilascio (o in finestra release).
8. **Done** — Rilasciato/chiuso.

### 3.2 Regole di transizione

- Un'Issue può stare in **In progress** solo se ha un **assignee**.
- Si entra in **Ready** solo se:
  - criteri di accettazione presenti
  - priorità e urgenza impostate
  - dipendenze note
- **Done** solo quando:
  - merge completato + deploy effettuato (o consegna effettuata)
  - note di rilascio/diagnostica aggiornate se necessario

### 3.3 Stati speciali (eccezioni)

- **Blocked** (label) quando c'è un impedimento esterno o dipendenza.
- **Waiting for input** (label) quando servono informazioni dal richiedente.
- **Won't do** (chiusura con motivazione) quando non si procede.

Decisione: **non** creiamo colonne aggiuntive per Blocked/Waiting; usiamo label per non proliferare stati.

---

## 4. Iter di assegnazione e responsabilità

### 4.1 Ruoli ufficiali

I ruoli sono **funzionali**, non legati al job title.

| Ruolo | Responsabilità |
|-------|----------------|
| **Requester / Triager (PM)** | Apre la Issue, governa il backlog, decide priorità/urgenza/milestone, risponde ai chiarimenti, responsabile della qualità funzionale |
| **Assignee** | Unico responsabile dell'esecuzione tecnica, aggiorna lo stato |
| **Reviewer** | Valida il codice e la qualità tecnica |

Decisione: **una Issue ha sempre un solo Assignee**. Il ruolo di Requester e Triager coincide.

### 4.2 Flusso obbligatorio di assegnazione

1. **Creazione Issue**
   - Stato iniziale: **Backlog**
   - Nessun assignee

2. **Triage**
   - Stato: **Triage**
   - Il Triager assegna: `type::*`, `priority::*`, `urgency::*`, milestone (se prevista)

3. **Ready**
   - L'Issue è completa e lavorabile
   - Solo il Triager può spostare in Ready

4. **Assegnazione**
   - Due modalità ufficiali:
     - **Pull**: l'Assignee prende una Issue da Ready
     - **Push**: il PM, tipicamente dopo lo Scrum, assegna direttamente
   - In entrambi i casi: un solo assignee, Issue spostata in **In progress**

5. **Review → QA → Deploy → Done**
   - Avanzamento sequenziale senza salti

### 4.3 Regole di lavoro

- Una Issue in **In progress**:
  - deve avere un assignee
  - non può restare ferma oltre un certo tempo senza commenti o motivazioni
- **WIP limit**: massimo **2** Issue in progress per persona

---

## 5. Regole per la scrittura di una Issue

Ogni Issue **deve** essere scritta in modo chiaro, completo e verificabile. Una Issue scritta male **non può** avanzare oltre *Backlog/Triage*.

### 5.1 Titolo

- Deve descrivere **azione + oggetto + contesto**
- Deve essere comprensibile senza leggere la descrizione

| Corretto | Errato |
|----------|--------|
| "Aggiungere validazione email in form registrazione" | "Bug login" |
| "Correggere errore 500 su salvataggio ordine" | "Problema form" |

### 5.2 Descrizione

La descrizione **deve** includere:
- **Contesto**: perché esiste la richiesta
- **Obiettivo**: cosa deve cambiare
- **Ambito**: cosa è incluso ed esplicitamente escluso

Se queste informazioni mancano, l'Issue resta in **Triage**.

### 5.3 Criteri di accettazione

- I criteri di accettazione **sono obbligatori** per tutte le Issue tranne i bug banali
- Devono essere: chiari, verificabili, possibilmente espressi come elenco puntato

Formato consigliato:
> Dato **X**, quando **Y**, allora **Z**

Un'Issue **non può** essere spostata in **Ready** senza criteri di accettazione.

### 5.4 Dipendenze tra Issue

- Ogni dipendenza **deve essere esplicitata**
- Gestione: `depends on #ID`, `blocked by #ID` + label `status::blocked`
- Se una Issue dipende da un'altra, **non può** essere in *In progress*
- La rimozione dello stato di blocco deve essere commentata

### 5.5 Collegamento al codice

- Link a MR quando applicabile
- Link a documentazione, design o ticket esterni
- La MR **deve** referenziare l'Issue (es. `Closes #ID`)

### 5.6 Qualità minima

Un'Issue è considerata "scritta correttamente" solo se:
- È comprensibile a una persona esterna al contesto
- Contiene abbastanza informazioni per essere stimata e implementata
- Non richiede chiarimenti immediati

---

## 6. Gestione di urgenza e priorità

### 6.1 Label standard

**Priorità (obbligatoria)**

| Label | Descrizione |
|-------|-------------|
| `priority::critical` | Blocco business / produzione giù |
| `priority::high` | Molto importante (rischio alto) |
| `priority::medium` | Normale |
| `priority::low` | Bassa / nice-to-have |

**Urgenza (obbligatoria)**

| Label | Descrizione |
|-------|-------------|
| `urgency::immediate` | Intervento immediato (incident / hotfix) |
| `urgency::short-term` | Presa in carico entro 1 giorno lavorativo |
| `urgency::normal` | Presa in carico entro 3 giorni lavorativi |
| `urgency::planned` | Pianificabile senza impatti immediati |

**Impatto (consigliata)**

- `impact::high` / `impact::medium` / `impact::low`

**Stato "non-colonna" (label)**

- `status::blocked`
- `status::waiting-input`

### 6.2 Matrice decisionale rapida

| Situazione | Priority | Urgency | Type |
|------------|----------|---------|------|
| Produzione giù | `critical` | `immediate` | `incident` |
| Bug serio ma workaround disponibile | `high` | `short-term` | `bug` |
| Miglioria richiesta dal cliente | `medium`/`low` | `normal`/`planned` | `feature` |

---

## 7. Gestione post-rilascio e manutenzione

### 7.1 Classificazione obbligatoria

Ogni Issue post-rilascio deve appartenere a **una sola** categoria:
- **Bug post-rilascio** (`type::bug`)
- **Incident / Hotfix** (`type::incident`)
- **Manutenzione programmata** (`type::task`)

### 7.2 Bug post-rilascio (non bloccante)

- Priorità: `priority::high` o `priority::medium`
- Urgenza: `urgency::short-term`, `urgency::normal` o `urgency::planned`
- Inserimento nella **milestone del prossimo rilascio utile**

### 7.3 Incident / Hotfix (bloccante)

Condizioni:
- Produzione non funzionante
- Perdita dati
- Rischio sicurezza

Regole operative:
1. Apertura immediata Issue
2. `priority::critical` + `urgency::immediate`
3. Assegnazione immediata
4. Fix, review rapida, deploy
5. Chiusura Issue con descrizione della causa
6. Apertura Issue di prevenzione se necessario

### 7.4 Manutenzione programmata

- Sempre pianificata
- Mai gestita come hotfix
- Inserita in milestone dedicata (es. `Maintenance Q1`)

---

## 8. Definition of Done (DoD) vincolante

Ogni Issue è "Done" solo se:
- [ ] Criteri di accettazione soddisfatti
- [ ] MR mergeata e pipeline verde
- [ ] Test aggiornati/aggiunti quando opportuno
- [ ] Documentazione aggiornata se cambia comportamento
- [ ] Log/monitoring considerati per bug/incident importanti

---

## 9. Templates Issue

### 9.1 Template "Task/Feature"

```markdown
## Contesto
[Perché esiste questa richiesta]

## Obiettivo
[Cosa deve cambiare]

## Criteri di accettazione
- [ ] Dato X, quando Y, allora Z
- [ ] ...

## Impatto
[Utenti/aree coinvolte]

## Note tecniche / dipendenze
[Considerazioni per lo sviluppo]

## Checklist
- [ ] ...
```

### 9.2 Template "Bug/Incident"

```markdown
## Ambiente
[prod/stage]

## Descrizione del problema
[Cosa succede]

## Passi per riprodurre
1. ...
2. ...

## Comportamento atteso vs reale
- **Atteso**: ...
- **Reale**: ...

## Impatto
[Utenti/aree coinvolte]

## Log/screenshot/link
[Allegati]

## Workaround
[Se disponibile]
```

---

## 10. Boards

| Board | Scopo | Filtro |
|-------|-------|--------|
| **Delivery (default)** | Colonne = stati (Backlog → Done) | — |
| **Triage** | Issue da classificare o bloccate | `status::waiting-input` + `status::blocked` |
| **Incident & Hotfix** | Emergenze | `type::incident` OR `urgency::immediate` |
| **Per area** | Focus per team | `area::*` (frontend, backend, devops, data) |

---

## 11. Routine operative (cadence)

| Attività | Frequenza | Durata |
|----------|-----------|--------|
| Triage | Giornaliero | 15-20 min |
| Planning | Settimanale o per sprint | — |
| Review backlog | Ogni 2 settimane | — |
| Retro/post-mortem | Dopo incident P0/U0 | — |

I check periodici:
- **Non sono opzionali**
- Fanno parte integrante del processo
- Verificano: qualità Issue, rispetto workflow, uso corretto etichette, efficacia delivery
- **Devono essere tracciati tramite Issue dedicate**

---

## 12. Schema operativo (end-to-end)

### 12.1 Flusso standard (Feature/Task)

1. **Apertura e Triage iniziale** (PM)
   - Usa template
   - Descrive obiettivo + contesto
   - Assegna `type::*`, `priority::*`, `urgency::*` (eventuale `impact::*`)
   - Assegna area (`area::*`)
   - Definisce criteri di accettazione
   - Se mancano info → `status::waiting-input` + domande in commento

2. **Ready** — L'Issue è "eseguibile"

3. **Presa in carico** (Assignee)
   - Assegna a sé stesso (pull) o viene assegnato (push)
   - Sposta in **In progress**

4. **Merge Request e Review**
   - Crea MR collegata
   - Sposta Issue in **In review**

5. **QA / Validation**
   - Test funzionali/regressione/UAT

6. **Ready to deploy** — Approvata e pronta

7. **Deploy + Done**
   - Deploy completato
   - Note di rilascio aggiornate se necessario
   - Chiusura automatica con "Closes #ID"

### 12.2 Flusso standard (Bug)

1. Apertura Issue con template bug (riproduzione + impatto)
2. Triage (severità, workaround, ambiente)
3. Se urgente → trattare come hotfix (sezione 12.3)
4. Altrimenti → pianificare in milestone del prossimo rilascio

### 12.3 Flusso Hotfix / Incident

1. **Apertura immediata Issue**
   - `type::incident` o `type::bug` + `urgency::immediate` + `priority::critical`
2. **Assegnazione rapida** (owner tecnico)
3. **Fix su branch appropriato** (es. release/hotfix)
4. **Review rapida** (1 reviewer) + pipeline verde
5. **QA mirata** sul perimetro impattato
6. **Deploy** e verifica (log/monitoring)
7. **Chiusura** con riepilogo causa e soluzione
8. **Post-mortem** (solo P0/U0) con azioni preventive tracciate come nuove Issue

---

## 13. Checklist di configurazione GitLab

### 13.1 Setup iniziale

- [ ] Creare Group di primo livello per tecnologia (`laravel/`, `drupal/`, `wordpress/`)
- [ ] Creare Project per applicazione (eventuale separazione frontend/backend)
- [ ] Creare tutte le **label standard** definite nel documento
- [ ] Creare **Milestone** per rilasci o periodi di lavoro
- [ ] Creare **Board "Delivery"** con tutte le colonne di stato ufficiali
- [ ] Creare **Board dedicate** (Triage, Incident & Hotfix, Area)
- [ ] Inserire e rendere obbligatori gli **Issue Template**

### 13.2 Regole da comunicare al team

- Ogni Issue deve usare un template ufficiale
- Nessuna Issue va in **Ready** senza criteri di accettazione
- Una Issue in **In progress** deve avere un solo assignee
- Le dipendenze devono essere sempre esplicitate e tracciate
- Le label di priorità e urgenza sono obbligatorie
- Le Issue bloccate devono avere commento esplicativo

### 13.3 Misure di controllo (minime)

- Triage giornaliero del backlog
- Verifica settimanale delle Issue bloccate
- Monitoraggio Issue in In progress > 2 giorni
- Retrospettiva obbligatoria dopo ogni Incident / Hotfix

---

## 14. Esempi e casi tipici

### 14.1 Richiesta cliente vaga

- Stato: **Backlog** → **Triage**
- Azione: aggiungere domande e `status::waiting-input`
- Quando arriva risposta: rimuovere label e portare a **Ready**

### 14.2 Task pronto ma bloccato da terzi

- Stato: può restare in **Ready** o **In progress** (se già iniziato)
- Label: `status::blocked`
- Commento obbligatorio: cosa blocca + prossima azione + owner esterno

### 14.3 Bug post-rilascio con workaround

- `type::bug`, `impact::*` coerente
- `priority::high` (se serio) ma `urgency::short-term/normal` se workaround disponibile
- Pianificazione in milestone del prossimo rilascio

---

## Allegato: set completo di label

```
type::task
type::feature
type::bug
type::incident

priority::critical
priority::high
priority::medium
priority::low

urgency::immediate
urgency::short-term
urgency::normal
urgency::planned

impact::high
impact::medium
impact::low

status::blocked
status::waiting-input

area::frontend
area::backend
area::devops
area::data
```

---

*Documento parte del PM Workspace — Net7*
