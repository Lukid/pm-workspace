# Guida al Processo di Gestione Progetti

## 1. Panoramica

Questo documento descrive il processo standard per gestire progetti software in Net7, integrando:
- Metodologia **gate-based** per controllo formale
- Pratiche **agili** per l'esecuzione
- Conformità **ISO 9001:2015** senza burocrazia eccessiva

### Principio guida
> Il processo deve essere **tracciato** e **pensato**. Ogni fase lascia evidenze. Ogni decisione è documentata.

---

## 2. Ciclo di Vita del Progetto

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   AVVIO     │───▶│   ANALISI   │───▶│  SVILUPPO   │───▶│    TEST     │───▶│  CHIUSURA   │
│             │    │             │    │             │    │             │    │             │
│ - Kickoff   │    │ - Requisiti │    │ - Sprint    │    │ - UAT       │    │ - Go-live   │
│ - Brief     │    │ - Wireframe │    │ - Review    │    │ - Bug fix   │    │ - Collaudo  │
│ - Setup     │    │ - Mockup    │    │ - Deploy    │    │ - Signoff   │    │ - Handover  │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
                        │                   │                  │                   │
                       G1                  G2                 G3                  G4
                   (Wireframe)          (Mockup)            (UAT)            (Go-live)
```

---

## 3. I Gate di Approvazione

I gate sono **checkpoint formali**. Il progetto non procede senza approvazione scritta del cliente.

### G1 — Approvazione Wireframe/Scope

| Aspetto | Dettaglio |
|---------|-----------|
| **Cosa approva** | Perimetro funzionale, struttura, wireframe |
| **Deliverable** | Documento Scope + Wireframe (o prototipo navigabile) |
| **Chi approva** | Referente cliente |
| **SLA** | 5 gg lavorativi review, 3 gg approvazione |
| **Output** | Email/firma di approvazione G1 |

**Conseguenze approvazione G1:**
- Lo scope è congelato
- Ogni modifica successiva richiede Change Request
- Si può iniziare design UI

### G2 — Approvazione UI/Mockup

| Aspetto | Dettaglio |
|---------|-----------|
| **Cosa approva** | Design grafico, UI, look & feel |
| **Deliverable** | Mockup grafici (Figma/XD/immagini) |
| **Chi approva** | Referente cliente (+ stakeholder se necessario) |
| **SLA** | 5 gg lavorativi review, 3 gg approvazione |
| **Output** | Email/firma di approvazione G2 |

**Conseguenze approvazione G2:**
- La grafica è congelata
- Modifiche estetiche successive = Change Request
- Si può iniziare sviluppo

### G3 — UAT e Approvazione Staging

| Aspetto | Dettaglio |
|---------|-----------|
| **Cosa approva** | Funzionamento del sistema in ambiente di test |
| **Deliverable** | Ambiente staging + UAT checklist completata |
| **Chi approva** | Referente cliente (test effettuati) |
| **SLA** | 5 gg lavorativi UAT, 3 gg signoff |
| **Output** | Buglist con severity + Signoff UAT |

**Conseguenze approvazione G3:**
- Bug Blocker/Major devono essere risolti
- Bug Minor possono andare in backlog post go-live
- Si può pianificare go-live

### G4 — Go-Live e Accettazione

| Aspetto | Dettaglio |
|---------|-----------|
| **Cosa approva** | Sistema in produzione, chiusura progetto |
| **Deliverable** | Sistema live + smoke test passati |
| **Chi approva** | Referente cliente / RUP (per PA) |
| **SLA** | 3 gg smoke test, poi accettazione |
| **Output** | Verbale di collaudo / Accettazione finale |

**Conseguenze approvazione G4:**
- Progetto chiuso formalmente
- Inizia periodo garanzia
- Fattura finale emessa

---

## 4. Gestione dello Scope

### Principio fondamentale
> **Se non è scritto nel documento di scope approvato, non è incluso.**

### Classificazione richieste

| Tipo | Descrizione | Azione |
|------|-------------|--------|
| **In Scope** | Esplicitamente nel perimetro approvato | Si esegue |
| **Out of Scope** | Esplicitamente escluso | Rifiuto o CR |
| **Zona grigia** | Non menzionato | Valutazione → CR se significativo |
| **Bug** | Comportamento diverso da requisito | Si corregge (in garanzia) |
| **Enhancement** | Miglioramento oltre requisito | CR |

### Change Request (CR)

Ogni richiesta fuori scope segue questo processo:

```
┌─────────────────┐
│ Cliente chiede  │
│ qualcosa        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ È nel perimetro │──── Sì ───▶ Si esegue
│ approvato?      │
└────────┬────────┘
         │ No
         ▼
┌─────────────────┐
│ Aprire CR       │
│ - Descrizione   │
│ - Impatto €     │
│ - Impatto tempo │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Cliente approva │──── No ───▶ Non si fa
│ CR?             │
└────────┬────────┘
         │ Sì
         ▼
┌─────────────────┐
│ Si esegue       │
│ (tracciato)     │
└─────────────────┘
```

### Il "No" elegante

Quando il cliente chiede qualcosa fuori scope, non dire "No". Dì:

> *"Certamente, possiamo farlo. Poiché questa richiesta non è nel perimetro approvato (rif. documento X), devo aprire una Change Request per valutare l'impatto. Ti invio la stima entro domani; se approvi, la inseriamo nel piano."*

Questo approccio:
1. Mostra disponibilità
2. Crea barriera procedurale che filtra richieste futili
3. Usa il processo come autorità esterna

---

## 5. SAL — Stato Avanzamento Lavori

### Scopo
Il SAL documenta periodicamente:
- Cosa è stato fatto
- Cosa rimane da fare
- Problemi emersi
- Decisioni necessarie

### Frequenza
| Durata progetto | Frequenza SAL |
|-----------------|---------------|
| < 3 mesi | Settimanale |
| 3-6 mesi | Bisettimanale |
| > 6 mesi | Mensile |
| Sempre | A ogni milestone contrattuale |

### Contenuto minimo
1. **Periodo di riferimento**
2. **Riepilogo esecutivo** (3 righe max)
3. **Stato semaforo**: Scope 🟢🟡🔴 | Tempi 🟢🟡🔴 | Budget 🟢🟡🔴
4. **Attività completate** (lista)
5. **Attività in corso** (con % avanzamento)
6. **Criticità e rischi** (con mitigazione)
7. **Decisioni richieste al cliente** (con scadenza)
8. **Prossimi passi**
9. **Quadro economico** (se rilevante)

### Approvazione SAL
- Il cliente ha **5 giorni lavorativi** per osservazioni
- Silenzio = approvazione tacita
- SAL approvato sblocca fatturazione (se a milestone)

---

## 6. Gestione Rischi (RAID Log)

### Cosa tracciare

| Categoria | Descrizione |
|-----------|-------------|
| **R**ischi | Eventi potenziali negativi |
| **A**ssunzioni | Cose che assumiamo vere |
| **I**ssue | Problemi già verificatisi |
| **D**ipendenze | Elementi esterni da cui dipendiamo |

### Formato rischio

```markdown
### R-001: [Titolo breve]
- **Descrizione**: Cosa può succedere
- **Probabilità**: Alta / Media / Bassa
- **Impatto**: Alto / Medio / Basso
- **Mitigazione**: Cosa facciamo per prevenire
- **Contingency**: Cosa facciamo se succede
- **Owner**: Chi monitora
- **Stato**: Aperto / Mitigato / Chiuso / Verificato
```

### Quando aggiornare
- A ogni SAL
- Quando emerge nuovo rischio
- Quando un rischio cambia stato

---

## 7. Gestione Migrazione Contenuti

Se il progetto include migrazione da vecchio sistema:

### Policy A — Import + Freeze + Delta (Raccomandata)

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│ Import iniziale │───▶│ Freeze contenuti│───▶│ Import delta    │
│ (appena pronto) │    │ (X gg prima GL) │    │ (prima go-live) │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

- **Pro**: Pulito, controllabile, un solo momento critico
- **Contro**: Periodo di freeze può essere problematico

### Policy B — Import multipli programmati

- 2-3 sync concordate durante sviluppo
- Freeze solo prima del go-live
- **Pro**: Cliente può continuare a pubblicare
- **Contro**: Più costoso, più rischi di conflitto

### Policy C — Migrazione manuale

- Cliente ricopia contenuti
- Net7 supporta/verifica
- **Pro**: Zero effort migrazione
- **Contro**: Alto rischio errori, lento

### Checklist migrazione
- [ ] Policy concordata con cliente
- [ ] Chi aggiorna cosa durante freeze
- [ ] Quali contenuti esclusi
- [ ] Piano redirect URL (se web)
- [ ] Validazione post-migrazione

---

## 8. UAT — User Acceptance Test

### Obiettivo
Verificare che il sistema soddisfi i requisiti dal punto di vista dell'utente finale.

### Processo

1. **Preparazione** (Net7)
   - Deploy in staging
   - Test interni completati
   - UAT Plan + Checklist pronti

2. **Esecuzione** (Cliente)
   - Cliente testa seguendo checklist
   - Segnala bug con severity
   - Durata: max 5 gg lavorativi

3. **Triage** (Net7 + Cliente)
   - Review bug segnalati
   - Conferma severity
   - Piano risoluzione

4. **Fix** (Net7)
   - Risoluzione bug Blocker/Major
   - Re-test

5. **Signoff** (Cliente)
   - Conferma che UAT è superato
   - Bug Minor in backlog accettati

### Severity bug

| Severity | Criterio | Azione |
|----------|----------|--------|
| **Blocker** | Impedisce go-live | Fix immediato, blocca tutto |
| **Major** | Funzionalità core compromessa | Fix prima di go-live |
| **Minor** | Problema con workaround | Fix post go-live (garanzia) |
| **Cosmetic** | Solo estetico | Backlog, bassa priorità |

---

## 9. Go-Live

### Pre-requisiti
- [ ] UAT completato e signoff ricevuto
- [ ] Bug Blocker/Major risolti
- [ ] Piano go-live approvato
- [ ] Rollback plan pronto
- [ ] Smoke test checklist pronta
- [ ] Comunicazione a stakeholder

### Giorno del go-live

1. **Backup** stato attuale (se sostituzione)
2. **Deploy** in produzione
3. **Smoke test** (checklist rapida funzionalità critiche)
4. **Comunicazione** a cliente "siamo live"
5. **Monitoraggio** intensivo prime 24-48h

### Post go-live

- Periodo garanzia attivo
- Bug segnalati gestiti con SLA garanzia
- Evolutive = nuovo progetto/CR

---

## 10. Documentazione ISO 9001

### Evidenze minime richieste

| Fase | Evidenza |
|------|----------|
| Offerta | Offerta firmata / Ordine / Contratto |
| Requisiti | Documento requisiti approvato |
| Pianificazione | Milestone GitLab / Gantt |
| Test | Piano test + Report esecuzione |
| Collaudo | Verbale collaudo firmato |
| Modifiche | Change Request approvate |

### Dove si trovano

- **GitLab**: issue, milestone, commit, MR
- **Google Drive / OpenMemo**: documenti formali, offerte, contratti
- **projects/[nome]/**: documentazione operativa progetto

### Flusso gestione ticket

```
Backlog → Ready → Doing → Review → Staging/UAT → Done
```

- Ogni transizione lascia traccia (commento, label)
- Code review obbligatoria prima di merge
- Test prima di passare a Done

---

## 11. Rituali di Progetto

### Kickoff (inizio progetto)
- Partecipanti: PM + Team + Cliente
- Durata: 1-2h
- Output: Brief validato, prossimi passi chiari

### Weekly interno (se progetto attivo)
- Partecipanti: PM + Team
- Durata: 15-30 min
- Focus: blocchi, priorità settimana

### SAL meeting (a ogni SAL)
- Partecipanti: PM + Cliente
- Durata: 30-60 min
- Focus: review SAL, decisioni, prossimi passi

### Retrospettiva (fine progetto)
- Partecipanti: PM + Team
- Durata: 1h
- Focus: cosa ha funzionato, cosa migliorare

---

## 12. Escalation

### Quando escalare

| Situazione | Azione |
|------------|--------|
| Cliente non risponde da > 10 gg | Escalation a sponsor/RUP |
| Bug critico in produzione | Notifica immediata + war room |
| Rischio sforamento budget > 20% | Escalation interna + cliente |
| Conflitto con cliente | Coinvolgere responsabile Net7 |

### Come escalare

1. Documenta il problema (scritto)
2. Proponi soluzioni (non solo il problema)
3. Coinvolgi il livello appropriato
4. Traccia l'esito

---

*Questo documento è parte del Sistema Qualità Net7 — ISO 9001:2015*
