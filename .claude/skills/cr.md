---
name: cr
description: Crea Change Request con analisi di impatto
arguments:
  - name: descrizione
    description: "Descrizione della richiesta di modifica"
    required: true
---

# Skill: Change Request

Crea un documento CR formale con analisi di impatto completa.

## Istruzioni

### 1. Identifica il progetto

Se c'è un progetto attivo in sessione, usa quello.
Altrimenti chiedi all'utente quale progetto.

### 2. Carica contesto

Leggi:
- `.project-context.md` — budget, timeline, scope
- `changes/` — conta CR esistenti per numerazione progressiva
- `actions.md` — per capire impatto su attività in corso

### 3. Raccogli informazioni

Dall'argomento dell'utente o chiedendo (max 3 domande):
1. **Cosa viene richiesto** e **chi lo richiede**
2. **Motivazione** (valore di business)
3. **Effort stimato** (ore/giorni) e **impatto su timeline**

Se l'utente non ha tutti i dati, usa placeholder "[DA STIMARE]".

### 4. Calcola numerazione

Formato: `CR-[ANNO]-[NNN]` progressivo (es: CR-2026-001).

### 5. Genera il documento

Usa il template sotto. Compila tutto ciò che puoi dai dati disponibili.

### 6. Salva

Salva in: `projects/[nome]/changes/CR-[ANNO]-[NNN]-[slug].md`

Dove `[slug]` è una versione kebab-case della descrizione (max 3-4 parole).

### 7. Suggerisci prossimi passi

```
CR creata: changes/CR-[id]-[slug].md

Prossimi passi:
1. Completa la stima di effort se mancante
2. Invia al cliente per approvazione
3. Attendi conferma scritta PRIMA di iniziare il lavoro
```

---

## Template CR

```markdown
# Change Request

---

| Campo | Valore |
|-------|--------|
| **CR ID** | CR-[ANNO]-[NNN] |
| **Progetto** | [Nome progetto] |
| **Data richiesta** | [YYYY-MM-DD] |
| **Richiedente** | [Nome e ruolo] |
| **Priorità** | 🔴/🟡/🟢 |
| **Stato** | Aperta |

---

## 1. Descrizione della Modifica

### Cosa viene richiesto
[Descrizione chiara della modifica. Cosa deve fare il sistema che oggi non fa?]

### Riferimento
- [Email/Call/Riunione del [data]]

---

## 2. Motivazione

**Perché serve**: [Valore di business, problema che risolve]

**Se non si fa**: [Impatto del non fare la modifica]

---

## 3. Analisi di Impatto

### Tempi
| Aspetto | Valore |
|---------|--------|
| Data consegna attuale | [Data] |
| Ritardo stimato | [N giorni] |
| Nuova data prevista | [Data] |

### Costi
| Aspetto | Valore |
|---------|--------|
| Effort aggiuntivo | [N ore/giorni] |
| Costo extra | €[importo] + IVA |

### Scope e rischi
[Impatto su funzionalità esistenti, rischi introdotti]

---

## 4. Alternative

| Alternativa | Pro | Contro | Costo |
|-------------|-----|--------|-------|
| A: Implementazione completa | [Pro] | [Contro] | €[X] |
| B: Implementazione ridotta | [Pro] | [Contro] | €[X] |
| C: Non implementare | Nessun costo | [Cosa si perde] | €0 |

---

## 5. Raccomandazione

[Opinione del PM: quale alternativa e perché]

---

## 6. Decisione

- [ ] **APPROVATA** — Procedere con implementazione
- [ ] **APPROVATA CON MODIFICHE** — Specificare: [...]
- [ ] **RINVIATA** — Rivalutare il [data]
- [ ] **RIFIUTATA** — Motivazione: [...]

---

## Approvazione

| Ruolo | Nome | Data |
|-------|------|------|
| PM Net7 | [Nome] | |
| Referente Cliente | [Nome] | |

> **Nessuna attività relativa a questa CR verrà avviata prima dell'approvazione scritta.**

---

*Documento generato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
```
