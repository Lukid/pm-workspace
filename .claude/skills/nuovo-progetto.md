---
name: nuovo-progetto
description: Crea un nuovo progetto con struttura canonica e formati standard
arguments:
  - name: nome
    description: "Nome del progetto in kebab-case (es: anci-cittadino-informato)"
    required: true
---

# Skill: Nuovo Progetto

Crea la struttura completa di un nuovo progetto con tutti i file in formato canonico.

## Istruzioni

### 1. Valida il nome

Il nome deve essere in kebab-case (minuscole, trattini). Se l'utente passa un nome diverso, convertilo automaticamente.
Esempio: "Portale ANCI" → `portale-anci`

Verifica che `projects/[nome]/` non esista già.

### 2. Raccogli informazioni base

Chiedi (usa AskUserQuestion con max 4 domande):

1. **Nome progetto completo** e **cliente**
2. **Tipo**: PA o Privato?
3. **Budget** e **data go-live prevista**
4. **PM** e **team** (nomi e ruoli principali)

### 3. Crea la struttura directory

```
projects/[nome]/
├── .project-context.md
├── actions.md
├── raid.md
├── decisions.md
├── gates/
├── sal/
├── changes/
├── comms/
├── context/
├── uat/
└── golive/
```

### 4. Genera i file con formati canonici

Usa ESATTAMENTE i template sotto. Non inventare formati diversi.

---

## Template: .project-context.md

```markdown
---
project_name: "[Nome completo]"
client: "[Cliente]"
pm: "[PM]"
status: "in-corso"
type: "[pa|privato]"
start_date: "[YYYY-MM-DD]"
target_golive: "[YYYY-MM-DD]"
budget: [importo numerico]
cig: ""
gitlab_project: ""
gates:
  G1: { stato: pending, data: null }
  G2: { stato: pending, data: null }
  G3: { stato: pending, data: null }
  G4: { stato: pending, data: null }
---

# [Nome Progetto]

## Scope

[Descrizione sintetica del progetto e degli obiettivi principali]

## Team

### Net7
| Ruolo | Nome |
|-------|------|
| PM | [Nome] |
| Tech Lead | [Nome] |
| Dev | [Nome] |
| Designer | [Nome] |

### Cliente
| Ruolo | Nome | Email |
|-------|------|-------|
| Sponsor/RUP | [Nome] | [Email] |
| Referente operativo | [Nome] | [Email] |

## Link Utili

- GitLab: [URL]
- Figma: [URL]
- Staging: [URL]
- Drive: [URL]

## Note

[Informazioni importanti, vincoli, peculiarità del cliente]
```

## Template: actions.md

```markdown
# Azioni — [Nome Progetto]

## Azioni Aperte

| ID | Azione | Owner | Scadenza | Priorità | Stato | Note |
|----|--------|-------|----------|----------|-------|------|

## Azioni Completate

| ID | Azione | Owner | Completata il | Note |
|----|--------|-------|---------------|------|
```

## Template: raid.md

```markdown
# RAID — [Nome Progetto]

## Rischi

| ID | Rischio | Prob. | Impatto | Priorità | Mitigazione | Owner | Stato |
|----|---------|-------|---------|----------|-------------|-------|-------|

**Stati**: Aperto | Mitigato | Chiuso | Verificato (→ diventa Issue)

## Assunzioni

| ID | Assunzione | Impatto se falsa | Owner | Stato |
|----|------------|------------------|-------|-------|

**Stati**: Da verificare | Valida | Invalida

## Issue

| ID | Issue | Impatto | Azione | Owner | Scadenza | Stato |
|----|-------|---------|--------|-------|----------|-------|

**Stati**: Aperta | In corso | Risolta | Escalata

## Dipendenze

| ID | Dipendenza | Da chi/cosa | Impatto | Data necessaria | Stato |
|----|------------|-------------|---------|-----------------|-------|

**Stati**: In attesa | Sollecitata | Ricevuta | Bloccata
```

## Template: decisions.md

```markdown
# Decisioni — [Nome Progetto]

## Decisioni Pendenti

| ID | Tema | Opzioni | Scadenza | Conseguenza se non deciso |
|----|------|---------|----------|---------------------------|

## Decisioni Prese

| ID | Data | Decisione | Contesto | Decisori | Impatto |
|----|------|-----------|----------|----------|---------|
```

## Convenzioni (da rispettare sempre)

- **Priorità**: 🔴 Alta, 🟡 Media, 🟢 Bassa (solo emoji, mai testo)
- **Stato azioni**: ⏳ Da fare, 🔄 In corso, ✅ Completata (solo emoji)
- **Date**: YYYY-MM-DD
- **ID**: A-001, R-001, I-001, D-001 (con prefisso categoria)
- **File naming**: kebab-case

### 5. Output finale

```
Progetto creato: projects/[nome]/

File generati:
- .project-context.md (source of truth)
- actions.md
- raid.md
- decisions.md
- Directory: gates/, sal/, changes/, comms/, context/, uat/, golive/

Prossimi passi:
1. Completa .project-context.md con link e dettagli mancanti
2. Genera il brief con `Genera brief`
3. Avvia la fase di analisi e wireframing
```
