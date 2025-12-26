# Gate G3 — UAT e Approvazione Staging

> Documento di approvazione dei test utente e del sistema in ambiente di staging

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Cliente** | [Nome cliente] |
| **Versione** | 1.0 |
| **Data** | [GG/MM/AAAA] |
| **Redatto da** | [Nome PM] |
| **Ambiente staging** | [URL] |
| **Periodo UAT** | [Data inizio] - [Data fine] |
| **Scadenza signoff** | [Data - 3gg dopo fine UAT] |

---

## 1. Scopo del Documento

Questo documento certifica:
1. **Completamento UAT** (User Acceptance Test)
2. **Stato dei bug** riscontrati e risolti
3. **Approvazione per go-live**

L'approvazione di questo documento costituisce il **Gate G3** e autorizza la pianificazione del go-live.

---

## 2. Riferimenti

| Documento | Versione | Data |
|-----------|----------|------|
| Gate G1 - Wireframe e Scope | [X.X] | [Data] |
| Gate G2 - Mockup | [X.X] | [Data] |
| UAT Plan | [X.X] | [Data] |

---

## 3. Ambiente di Test

| Aspetto | Dettaglio |
|---------|-----------|
| URL Staging | [https://...] |
| Credenziali test | [Fornite separatamente] |
| Versione deployata | [vX.X.X] |
| Data ultimo deploy | [GG/MM/AAAA] |

---

## 4. Riepilogo UAT

### 4.1 Test eseguiti

| Categoria | Totale | Superati | Falliti |
|-----------|--------|----------|---------|
| Funzionalità core | [N] | [N] | [N] |
| Form e validazioni | [N] | [N] | [N] |
| Responsive | [N] | [N] | [N] |
| Accessibilità | [N] | [N] | [N] |
| Performance | [N] | [N] | [N] |
| **TOTALE** | **[N]** | **[N]** | **[N]** |

### 4.2 Tasso di successo
**[XX]%** dei test superati

---

## 5. Riepilogo Bug

### 5.1 Statistiche

| Severity | Trovati | Risolti | Aperti |
|----------|---------|---------|--------|
| Blocker | [N] | [N] | [N] |
| Major | [N] | [N] | [N] |
| Minor | [N] | [N] | [N] |
| Cosmetic | [N] | [N] | [N] |
| **TOTALE** | **[N]** | **[N]** | **[N]** |

### 5.2 Bug Blocker/Major risolti

| ID | Descrizione | Risolto in |
|----|-------------|------------|
| BUG-001 | [Descrizione] | v[X.X.X] |
| BUG-002 | [Descrizione] | v[X.X.X] |

### 5.3 Bug Minor/Cosmetic aperti (accettati per post go-live)

| ID | Descrizione | Piano risoluzione |
|----|-------------|-------------------|
| BUG-010 | [Descrizione] | Garanzia - entro [data] |
| BUG-011 | [Descrizione] | Backlog post go-live |

---

## 6. Funzionalità Verificate

### Checklist funzionalità core

- [x] [Funzionalità 1] — Verificata OK
- [x] [Funzionalità 2] — Verificata OK
- [x] [Funzionalità 3] — Verificata OK con nota: [nota]
- [ ] [Funzionalità 4] — Da completare post go-live (concordato)

---

## 7. Condizioni per Go-Live

### 7.1 Prerequisiti soddisfatti

- [x] Tutti i bug Blocker risolti
- [x] Tutti i bug Major risolti
- [x] Funzionalità core verificate e funzionanti
- [x] Performance accettabili
- [ ] Contenuti definitivi inseriti
- [ ] Redirect configurati (se migrazione)

### 7.2 Bug accettati per post go-live
Il Cliente accetta che i seguenti bug Minor/Cosmetic vengano risolti dopo il go-live:
- [Lista bug IDs]

### 7.3 Funzionalità rimandate (se presenti)
Le seguenti funzionalità sono state concordate per una fase successiva:
- [Lista funzionalità]

---

## 8. Dichiarazione UAT

### Esito

- [ ] **UAT SUPERATO** — Il sistema è pronto per il go-live
- [ ] **UAT SUPERATO CON RISERVA** — Pronto per go-live con condizioni elencate in sez. 7
- [ ] **UAT NON SUPERATO** — Richieste correzioni prima di nuovo UAT

### Note
[Eventuali note o condizioni particolari]

---

## 9. Prossimi Passi (post approvazione G3)

| Azione | Responsabile | Scadenza |
|--------|--------------|----------|
| Definizione data go-live | PM + Cliente | [Data] |
| Preparazione piano go-live | PM | [Data] |
| Comunicazione stakeholder | Cliente | [Data] |
| Go-live (G4) | Team | [Data] |

---

## Approvazione Gate G3

Con la presente approvazione, il Cliente conferma che:
1. I test UAT sono stati eseguiti
2. Il sistema risponde ai requisiti approvati
3. I bug aperti sono accettabili per go-live
4. Si autorizza la pianificazione del go-live

| Ruolo | Nome | Firma/Conferma | Data |
|-------|------|----------------|------|
| Referente Cliente | [Nome] | | |
| Project Manager Net7 | [Nome] | | |

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
