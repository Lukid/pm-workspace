---
name: gate
description: Genera documento di Gate (G1/G2/G3/G4) con wizard interattivo
arguments:
  - name: tipo
    description: "Tipo gate: G1, G2, G3, G4"
    required: false
  - name: progetto
    description: Nome del progetto
    required: false
---

# Skill: Genera Documento Gate

Genera un documento di approvazione Gate con wizard interattivo.

## Istruzioni

### 1. Identifica il progetto

Se `$ARGUMENTS` contiene un nome progetto, usa quello.
Altrimenti:
- Controlla se la directory corrente è sotto `projects/`
- Se sì, usa quel progetto
- Se no, chiedi all'utente

Carica `.project-context.md` per ottenere:
- Nome progetto, cliente, CIG/CUP
- Stato gate precedenti
- Tipo cliente (PA/Privato)

### 2. Determina il tipo di gate

Se `$ARGUMENTS` contiene G1/G2/G3/G4, usa quello.
Altrimenti chiedi:

> **Quale gate vuoi generare?**
> 1. G1 — Wireframe e Scope
> 2. G2 — Mockup e Design UI
> 3. G3 — UAT e Staging
> 4. G4 — Go-live e Chiusura

### 3. Verifica prerequisiti

- **G2** richiede G1 approvato
- **G3** richiede G2 approvato
- **G4** richiede G3 approvato

Se il gate precedente non è approvato, avvisa e chiedi se procedere comunque.

### 4. Wizard domande per tipo

#### G1 — Wireframe e Scope
1. "Link ai wireframe (Figma/Miro)?"
2. "Le funzionalità incluse sono già documentate? Se sì, dove?"
3. "Ci sono esclusioni esplicite da evidenziare?"
4. "Data prevista per feedback cliente?"

#### G2 — Mockup e Design UI
1. "Link Figma ai mockup completi?"
2. "Link al prototipo navigabile (se presente)?"
3. "Elenco pagine principali da includere nella tabella?"
4. "Link all'UI kit / Design System (se separato)?"
5. "Data consegna ufficiale?"

#### G3 — UAT e Staging
1. "URL ambiente staging?"
2. "Periodo UAT (date inizio-fine)?"
3. "Riepilogo bug: quanti Blocker/Major/Minor risolti?"
4. "Ci sono bug Minor accettati per post go-live?"
5. "Tutte le funzionalità core sono verificate?"

#### G4 — Go-live e Chiusura
1. "URL produzione?"
2. "Versione rilasciata?"
3. "Data effettiva go-live?"
4. "Smoke test superato? Eventuali note?"
5. "Periodo garanzia (mesi)?"
6. "Anomalie residue o funzionalità rinviate?"

### 5. Genera il documento

Usa la struttura del gate corrispondente (vedi template sotto).

**Per progetti PA**, aggiungi sezione conformità:

| Normativa/Linea guida | Stato | Note |
| :---- | :---- | :---- |
| **Linee Guida Design PA** (AgID) | ✓ Conforme | [note] |
| **WCAG 2.1 Livello AA** | ✓ Previsto | Verifiche accessibilità in fase sviluppo |
| **Legge 4/2004** (Legge Stanca) | ✓ Previsto | Dichiarazione accessibilità post go-live |
| **GDPR** | ✓ Conforme | Privacy by design applicata |

### 6. Calcola date SLA

- **Review**: +5 giorni lavorativi dalla data consegna
- **Approvazione**: +3 giorni lavorativi dalla scadenza review
- Escludi weekend dal calcolo.

### 7. Salva il documento

Salva in: `projects/[nome]/gates/G[N]-[tipo].md`
- G1 → `wireframe`, G2 → `mockup`, G3 → `uat`, G4 → `golive`

### 8. Aggiorna project-context

Suggerisci di aggiornare `.project-context.md` con lo stato del gate.

### 9. Output finale

```
Gate G[N] generato: gates/G[N]-[tipo].md

Riepilogo:
- Progetto: [nome]
- Cliente: [cliente]
- Data consegna: [data]
- Scadenza review: [data] (5gg lavorativi)
- Scadenza approvazione: [data] (silenzio-assenso)

Prossimi passi:
1. Revisiona il documento
2. Invia al cliente (usa /email per la bozza)
3. Segna in calendario le scadenze SLA
```

---

## Struttura Gate G1 — Wireframe e Scope

```markdown
# GATE G1 — Approvazione Wireframe e Scope

---

**Progetto**: [Nome]
**Cliente**: [Cliente]
**Fornitore**: Net7 S.r.l.
**CIG/CUP**: [Codice]
**Data consegna**: [YYYY-MM-DD]

---

## 1. Oggetto

Con il presente documento si sottopone all'approvazione del Cliente il **perimetro funzionale e la struttura** di [deliverable]. Il superamento del Gate G1 è requisito propedeutico all'avvio della fase di design UI.

## 2. Deliverable consegnati

### Perimetro funzionale
- Documento scope: [Link]

### Architettura dell'informazione
- Sitemap: [Link]

### Wireframe
| Wireframe | Link |
| :---- | :---- |
| Homepage | ✓ [Figma](link) |
| [Pagina] | ✓ [Figma](link) |

## 3. Perimetro funzionale

### Incluso
| ID | Funzionalità | Priorità |
| :---- | :---- | :---- |
| F01 | [Nome] | Must |
| F02 | [Nome] | Should |

### Escluso
| ID | Elemento | Motivo |
| :---- | :---- | :---- |
| X01 | [Nome] | [Motivo] |

> Richieste sugli elementi esclusi richiedono **Change Request** formale.

<!-- SEZIONE PA: solo per progetti PA -->
## 4. Conformità normativa
[Tabella conformità — vedi sopra]
<!-- FINE SEZIONE PA -->

## 5. Criteri di accettazione
- [ ] Perimetro funzionale (incluso ed escluso)
- [ ] Architettura dell'informazione e sitemap
- [ ] Wireframe e flussi utente principali

## 6. Modalità di approvazione

| Fase | Durata | Scadenza |
| :---- | :---- | :---- |
| Review | 5gg lavorativi | [Data] |
| Approvazione | 3gg lavorativi | [Data] |

Silenzio-assenso dopo le scadenze indicate.
Modifiche post-approvazione = **Change Request**.

## 7. Impatto dell'approvazione
1. Avvio design UI/mockup
2. Congelamento scope funzionale
3. Pianificazione milestone successive

## 8. Approvazione formale

| Ruolo | Nome | Data | Firma |
| :---- | :---- | :---- | :---- |
| PM Fornitore | [Nome] | [Data] | |
| Referente Cliente | [Nome] | | |

---

*Sistema Qualità Net7 — ISO 9001:2015*
```

## Struttura Gate G2 — Mockup e Design UI

```markdown
# GATE G2 — Consegna e Approvazione Design UI/UX

---

**Progetto**: [Nome]
**Cliente**: [Cliente]
**Fornitore**: Net7 S.r.l.
**CIG/CUP**: [Codice]
**Data consegna**: [YYYY-MM-DD]

---

## 1. Oggetto

Si sottopone all'approvazione del Cliente la **proposta grafica e di User Experience**. Il superamento del Gate G2 è requisito propedeutico all'avvio dello sviluppo.

## 2. Deliverable consegnati

### Pagine e percorsi utente
- Vista complessiva: [Link Figma]
- Prototipo navigabile: [Link]

| Pagina | Link |
| :---- | :---- |
| Homepage | ✓ [Figma](link) |
| [Pagina] | ✓ [Figma](link) |

### Design System e UI Kit
| Elemento | Riferimento |
| :---- | :---- |
| Palette colori | [Figma](link) |
| Tipografia | [Figma](link) |
| Componenti UI | [Figma](link) |

<!-- SEZIONE PA -->
## 3. Conformità normativa
[Tabella conformità]
<!-- FINE SEZIONE PA -->

## 4. Criteri di accettazione
- [ ] Pagine e sezioni principali e percorsi utente
- [ ] Design system e UI kit
- [ ] Architettura dell'informazione

## 5. Modalità di approvazione

| Fase | Durata | Scadenza |
| :---- | :---- | :---- |
| Review | 5gg lavorativi | [Data] |
| Approvazione | 3gg lavorativi | [Data] |

Silenzio-assenso dopo le scadenze. Modifiche post-approvazione = **Change Request**.

## 6. Impatto dell'approvazione
1. Avvio sviluppo
2. Setup ambienti
3. Congelamento baseline grafica

## 7. Approvazione formale

| Ruolo | Nome | Data | Firma |
| :---- | :---- | :---- | :---- |
| PM Fornitore | [Nome] | [Data] | |
| Referente Cliente | [Nome] | | |

---

*Sistema Qualità Net7 — ISO 9001:2015*
```

## Struttura Gate G3 — UAT

```markdown
# Gate G3 — UAT e Approvazione Staging

---

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome] |
| **Cliente** | [Cliente] |
| **Data** | [YYYY-MM-DD] |
| **Ambiente staging** | [URL] |
| **Periodo UAT** | [Inizio] - [Fine] |

---

## 1. Scopo
Certifica: completamento UAT, stato bug, approvazione per go-live.

## 2. Riepilogo UAT

| Categoria | Totale | Superati | Falliti |
|-----------|--------|----------|---------|
| Funzionalità core | [N] | [N] | [N] |
| Form e validazioni | [N] | [N] | [N] |
| Responsive | [N] | [N] | [N] |
| Accessibilità | [N] | [N] | [N] |
| **TOTALE** | **[N]** | **[N]** | **[N]** |

Tasso di successo: **[XX]%**

## 3. Riepilogo Bug

| Severity | Trovati | Risolti | Aperti |
|----------|---------|---------|--------|
| Blocker | [N] | [N] | [N] |
| Major | [N] | [N] | [N] |
| Minor | [N] | [N] | [N] |
| Cosmetic | [N] | [N] | [N] |

### Bug Minor/Cosmetic accettati per post go-live
| ID | Descrizione | Piano risoluzione |
|----|-------------|-------------------|
| [ID] | [Desc] | Garanzia - entro [data] |

## 4. Funzionalità Verificate
- [x] [Funzionalità 1] — OK
- [x] [Funzionalità 2] — OK
- [ ] [Funzionalità 3] — Post go-live (concordato)

## 5. Condizioni per Go-Live
- [x] Tutti i bug Blocker risolti
- [x] Tutti i bug Major risolti
- [x] Funzionalità core verificate
- [ ] Contenuti definitivi inseriti
- [ ] Redirect configurati

## 6. Esito UAT
- [ ] **SUPERATO** — Pronto per go-live
- [ ] **SUPERATO CON RISERVA** — Con condizioni in sez. 5
- [ ] **NON SUPERATO** — Correzioni necessarie

## 7. Approvazione Gate G3

| Ruolo | Nome | Data |
|-------|------|------|
| Referente Cliente | [Nome] | |
| PM Net7 | [Nome] | |

---

*Sistema Qualità Net7 — ISO 9001:2015*
```

## Struttura Gate G4 — Go-live

```markdown
# Gate G4 — Go-Live e Accettazione Finale

---

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome] |
| **Cliente** | [Cliente] |
| **Data go-live** | [YYYY-MM-DD] |
| **Data verbale** | [YYYY-MM-DD] |

---

## 1. Riepilogo Progetto

| Aspetto | Previsto | Effettivo | Scostamento |
|---------|----------|-----------|-------------|
| Data avvio | [Data] | [Data] | [+/- N gg] |
| Data go-live | [Data] | [Data] | [+/- N gg] |
| Budget | €[X] | €[X] | [+/- €X] |

## 2. Gate Superati

| Gate | Data approvazione |
|------|-------------------|
| G1 Wireframe | [Data] |
| G2 Mockup | [Data] |
| G3 UAT | [Data] |
| G4 Go-live | [Data odierna] |

## 3. Ambiente di Produzione

| Aspetto | Dettaglio |
|---------|-----------|
| URL | [https://...] |
| Versione | [vX.X.X] |
| Backup | Sì/No |
| Monitoraggio | Sì/No |

## 4. Smoke Test

| Test | Esito |
|------|-------|
| Sistema raggiungibile | ✅ |
| Login funzionante | ✅ |
| Pagine principali | ✅ |
| Form principali | ✅ |
| [Test specifico] | ✅ |

**SMOKE TEST SUPERATO**

## 5. Riepilogo Economico

| Voce | Importo |
|------|---------|
| Valore contrattuale | €[X] |
| CR approvate | €[X] |
| **Totale** | **€[X]** |
| Già fatturato | €[X] |
| **Saldo finale** | **€[X]** |

## 6. Anomalie Residue

### Bug minori accettati
| ID | Descrizione | Piano |
|----|-------------|-------|
| [ID] | [Desc] | Garanzia - [data] |

### Funzionalità rinviate
| Funzionalità | Pianificazione |
|--------------|----------------|
| [Nome] | Fase 2 / Backlog |

## 7. Garanzia e Supporto

| Aspetto | Dettaglio |
|---------|-----------|
| Periodo | [N] mesi |
| Inizio | [Data] |
| Fine | [Data] |
| Canale | [Email/Ticket] |
| SLA risposta | [Es: 8h per Blocker] |

**Coperto**: bug fix su funzionalità rilasciate
**Non coperto**: nuove funzionalità, modifiche, problemi di hosting

## 8. Dichiarazione di Chiusura

Il progetto è formalmente concluso. Tutti i deliverable consegnati e accettati. Periodo di garanzia attivo.

## Approvazione Gate G4

| Ruolo | Nome | Data |
|-------|------|------|
| Sponsor/RUP Cliente | [Nome] | |
| PM Net7 | [Nome] | |

---

*Sistema Qualità Net7 — ISO 9001:2015*
```
