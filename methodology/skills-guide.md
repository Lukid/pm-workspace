# Skills Guide — PM Workspace

Le skills sono comandi rapidi invocabili con `/nome` che automatizzano operazioni frequenti.

---

## Skills Disponibili

| Skill | Descrizione | File |
|-------|-------------|------|
| `/status` | Status rapido progetto | `.claude/skills/status.md` |
| `/sal` | Genera SAL completo | `.claude/skills/sal.md` |

---

## Come Usare le Skills

### Sintassi Base

```bash
/nome-skill [argomenti opzionali]
```

### Esempi

```bash
# Status progetto corrente
/status

# Status progetto specifico
/status anci-cittadino-informato

# SAL con periodo esplicito
/sal ispro 15-31 gennaio

# SAL ultime 2 settimane (default)
/sal sviluppo-toscana
```

### Contesto Automatico

Se sei nella directory di un progetto, le skills lo rilevano automaticamente:

```bash
cd projects/anci-cittadino-informato
/status  # usa automaticamente anci-cittadino-informato
```

---

## Creare Nuove Skills

### Struttura File

Le skills sono file markdown in `.claude/skills/` con frontmatter YAML:

```markdown
---
name: nome-skill
description: Descrizione breve
arguments:
  - name: argomento1
    description: Cosa fa questo argomento
    required: false
  - name: argomento2
    description: Altro argomento
    required: true
---

# Skill: Nome Skill

[Istruzioni dettagliate per Claude]
```

### Elementi Chiave

1. **Frontmatter** — Metadata YAML obbligatorio
2. **Istruzioni** — Passo-passo dettagliato
3. **Esempi** — Come invocare la skill
4. **Output** — Formato atteso dell'output

### Variabili Disponibili

- `$ARGUMENTS` — Argomenti passati dall'utente
- Directory corrente rilevabile con tool standard

### Best Practices

1. **Istruzioni chiare**: Scrivi come se spiegassi a un collega
2. **Gestisci i casi edge**: Cosa fare se manca un file?
3. **Output consistente**: Definisci formato di output prevedibile
4. **Fallback ragionevoli**: Se manca un argomento, usa default sensati

---

## Esempio Completo: Skill `/cr`

```markdown
---
name: cr
description: Crea una Change Request
arguments:
  - name: descrizione
    description: Breve descrizione della CR
    required: true
  - name: progetto
    description: Nome progetto (opzionale se in directory)
    required: false
---

# Skill: Crea Change Request

## Istruzioni

### 1. Identifica il progetto
[come per altre skills]

### 2. Determina numero CR
Conta file in `changes/` per numero progressivo.

### 3. Raccogli informazioni
Chiedi all'utente:
- Descrizione dettagliata
- Impatto su scope/tempi/budget
- Urgenza

### 4. Genera CR
Usa template `templates/change-request.md`

### 5. Salva
`changes/CR-[NNN]-[slug].md`

### 6. Output
Conferma creazione e prossimi passi (approvazione cliente)
```

---

## Skills Suggerite per il Futuro

| Skill | Descrizione | Priorità |
|-------|-------------|----------|
| `/cr` | Crea Change Request | Alta |
| `/gate` | Prepara documento gate | Alta |
| `/azione` | Aggiungi azione con wizard | Media |
| `/rischio` | Aggiungi rischio con wizard | Media |
| `/sync` | Alias per sincronizza GitLab | Media |
| `/brief` | Genera project brief | Bassa |

---

## Differenza tra Skills e Comandi

| Aspetto | Comandi Testuali | Skills |
|---------|------------------|--------|
| Invocazione | Frase libera | `/nome` |
| Parsing | Interpretazione NL | Argomenti strutturati |
| Documentazione | CLAUDE.md | File dedicato |
| Estensibilità | Modifica CLAUDE.md | Aggiungi file in skills/ |

Le skills sono preferibili per operazioni:
- Frequenti
- Con output standardizzato
- Che beneficiano di wizard/prompt guidati

---

*Ultimo aggiornamento: Febbraio 2026*
