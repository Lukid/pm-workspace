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

Genera un documento SAL completo e self-contained.

## Istruzioni

### 1. Identifica il progetto

Se `$ARGUMENTS` contiene un nome progetto, usa quello.
Altrimenti:
- Controlla se la directory corrente è sotto `projects/`
- Se sì, usa quel progetto
- Se no, chiedi all'utente quale progetto

### 2. Carica il contesto

Leggi in parallelo dalla directory del progetto:
- `.project-context.md` — metadata (nome, cliente, budget, stato gate)
- `actions.md` — azioni in corso e completate
- `raid.md` — rischi, assunzioni, issue, dipendenze
- `decisions.md` — decisioni prese e pendenti
- `changes/` — eventuali CR attive

### 3. Determina il periodo

Se specificato in `$ARGUMENTS`, usa quel periodo.
Altrimenti usa le ultime 2 settimane dalla data odierna.

### 4. Calcola numero SAL

Conta i file esistenti in `sal/` per determinare il numero progressivo.

### 5. Genera il SAL

Compila il template sotto con i dati reali del progetto.

**Regole per il riepilogo esecutivo:**
- Max 3 frasi, tono professionale ma chiaro
- Evidenzia subito se ci sono criticità
- Stile: "Il progetto procede in linea con la pianificazione..." oppure "Si segnala un ritardo di X giorni su..."

**Regole semaforo:**

| Indicatore | 🟢 Verde | 🟡 Giallo | 🔴 Rosso |
|-----------|----------|-----------|----------|
| **Ambito** | Scope stabile, nessuna CR pendente | CR pendenti o scope in discussione | Multiple CR non approvate, scope fuori controllo |
| **Tempi** | In linea con go-live, nessuna azione scaduta | Ritardo < 1 settimana o azioni scadute < 3 | Ritardo > 1 settimana o azioni scadute >= 3 |
| **Budget** | Nessuna CR che impatta budget | CR approvate < 10% budget | CR approvate >= 10% budget |

### 6. Salva il documento

Salva in: `projects/[nome]/sal/SAL-[YYYY-MM-DD].md`

### 7. Output finale

Conferma con riepilogo:
```
SAL generato: sal/SAL-[data].md

Riepilogo:
- Periodo: [periodo]
- Semaforo: Ambito [emoji] | Tempi [emoji] | Budget [emoji]
- Attività completate: [N]
- Rischi attivi: [N]
- Decisioni pendenti: [N]
```

---

## Template SAL

```markdown
# SAL — Stato Avanzamento Lavori

---

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Cliente** | [Nome cliente] |
| **Periodo** | [Data inizio] - [Data fine] |
| **SAL n.** | [Numero progressivo] |
| **Redatto da** | [Nome PM] |
| **Data** | [YYYY-MM-DD] |

---

## 1. Riepilogo Esecutivo

[2-3 frasi: stato generale, criticità, risultati principali del periodo]

---

## 2. Stato Generale

| Ambito | Tempi | Budget |
|--------|-------|--------|
| 🟢/🟡/🔴 | 🟢/🟡/🔴 | 🟢/🟡/🔴 |

**Legenda**: 🟢 In linea | 🟡 A rischio | 🔴 Critico

---

## 3. Attività Completate

| Attività / Deliverable | Data | Note |
|------------------------|------|------|
| [Attività 1] | [Data] | ✅ |

---

## 4. Attività in Corso

| Attività | Avanzamento | Scadenza prevista |
|----------|-------------|-------------------|
| [Attività 1] | [XX]% | [Data] |

---

## 5. Milestone

| Milestone | Data prevista | Stato |
|-----------|---------------|-------|
| G1 Wireframe | [Data] | ✅/🔄/⏳ |
| G2 Mockup | [Data] | ✅/🔄/⏳ |
| G3 UAT | [Data] | ✅/🔄/⏳ |
| G4 Go-live | [Data] | ✅/🔄/⏳ |

---

## 6. Criticità e Rischi

| Criticità / Rischio | Impatto | Azione |
|---------------------|---------|--------|
| [Descrizione] | Alto/Medio | [Mitigazione] |

---

## 7. Decisioni Richieste

| Decisione | Entro il | Priorità | Conseguenza se non deciso |
|-----------|----------|----------|---------------------------|
| [Tema] | [Data] | Alta/Media | [Impatto] |

> **Nota**: In assenza di risposta entro la scadenza, Net7 procederà con l'opzione di default o sospenderà le attività dipendenti.

---

## 8. Change Request

| CR ID | Descrizione | Stato | Impatto |
|-------|-------------|-------|---------|
| CR-XXX | [Descrizione] | Approvata/Pendente | €[X] |

---

## 9. Prossimi Passi

| Attività | Responsabile | Scadenza |
|----------|--------------|----------|
| [Attività 1] | [Chi] | [Data] |

---

## 10. Quadro Economico

| Voce | Importo |
|------|---------|
| Valore contratto | €[importo] |
| SAL precedenti | €[importo] |
| Presente SAL | €[importo] |
| CR approvate | €[importo] |
| **Totale fatturato** | **€[importo]** |
| **Residuo** | **€[importo]** |

---

## Approvazione SAL

Il presente SAL si considera approvato se non pervengono osservazioni scritte entro **5 giorni lavorativi** dalla ricezione.

| Ruolo | Firma | Data |
|-------|-------|------|
| PM Net7 | | |
| Referente Cliente | | |

---

*Documento generato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
```
