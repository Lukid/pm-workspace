# Gate G4 — Go-Live e Accettazione Finale

> Verbale di collaudo e chiusura progetto

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Cliente** | [Nome cliente] |
| **Codice contratto** | [Riferimento] |
| **Data go-live** | [GG/MM/AAAA] |
| **Data verbale** | [GG/MM/AAAA] |
| **Versione** | 1.0 |

---

## 1. Scopo del Documento

Questo documento certifica:
1. **Rilascio in produzione** del sistema
2. **Superamento smoke test**
3. **Accettazione formale** del progetto
4. **Avvio periodo di garanzia**

L'approvazione di questo documento costituisce il **Gate G4** e chiude formalmente il progetto.

---

## 2. Riepilogo Progetto

| Aspetto | Previsto | Effettivo | Scostamento |
|---------|----------|-----------|-------------|
| Data avvio (G0) | [Data] | [Data] | [+/- N gg] |
| Data go-live | [Data] | [Data] | [+/- N gg] |
| Budget | €[importo] | €[importo] | [+/- €X] |

---

## 3. Gate Superati

| Gate | Descrizione | Data approvazione |
|------|-------------|-------------------|
| G1 | Wireframe e Scope | [Data] |
| G2 | Mockup e Design UI | [Data] |
| G3 | UAT e Staging | [Data] |
| G4 | Go-live (questo doc) | [Data] |

---

## 4. Deliverable Consegnati

| Deliverable | Data consegna | Stato |
|-------------|---------------|-------|
| Sistema in produzione | [Data] | ✅ Consegnato |
| Documentazione tecnica | [Data] | ✅ / N/A |
| Manuale utente | [Data] | ✅ / N/A |
| Formazione | [Data] | ✅ / N/A |
| Codice sorgente | [Data] | ✅ / N/A |
| Credenziali e accessi | [Data] | ✅ Consegnato |

---

## 5. Ambiente di Produzione

| Aspetto | Dettaglio |
|---------|-----------|
| URL produzione | [https://...] |
| Versione rilasciata | [vX.X.X] |
| Hosting | [Provider/Server] |
| Backup configurato | Sì / No |
| Monitoraggio attivo | Sì / No |

---

## 6. Smoke Test

### 6.1 Risultati

| Test | Esito |
|------|-------|
| Sistema raggiungibile | ✅ OK |
| Login funzionante | ✅ OK |
| Pagine principali caricano | ✅ OK |
| Form principali funzionano | ✅ OK |
| [Test specifico] | ✅ OK |

### 6.2 Esito complessivo
**SMOKE TEST SUPERATO** — Il sistema è operativo in produzione.

---

## 7. Obiettivi di Progetto

| Obiettivo (da Brief) | Raggiunto | Note |
|----------------------|-----------|------|
| [Obiettivo 1] | ✅ Sì / ⚠️ Parziale / ❌ No | [Note] |
| [Obiettivo 2] | ✅ Sì / ⚠️ Parziale / ❌ No | [Note] |
| [Obiettivo 3] | ✅ Sì / ⚠️ Parziale / ❌ No | [Note] |

---

## 8. Riepilogo Economico

| Voce | Importo |
|------|---------|
| Valore contrattuale | €[importo] |
| Change Request approvate | €[importo] |
| **Totale progetto** | **€[importo]** |
| Già fatturato (SAL precedenti) | €[importo] |
| **Saldo finale** | **€[importo]** |

---

## 9. Anomalie Residue

### 9.1 Bug minori accettati
| ID | Descrizione | Piano risoluzione |
|----|-------------|-------------------|
| [BUG-XXX] | [Descrizione] | Garanzia - [data] |

### 9.2 Funzionalità rinviate
| Funzionalità | Motivo | Pianificazione |
|--------------|--------|----------------|
| [Nome] | [Motivo] | Fase 2 / Backlog |

---

## 10. Garanzia e Supporto

| Aspetto | Dettaglio |
|---------|-----------|
| Periodo garanzia | [N] mesi dalla data di questo verbale |
| Data inizio garanzia | [Data] |
| Data fine garanzia | [Data] |
| Copertura | Bug fix su funzionalità esistenti |
| Canale segnalazione | [Email / Ticket system] |
| SLA risposta | [Es: 8h lavorative per Blocker] |

### Cosa è coperto dalla garanzia
- Correzione bug su funzionalità rilasciate
- Malfunzionamenti rispetto ai requisiti approvati

### Cosa NON è coperto
- Nuove funzionalità
- Modifiche a funzionalità esistenti
- Problemi causati da interventi del cliente
- Problemi di hosting/infrastruttura non gestita da Net7

---

## 11. Handover

### 11.1 Documentazione consegnata
- [ ] Credenziali amministrazione
- [ ] Documentazione tecnica
- [ ] Guida contenuti (se CMS)
- [ ] Contatti supporto

### 11.2 Formazione erogata
- [ ] Formazione utenti: [Data], [Durata], [Partecipanti]
- [ ] Formazione admin: [Data], [Durata], [Partecipanti]

---

## 12. Lesson Learned (opzionale)

### Cosa ha funzionato bene
- [Punto positivo 1]
- [Punto positivo 2]

### Cosa migliorare
- [Area di miglioramento 1]
- [Area di miglioramento 2]

---

## 13. Dichiarazione di Chiusura

Con la firma del presente verbale, le parti dichiarano che:
1. Il progetto è **formalmente concluso**
2. Tutti i deliverable previsti sono stati **consegnati e accettati**
3. Il sistema è **operativo in produzione**
4. Il periodo di **garanzia è attivo** come da sezione 10
5. Non sussistono ulteriori obbligazioni contrattuali al di fuori di garanzia e supporto

---

## Approvazione Gate G4 — Chiusura Progetto

| Ruolo | Nome | Firma | Data |
|-------|------|-------|------|
| Sponsor / RUP (Cliente) | [Nome] | | |
| Referente Tecnico (Cliente) | [Nome] | | |
| Project Manager (Net7) | [Nome] | | |
| Responsabile (Net7) | [Nome] | | |

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
