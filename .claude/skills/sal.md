---
name: sal
description: Genera SAL (Stato Avanzamento Lavori) per un progetto
arguments:
  - name: progetto
    description: Nome del progetto (opzionale se in directory progetto)
    required: false
  - name: periodo
    description: "Periodo del SAL (es: '15-31 gennaio' o 'ultima settimana')"
    required: false
---

# Skill: Genera SAL

Genera un documento SAL (Stato Avanzamento Lavori) per il progetto specificato.

## Istruzioni

### 1. Identifica il progetto

Se `$ARGUMENTS` contiene un nome progetto, usa quello.
Altrimenti:
- Controlla se la directory corrente è sotto `projects/`
- Se sì, usa quel progetto
- Se no, chiedi all'utente quale progetto

### 2. Carica il contesto del progetto

Leggi i seguenti file dalla directory del progetto:
- `.project-context.md` — metadata progetto (nome, cliente, budget, stato gate)
- `actions.md` — azioni in corso e completate
- `raid.md` — rischi, assunzioni, issue, dipendenze
- `decisions.md` — decisioni prese
- `changes/` — eventuali CR attive

### 3. Determina il periodo

Se specificato in `$ARGUMENTS`, usa quel periodo.
Altrimenti usa le ultime 2 settimane dalla data odierna.

### 4. Identifica il numero SAL

Conta i file esistenti in `sal/` per determinare il numero progressivo.

### 5. Genera il SAL

Usa il template `templates/sal.md` e compila:

**Sezione 1 - Riepilogo Esecutivo**:
- Sintesi in 2-3 frasi dello stato generale
- Evidenzia se siamo in linea o ci sono criticità

**Sezione 2 - Stato Generale**:
- Ambito: 🟢 se scope stabile, 🟡 se ci sono CR pendenti, 🔴 se scope fuori controllo
- Tempi: 🟢 se in linea con timeline, 🟡 se ritardi < 1 settimana, 🔴 se ritardi > 1 settimana
- Budget: 🟢 se nessuna CR, 🟡 se CR < 10% budget, 🔴 se CR > 10% budget

**Sezione 3 - Attività Completate**:
- Estrai da `actions.md` le azioni con stato "Completato" nel periodo

**Sezione 4 - Attività in Corso**:
- Estrai da `actions.md` le azioni con stato "In corso"
- Stima avanzamento % se possibile

**Sezione 5 - Milestone**:
- Usa i gate da `.project-context.md`
- Aggiungi milestone significative

**Sezione 6 - Criticità e Rischi**:
- Estrai da `raid.md` i rischi con priorità Alta o Media
- Aggiungi criticità emerse nel periodo

**Sezione 7 - Decisioni Richieste**:
- Estrai da `decisions.md` le decisioni pendenti
- Evidenzia conseguenze se non deciso

**Sezione 8 - Change Request**:
- Lista CR dalla directory `changes/`

**Sezione 9 - Prossimi Passi**:
- Prossime 3-5 attività pianificate
- Assegna responsabile e scadenza

**Sezione 10 - Quadro Economico**:
- Solo se dati disponibili in project-context

### 6. Salva il documento

Salva in: `projects/[nome-progetto]/sal/SAL-[YYYY-MM-DD].md`

### 7. Output finale

Conferma:
```
SAL generato: sal/SAL-[data].md

Riepilogo:
- Periodo: [periodo]
- Stato: [🟢/🟡/🔴]
- Attività completate: [N]
- Rischi attivi: [N]
- Decisioni pendenti: [N]
```

## Esempi di utilizzo

```
/sal
/sal anci-cittadino-informato
/sal anci-cittadino-informato 15-31 gennaio
/sal periodo ultima settimana
```
