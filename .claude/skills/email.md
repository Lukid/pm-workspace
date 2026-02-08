---
name: email
description: Bozza email/comunicazione al cliente con contesto progetto
arguments:
  - name: argomento
    description: "Cosa comunicare (es: 'sollecito approvazione G2', 'segnalare ritardo API')"
    required: true
---

# Skill: Email Cliente

Genera una bozza email professionale al cliente, sfruttando il contesto del progetto attivo.

## Istruzioni

### 1. Identifica il progetto

Se c'è un progetto attivo in sessione, usa quello.
Altrimenti chiedi all'utente quale progetto.

### 2. Carica contesto

Leggi:
- `.project-context.md` — nomi, ruoli, contatti
- `actions.md` — per azioni in corso se rilevante
- `raid.md` — per rischi/issue se rilevante
- Ultimo SAL in `sal/` — per contesto recente

### 3. Identifica il tipo di email

Dall'argomento dell'utente, determina quale pattern usare:

| Tipo | Quando |
|------|--------|
| Richiesta approvazione | Gate, SAL, deliverable da approvare |
| Segnalazione problema | Ritardi, blocchi, rischi concretizzati |
| Sollecito | Cliente non risponde |
| Chiusura SAL | Invio SAL periodico |
| Scope / CR | Cliente chiede qualcosa fuori perimetro |
| Escalation | Blocco prolungato, rischio grave |
| Informativa | Aggiornamento, comunicazione generica |

### 4. Genera la bozza

Usa la struttura e il tono appropriati (vedi sotto).

### 5. Output

Presenta la bozza in formato copy-paste. Alla fine suggerisci:
- Se archiviare in `comms/YYYY-MM-DD-tipo.md`
- Se aggiornare actions.md o decisions.md di conseguenza

---

## Struttura Email Standard

```
Oggetto: [Progetto] - [Argomento chiaro e specifico]

Ciao [Nome referente],

[1-2 frasi di contesto]

[Corpo del messaggio]

[Se servono azioni dal cliente:]
Ti chiedo di:
- [Azione 1] entro [data]
- [Azione 2] entro [data]

[Se serve decisione:]
Attendo conferma entro [data]. In assenza di risposta, procederò con [opzione default].

Resto a disposizione per chiarimenti.

A presto,
Luca
```

---

## Pattern per Tipo

### Richiesta Approvazione
- Oggetto: `[Progetto] - Approvazione [deliverable]`
- Corpo: cosa è stato consegnato, link, cosa include
- Chiusura: "Ti chiedo di revisionare e darmi feedback entro [data]. Se non ho osservazioni entro tale data, considererò [il deliverable] approvato."
- Menzionare silenzio-assenso se gate formale
- Menzionare CR per modifiche post-approvazione

### Segnalazione Problema
- Oggetto: `[Progetto] - [Problema] - Impatto su [cosa]`
- Struttura: **Situazione attuale** → **Impatto** → **Azioni in corso** → **Opzioni** (numerate, con pro/contro)
- Chiudere con richiesta di indicazione su come procedere
- Tono: trasparente, mai allarmista, sempre con soluzioni

### Sollecito
- **Primo sollecito** (3-5gg senza risposta): gentile, riformula richiesta
- **Secondo sollecito** (altri 3-5gg): avvisa che procederà con default
- **Escalation** (altri 5gg): coinvolgere sponsor/RUP in CC

### Scope / CR
- MAI dire "No, non è incluso"
- SEMPRE dire: "Possiamo farlo. Non era nel perimetro approvato, quindi devo valutarne l'impatto e proporti una Change Request. Ti mando la stima entro [data]."

### Escalation
- Oggetto: `[ESCALATION] [Progetto] - [Problema]`
- Struttura: **Problema** → **Impatto** → **Azioni già tentate** → **Opzioni proposte** → **Raccomandazione**
- Destinatario: livello superiore (sponsor/RUP), CC al referente

---

## Tono per Contesto

| Contesto | Tono |
|----------|------|
| **PA** | Formale, riferimenti normativi se rilevanti, attenzione ai ruoli (RUP, DEC) |
| **Privato PMI** | Diretto, informale, focus su risultati |
| **Privato Corporate** | Bilanciato, attenzione a catena decisionale |

## Regole Sempre Valide

- Oggetto email chiaro e specifico
- Azioni richieste in evidenza (elenco puntato)
- Sempre una data/scadenza se si chiede qualcosa
- Mai passivo-aggressivo
- Ammettere errori se nostri, con soluzioni
- Risposta attesa: sempre esplicitare
