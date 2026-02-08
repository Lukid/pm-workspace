---
name: status
description: Mostra status rapido di un progetto
arguments:
  - name: progetto
    description: Nome del progetto (opzionale se in directory progetto)
    required: false
---

# Skill: Status Progetto

Mostra un riepilogo rapido dello stato di un progetto.

## Istruzioni

### 1. Identifica il progetto

Se `$ARGUMENTS` contiene un nome progetto, usa quello.
Altrimenti:
- Controlla se la directory corrente è sotto `projects/`
- Se sì, usa quel progetto
- Se no, mostra lista progetti disponibili e chiedi quale

### 2. Carica il contesto

Leggi in parallelo:
- `projects/[nome]/.project-context.md`
- `projects/[nome]/actions.md`
- `projects/[nome]/raid.md`
- `projects/[nome]/decisions.md`

### 3. Calcola metriche

**Azioni** (riconosci i vari formati usati nei progetti):
- Conta azioni per stato: Completate, In corso, Bloccate, Pendenti
- Identifica azioni scadute (data < oggi e stato != Completato)
- Formati stato riconosciuti: ⏳/🔄/✅ emoji, "Da fare"/"In corso"/"Completata" testo, "DA FARE"/"IN CORSO" caps

**Rischi**:
- Conta rischi attivi per priorità (🔴 Alta, 🟡 Media, 🟢 Bassa)
- Riconosci anche formati testo: "Alta"/"ALTA", P0/P1/P2
- Evidenzia rischi P0/P1 non mitigati

**Decisioni**:
- Conta decisioni pendenti vs prese
- Evidenzia decisioni urgenti (scadenza < 7 giorni)

**Gate**:
- Stato di ogni gate (pending/approved)
- Prossimo gate da raggiungere

### 4. Genera output

```
## [Nome Progetto] — Status

**Cliente**: [cliente]
**Stato**: [In corso / Completato / Sospeso]
**Go-live previsto**: [data] ([N] giorni)

### Semaforo
| Ambito | Tempi | Budget |
|--------|-------|--------|
| 🟢/🟡/🔴 | 🟢/🟡/🔴 | 🟢/🟡/🔴 |

### Gate
- [x] G1 Wireframe — [data]
- [x] G2 Mockup — [data]
- [ ] G3 UAT — previsto [data]
- [ ] G4 Go-live — previsto [data]

### Azioni
- ✅ Completate: [N]
- 🔄 In corso: [N]
- ⚠️ Scadute: [N]
- 📋 Pendenti: [N]

### Rischi Attivi
- 🔴 Critici: [N]
- 🟡 Medi: [N]

### Decisioni Pendenti
- [N] decisioni in attesa ([N] urgenti)

### Prossimi Passi
1. [Azione più urgente]
2. [Azione 2]
3. [Azione 3]
```

### 5. Logica semaforo

| Indicatore | 🟢 Verde | 🟡 Giallo | 🔴 Rosso |
|-----------|----------|-----------|----------|
| **Ambito** | Nessuna CR pendente, scope stabile | CR pendenti o scope in discussione | Scope fuori controllo, multiple CR non approvate |
| **Tempi** | In linea con go-live, nessuna azione scaduta | Ritardo < 1 settimana o azioni scadute < 3 | Ritardo > 1 settimana o azioni scadute >= 3 |
| **Budget** | Nessuna CR approvata che impatta budget | CR approvate < 10% budget originale | CR approvate >= 10% budget originale |

## Varianti

Per uno status più dettagliato, suggerisci:
- `/sal` per report formale completo
- `Apri progetto [nome]` per entrare nel contesto completo
