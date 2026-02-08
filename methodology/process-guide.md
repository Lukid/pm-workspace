# Guida al Processo di Gestione Progetti

Processo standard Net7: gate-based + pratiche agili + ISO 9001:2015 senza burocrazia eccessiva.

> Il processo deve essere **tracciato** e **pensato**. Ogni fase lascia evidenze. Ogni decisione è documentata.

---

## 1. Ciclo di Vita

```
AVVIO → ANALISI → SVILUPPO → TEST → CHIUSURA
         G1          G2          G3        G4
     (Wireframe)  (Mockup)    (UAT)   (Go-live)
```

I gate sono **checkpoint formali**. Il progetto non procede senza approvazione scritta del cliente. SLA e dettagli operativi dei gate sono nella skill `/gate`.

---

## 2. Gestione dello Scope

> **Se non è scritto nel documento di scope approvato, non è incluso.**

| Tipo | Azione |
|------|--------|
| **In Scope** | Si esegue |
| **Out of Scope** | Rifiuto o CR |
| **Zona grigia** | Valutazione → CR se significativo |
| **Bug** | Si corregge (in garanzia) |
| **Enhancement** | CR |

Ogni richiesta fuori scope → Change Request (vedi skill `/cr`).

---

## 3. SAL — Frequenza

| Durata progetto | Frequenza |
|-----------------|-----------|
| < 3 mesi | Settimanale |
| 3-6 mesi | Bisettimanale |
| > 6 mesi | Mensile |
| Sempre | A ogni milestone contrattuale |

Dettagli e template SAL nella skill `/sal`.

---

## 4. RAID Log

| Categoria | Descrizione |
|-----------|-------------|
| **R**ischi | Eventi potenziali negativi |
| **A**ssunzioni | Cose che assumiamo vere |
| **I**ssue | Problemi già verificatisi |
| **D**ipendenze | Elementi esterni da cui dipendiamo |

Aggiornare a ogni SAL, quando emerge nuovo rischio, quando un rischio cambia stato.

---

## 5. Gestione Migrazione

| Policy | Quando | Pro | Contro |
|--------|--------|-----|--------|
| **A) Import + Freeze + Delta** (default) | Standard | Pulito, controllabile | Periodo freeze |
| **B) Import multipli** | Cliente pubblica molto | Continuità | Più costoso |
| **C) Migrazione manuale** | Siti piccoli | Zero effort | Alto rischio errori |

Checklist: policy concordata, chi aggiorna cosa, contenuti esclusi, piano redirect, validazione.

---

## 6. UAT

1. **Preparazione** (Net7): deploy staging, test interni, UAT plan
2. **Esecuzione** (Cliente): test da checklist, segnalazione bug, max 5gg
3. **Triage** (insieme): review bug, conferma severity
4. **Fix** (Net7): Blocker/Major risolti, re-test
5. **Signoff** (Cliente): UAT superato, Minor in backlog accettati

---

## 7. Go-Live

### Pre-requisiti
- UAT + signoff, bug critici risolti, piano go-live, rollback plan, comunicazione stakeholder

### Giorno del go-live
1. Backup → Deploy produzione → Smoke test → Comunicazione → Monitoraggio 24-48h

### Post go-live
- Garanzia attiva, bug gestiti con SLA, evolutive = nuovo progetto/CR

---

## 8. Documentazione ISO 9001

| Fase | Evidenza |
|------|----------|
| Offerta | Contratto firmato |
| Requisiti | Documento approvato |
| Pianificazione | Milestone GitLab |
| Test | Piano + Report |
| Collaudo | Verbale firmato |
| Modifiche | CR approvate |

---

## 9. Rituali di Progetto

| Rituale | Quando | Durata |
|---------|--------|--------|
| Kickoff | Inizio progetto | 1-2h |
| Weekly interno | Settimanale (se attivo) | 15-30 min |
| SAL meeting | A ogni SAL | 30-60 min |
| Retrospettiva | Fine progetto | 1h |

---

## 10. Escalation

| Situazione | Azione |
|------------|--------|
| Cliente non risponde > 10 gg | Escalation a sponsor/RUP |
| Bug critico in produzione | Notifica immediata + war room |
| Rischio sforamento > 20% | Escalation interna + cliente |
| Conflitto con cliente | Coinvolgere responsabile Net7 |

Come: documenta → proponi soluzioni → coinvolgi livello appropriato → traccia esito.

---

*Documento parte del Sistema Qualità Net7 — ISO 9001:2015*
