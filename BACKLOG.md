# Backlog Miglioramenti — PM Workspace

> Elenco dei miglioramenti futuri per il workspace. Da consultare in **Develop Mode**.

---

## Gap Critici (Priorità Alta)

### 1. Template Lessons Learned
**Problema**: La checklist di closure lo menziona ma non esiste un template dedicato.
**Impatto**: Requisito ISO 9001 (miglioramento continuo), perdita di conoscenza.

**Contenuto suggerito**:
- Cosa ha funzionato bene
- Cosa è andato storto
- Cause root dei problemi
- Azioni correttive per progetti futuri
- Feedback del team
- Feedback del cliente

**File da creare**: `templates/lessons-learned.md`

---

### 2. Template Garanzia/Post-Go-Live
**Problema**: Dopo G4 inizia la garanzia ma non c'è template per gestirla.
**Impatto**: Ambiguità su SLA, rischio di lavoro extra non pagato.

**Contenuto suggerito**:
- Durata garanzia (30/60/90 gg)
- SLA risposta e risoluzione per severity
- Canale di segnalazione (email? GitLab?)
- Criteri per distinguere bug vs enhancement
- Processo escalation in garanzia
- Cosa è coperto vs cosa è fatturabile

**File da creare**: `templates/warranty-plan.md`

---

### 3. Template Stima/Estimate
**Problema**: Le stime non sono strutturate, causa #1 di sforamenti.
**Impatto**: Budget errati, margini erosi.

**Contenuto suggerito**:
- Breakdown per componente/funzionalità
- Assunzioni di stima (esplicitate)
- Rischi e contingency %
- Confronto stima vs consuntivo (per calibrazione futura)
- Chi ha stimato e quando

**File da creare**: `templates/estimate.md`

---

### 4. Sezione Accessibilità WCAG
**Problema**: Per progetti PA è obbligatorio (CAD, AGID), non menzionato nei template.
**Impatto**: Bug di accessibilità possono essere bloccanti per legge.

**Azioni**:
- [ ] Aggiungere checklist WCAG 2.1 AA in `checklists/pre-uat.md`
- [ ] Aggiungere sezione "Requisiti di accessibilità" in `templates/project-brief.md`
- [ ] Creare `checklists/accessibility-checklist.md` (opzionale)

---

### 5. Sezione GDPR/Privacy
**Problema**: Per PA e privati è critico, nessun template lo copre.
**Impatto**: Rischio legale, mancata compliance.

**Azioni**:
- [ ] Aggiungere sezione in `templates/project-brief.md`:
  - Tipologia dati trattati
  - Titolare/Responsabile trattamento
  - Luogo hosting
  - Misure di sicurezza
  - Informativa privacy necessaria?

---

## Gap Secondari (Priorità Media)

### 6. Template Handover/Passaggio Consegne
**Quando serve**: Cambio PM mid-progetto, passaggio a manutenzione.

**Contenuto suggerito**:
- Stato attuale progetto
- Contatti chiave (interni ed esterni)
- Rischi aperti
- Decisioni pendenti
- Dove trovare cosa (documentazione, credenziali, repo)
- Prossimi passi critici

**File da creare**: `templates/handover.md`

---

### 7. Template Survey/Feedback Cliente
**Quando serve**: Post-progetto per misurare soddisfazione.
**Valore aggiunto**: Utile anche per ISO (customer satisfaction).

**Contenuto suggerito**:
- NPS (Net Promoter Score)
- Soddisfazione su: comunicazione, qualità, tempi, supporto
- Cosa ha funzionato bene
- Cosa potevamo fare meglio
- Referenza/testimonial

**File da creare**: `templates/client-feedback.md`

---

### 8. Gestione Multi-Progetto/Capacity
**Problema**: Luca gestisce più progetti contemporaneamente, manca vista d'insieme.

**Idee**:
- File `projects/_portfolio.md` con overview tutti i progetti attivi
- Template per allocazione risorse settimanale
- Sistema per segnalare conflitti di priorità

---

### 9. Template Proposta Evolutive
**Quando serve**: Alla chiusura progetto per proporre manutenzione/sviluppi futuri.

**Contenuto suggerito**:
- Riepilogo progetto concluso
- Proposte evolutive identificate durante il progetto
- Stima di massima
- Vantaggi per il cliente
- Modalità contrattuali (T&M, pacchetto ore, nuovo fixed price)

**File da creare**: `templates/proposal-evolutive.md`

---

### 10. Template Debito Tecnico
**Problema**: Le cose fatte "quick & dirty" non vengono tracciate.

**Contenuto suggerito**:
- Cosa è stato fatto in modo subottimale
- Perché (pressione tempi, budget, scope)
- Impatto se non sistemato
- Effort stimato per sistemare
- Priorità

**File da creare**: `templates/technical-debt.md` o sezione in `raid.md`

---

## Miglioramenti Minori (Nice to Have)

### 11. Più esempi
Attualmente c'è solo 1 esempio (PA). Aggiungere:
- [ ] Esempio brief progetto privato
- [ ] Esempio SAL
- [ ] Esempio CR compilata

### 12. Checklist sicurezza
Per progetti con dati sensibili:
- [ ] `checklists/security-checklist.md`

### 13. Template per kick-off meeting
Agenda strutturata per il primo incontro con il cliente.

---

## Come Usare Questo File

1. In **Develop Mode**, consulta questo backlog per decidere cosa implementare
2. Quando completi un item, spostalo in fondo con ✅ e data
3. Aggiungi nuovi item man mano che emergono

---

## Completati

*Nessun item completato ancora*

---

*Ultimo aggiornamento: Dicembre 2024*
