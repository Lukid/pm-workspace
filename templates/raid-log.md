# RAID Log

> Rischi, Assunzioni, Issue, Dipendenze

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Ultimo aggiornamento** | [GG/MM/AAAA] |
| **Owner** | [PM] |

---

## Riepilogo

| Categoria | Aperti | Chiusi | Totale |
|-----------|--------|--------|--------|
| Rischi | | | |
| Assunzioni | | | |
| Issue | | | |
| Dipendenze | | | |

---

## Rischi (R)

| ID | Rischio | Prob. | Impatto | Livello | Mitigazione | Owner | Stato |
|----|---------|-------|---------|---------|-------------|-------|-------|
| R-001 | [Descrizione] | A/M/B | A/M/B | 🔴/🟡/🟢 | [Azione] | [Chi] | Aperto |
| R-002 | [Descrizione] | A/M/B | A/M/B | 🔴/🟡/🟢 | [Azione] | [Chi] | Mitigato |

### Legenda Livello
- 🔴 Alto (prob. alta + impatto alto)
- 🟡 Medio 
- 🟢 Basso

### Stati Rischio
- **Aperto**: rischio attivo, da monitorare
- **Mitigato**: azioni in corso, rischio ridotto
- **Chiuso**: rischio non più rilevante
- **Verificato**: il rischio si è concretizzato → diventa Issue

---

## Assunzioni (A)

| ID | Assunzione | Validata | Impatto se falsa | Owner | Stato |
|----|------------|----------|------------------|-------|-------|
| A-001 | [Cosa assumiamo vero] | Sì/No/Parziale | [Conseguenze] | [Chi] | Valida |
| A-002 | [Cosa assumiamo vero] | Sì/No/Parziale | [Conseguenze] | [Chi] | Da verificare |

### Stati Assunzione
- **Da verificare**: non ancora confermata
- **Valida**: confermata vera
- **Invalida**: risultata falsa → azioni correttive necessarie

---

## Issue (I)

| ID | Issue | Impatto | Azione | Owner | Scadenza | Stato |
|----|-------|---------|--------|-------|----------|-------|
| I-001 | [Problema verificatosi] | A/M/B | [Cosa fare] | [Chi] | [Data] | Aperta |
| I-002 | [Problema verificatosi] | A/M/B | [Cosa fare] | [Chi] | [Data] | Risolta |

### Stati Issue
- **Aperta**: problema attivo
- **In corso**: azioni in esecuzione
- **Risolta**: problema risolto
- **Escalata**: richiede intervento superiore

---

## Dipendenze (D)

| ID | Dipendenza | Da chi/cosa | Impatto | Data necessaria | Stato |
|----|------------|-------------|---------|-----------------|-------|
| D-001 | [Di cosa abbiamo bisogno] | [Fonte] | [Se manca] | [Quando serve] | In attesa |
| D-002 | [Di cosa abbiamo bisogno] | [Fonte] | [Se manca] | [Quando serve] | Ricevuta |

### Stati Dipendenza
- **In attesa**: non ancora ricevuta
- **Sollecitata**: richiesta inviata, attesa risposta
- **Ricevuta**: dipendenza soddisfatta
- **Bloccata**: problema nell'ottenimento

---

## Storico Aggiornamenti

| Data | Aggiornamento |
|------|---------------|
| [Data] | [Cosa è cambiato] |
| [Data] | [Cosa è cambiato] |

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
