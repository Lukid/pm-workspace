# Project Brief

> Template per l'avvio di un nuovo progetto

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Cliente** | [Nome cliente] |
| **Tipo** | [ ] PA  [ ] Privato |
| **Contratto** | [ ] Fixed Price  [ ] T&M |
| **Versione** | 1.0 |
| **Data** | [GG/MM/AAAA] |
| **Owner** | [Nome PM] |
| **Stato** | [ ] Bozza  [ ] In revisione  [ ] Approvato |

---

## 1. Executive Summary

[2-3 frasi che riassumono il progetto: cosa, per chi, perché, quando]

---

## 2. Contesto e Obiettivi

### 2.1 Contesto
[Descrizione del contesto: chi è il cliente, perché nasce questo progetto, quale problema risolve]

### 2.2 Obiettivi di business
1. [Obiettivo 1 - es: Aumentare l'engagement degli utenti del 20%]
2. [Obiettivo 2]
3. [Obiettivo 3]

### 2.3 Criteri di successo
Il progetto sarà considerato un successo se:
- [ ] [Criterio misurabile 1]
- [ ] [Criterio misurabile 2]
- [ ] [Criterio misurabile 3]

---

## 3. Scope

### 3.1 In Scope ✅

#### Funzionalità
- [Funzionalità 1]
- [Funzionalità 2]
- [Funzionalità 3]

#### Deliverable
- [Deliverable 1 - es: Sito web responsive]
- [Deliverable 2 - es: Documentazione tecnica]
- [Deliverable 3 - es: Formazione utenti]

### 3.2 Out of Scope ❌
- [Esplicitamente escluso 1 - es: App mobile nativa]
- [Esplicitamente escluso 2 - es: Migrazione dati pre-2020]
- [Esplicitamente escluso 3 - es: Integrazioni con sistemi terzi non specificati]

### 3.3 Assunzioni
- [Assunzione 1 - es: Il cliente fornirà contenuti entro le date concordate]
- [Assunzione 2 - es: L'hosting è già disponibile e configurato]
- [Assunzione 3]

### 3.4 Vincoli
- [Vincolo 1 - es: Go-live obbligatorio entro 31/03/2025]
- [Vincolo 2 - es: Budget massimo €XX.XXX]
- [Vincolo 3 - es: Conformità WCAG 2.1 AA]

---

## 4. Timeline e Milestone

### 4.1 Date chiave

| Milestone | Data prevista | Gate |
|-----------|---------------|------|
| Kickoff | [Data] | - |
| Approvazione Wireframe/Scope | [Data] | G1 |
| Approvazione Mockup | [Data] | G2 |
| Inizio UAT | [Data] | - |
| Approvazione UAT | [Data] | G3 |
| Go-live | [Data] | G4 |
| Fine garanzia | [Data] | - |

### 4.2 Dipendenze esterne
- [Dipendenza 1 - es: API del sistema XYZ disponibili entro [data]]
- [Dipendenza 2 - es: Contenuti forniti dal cliente entro [data]]

---

## 5. Team e Responsabilità

### 5.1 Team Net7

| Ruolo | Nome | Responsabilità |
|-------|------|----------------|
| Project Manager | [Nome] | Gestione progetto, comunicazione cliente |
| Tech Lead | [Nome] | Architettura, decisioni tecniche |
| Developer | [Nome] | Sviluppo backend/frontend |
| Designer | [Nome] | UX/UI design |
| Content | [Nome] | Contenuti e copy |

### 5.2 Team Cliente

| Ruolo | Nome | Email | Responsabilità |
|-------|------|-------|----------------|
| Sponsor / RUP | [Nome] | [email] | Approvazioni, escalation |
| Referente operativo | [Nome] | [email] | Feedback, test, contenuti |
| Referente tecnico | [Nome] | [email] | Integrazioni, infrastruttura |

---

## 6. Budget

| Voce | Importo |
|------|---------|
| Totale contratto | € [importo] |
| Contingency (se prevista) | € [importo] |
| **Totale** | **€ [importo]** |

### 6.1 Piano di fatturazione

| Milestone | % | Importo | Condizione |
|-----------|---|---------|------------|
| Avvio / Firma | [X]% | € [importo] | Firma contratto |
| SAL 1 - [Descrizione] | [X]% | € [importo] | Approvazione G1 |
| SAL 2 - [Descrizione] | [X]% | € [importo] | Approvazione G2 |
| SAL 3 - [Descrizione] | [X]% | € [importo] | Approvazione G3 |
| Saldo | [X]% | € [importo] | Go-live / G4 |

---

## 7. Rischi Iniziali

| ID | Rischio | Prob. | Impatto | Mitigazione |
|----|---------|-------|---------|-------------|
| R1 | [Descrizione] | A/M/B | A/M/B | [Azione] |
| R2 | [Descrizione] | A/M/B | A/M/B | [Azione] |
| R3 | [Descrizione] | A/M/B | A/M/B | [Azione] |

---

## 8. Comunicazione e Governance

### 8.1 Canali
- **Email**: [email PM] (comunicazioni formali)
- **Call/Meet**: [frequenza - es: settimanale il martedì h.10]
- **GitLab**: [URL repository] (tracking tecnico)

### 8.2 Reportistica
- **SAL**: [Frequenza - es: Quindicinale / Mensile]
- **Formato**: Documento + call di presentazione

### 8.3 SLA Feedback Cliente
| Tipo | Tempo review | Tempo approvazione | Silenzio-assenso |
|------|--------------|--------------------|--------------------|
| Wireframe/Scope | 5 gg lav. | 3 gg lav. | Sì |
| Mockup | 5 gg lav. | 3 gg lav. | Sì |
| SAL | 5 gg lav. | - | Sì |
| UAT | 5 gg lav. | 3 gg lav. | Sì |
| Change Request | 5 gg lav. | 3 gg lav. | No |

### 8.4 Gestione Modifiche
Ogni richiesta non presente nel perimetro approvato richiede Change Request formale.
Il processo è descritto nel documento di governance allegato.

---

## 9. Migrazione (se applicabile)

### 9.1 Policy scelta
- [ ] **A) Import + Freeze + Delta** (consigliata)
- [ ] **B) Import multipli programmati**
- [ ] **C) Migrazione manuale**

### 9.2 Dettagli
- **Fonte dati**: [Sistema/sito attuale]
- **Cosa migrare**: [Contenuti, utenti, ecc.]
- **Cosa NON migrare**: [Esclusi]
- **Periodo freeze**: [Da - A]
- **Responsabile contenuti durante freeze**: [Nome]
- **Validazione redirect**: [ ] Sì  [ ] No  [ ] N/A

---

## 10. Tecnologie (se rilevante)

| Area | Tecnologia |
|------|------------|
| CMS | [es: WordPress] |
| Frontend | [es: React, Tailwind] |
| Backend | [es: PHP, Laravel] |
| Hosting | [es: AWS, Regione Toscana] |
| Altro | [es: SPID, PagoPA] |

---

## 11. Prossimi Passi

| Azione | Responsabile | Scadenza |
|--------|--------------|----------|
| Kickoff meeting | PM | [Data] |
| Setup repository GitLab | Tech Lead | [Data] |
| Prima bozza wireframe | Designer | [Data] |
| [Altra azione] | [Chi] | [Data] |

---

## 12. Allegati

- [ ] Offerta / Contratto
- [ ] Progetto esecutivo (se disponibile)
- [ ] Specifiche tecniche
- [ ] Wireframe / Mockup iniziali
- [ ] Altro: [specificare]

---

## Approvazione

| Ruolo | Nome | Firma/Email | Data |
|-------|------|-------------|------|
| PM Net7 | | | |
| Responsabile Net7 | | | |
| Referente Cliente | | | |

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
