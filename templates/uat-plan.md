# UAT Plan — Piano di Test Utente

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Versione** | 1.0 |
| **Data** | [GG/MM/AAAA] |
| **Ambiente test** | [URL staging] |
| **Periodo UAT** | [Data inizio] - [Data fine] |

---

## 1. Obiettivi

Verificare che il sistema:
- Soddisfi i requisiti funzionali approvati
- Sia utilizzabile dagli utenti finali
- Non presenti bug bloccanti

---

## 2. Scope del Test

### In scope
- [Funzionalità 1]
- [Funzionalità 2]
- [Funzionalità 3]

### Out of scope
- [Cosa non viene testato e perché]

---

## 3. Partecipanti

| Ruolo | Nome | Responsabilità |
|-------|------|----------------|
| Test Lead (Cliente) | [Nome] | Coordinamento test cliente |
| Tester | [Nome] | Esecuzione test |
| Supporto (Net7) | [Nome] | Assistenza tecnica |

---

## 4. Ambiente e Accessi

| Aspetto | Dettaglio |
|---------|-----------|
| URL | [https://...] |
| Utente test 1 | [username] / [ruolo] |
| Utente test 2 | [username] / [ruolo] |
| Credenziali | [Inviate separatamente] |

---

## 5. Criteri di Accettazione

### UAT Superato se:
- [ ] Tutti i test critici superati
- [ ] Nessun bug Blocker aperto
- [ ] Nessun bug Major aperto (o accettati per post go-live)
- [ ] Tasso successo test ≥ 90%

### UAT Non Superato se:
- Bug Blocker non risolti
- Funzionalità core non funzionanti
- Tasso successo < 80%

---

## 6. Processo di Segnalazione Bug

1. Tester identifica problema
2. Compila segnalazione con:
   - Descrizione (cosa succede vs cosa dovrebbe)
   - Passi per riprodurre
   - Screenshot/video
   - Severity proposta
3. Invia a [email/sistema]
4. Net7 conferma ricezione e severity
5. Net7 risolve e notifica
6. Tester verifica fix

---

## 7. Severity Bug

| Severity | Definizione | SLA |
|----------|-------------|-----|
| **Blocker** | Blocca uso sistema | Immediato |
| **Major** | Funzionalità core KO | 24-48h |
| **Minor** | Workaround disponibile | Pre go-live |
| **Cosmetic** | Solo estetico | Backlog |

---

## 8. Timeline

| Fase | Data | Durata |
|------|------|--------|
| Preparazione ambiente | [Data] | 1 gg |
| Esecuzione test | [Data-Data] | [N] gg |
| Triage bug | [Data] | 1 gg |
| Fix e re-test | [Data-Data] | [N] gg |
| Signoff | [Data] | 1 gg |

---

## 9. Deliverable

- [ ] UAT Checklist compilata
- [ ] Buglist con tutti i bug trovati
- [ ] Signoff UAT firmato (Gate G3)

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
