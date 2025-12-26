# Go-Live Plan

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Data go-live** | [GG/MM/AAAA] |
| **Ora prevista** | [HH:MM] |
| **Versione** | 1.0 |
| **Owner** | [PM] |

---

## 1. Pre-requisiti

### Checklist Pre Go-Live

- [ ] UAT completato e signoff ricevuto (G3)
- [ ] Bug Blocker/Major risolti
- [ ] Contenuti definitivi inseriti
- [ ] Redirect configurati (se migrazione)
- [ ] DNS preparato (TTL abbassato)
- [ ] Backup ambiente attuale
- [ ] Rollback plan pronto e testato
- [ ] Team disponibile e reperibile
- [ ] Cliente informato e disponibile
- [ ] Comunicazione stakeholder preparata

---

## 2. Team e Contatti

| Ruolo | Nome | Telefono | Disponibilità |
|-------|------|----------|---------------|
| PM | [Nome] | [Tel] | [Orari] |
| Tech Lead | [Nome] | [Tel] | [Orari] |
| Dev | [Nome] | [Tel] | [Orari] |
| Referente Cliente | [Nome] | [Tel] | [Orari] |
| Hosting/Ops | [Nome] | [Tel] | [Orari] |

---

## 3. Timeline Go-Live

| Ora | Attività | Responsabile | Durata | Stato |
|-----|----------|--------------|--------|-------|
| [HH:MM] | Backup ambiente attuale | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Freeze modifiche staging | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Deploy in produzione | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Configurazione ambiente | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Migrazione dati (se prevista) | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Switch DNS | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Smoke test | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Verifica con cliente | [Chi] | [Xmin] | ⬜ |
| [HH:MM] | Comunicazione "Siamo live" | [Chi] | [Xmin] | ⬜ |

---

## 4. Smoke Test Checklist

| Test | Esito |
|------|-------|
| Sito raggiungibile su URL produzione | ⬜ |
| HTTPS funzionante | ⬜ |
| Homepage carica correttamente | ⬜ |
| Login funziona | ⬜ |
| Pagine principali accessibili | ⬜ |
| Form principale funziona | ⬜ |
| [Test specifico progetto] | ⬜ |
| [Test specifico progetto] | ⬜ |

---

## 5. Criteri Go/No-Go

### GO se:
- Tutti i smoke test passati
- Nessun problema critico rilevato
- Cliente conferma OK

### NO-GO se:
- Smoke test critici falliti
- Problemi di performance gravi
- Errori bloccanti rilevati
→ Attivare **Rollback Plan**

---

## 6. Comunicazioni

### Pre go-live (inviare [data])
- [ ] Email a stakeholder: "Go-live previsto per [data/ora]"
- [ ] Avviso eventuale downtime (se necessario)

### Post go-live (inviare appena confermato)
- [ ] Email a stakeholder: "Siamo live!"
- [ ] Comunicazione social/newsletter (se prevista)

---

## 7. Post Go-Live

### Prime 24-48 ore
- Monitoraggio intensivo
- Reperibilità team
- Controllo log errori
- Risposta rapida a segnalazioni

### Prima settimana
- Monitoraggio giornaliero
- Raccolta feedback utenti
- Fix bug urgenti

---

## 8. Rollback

In caso di problemi gravi, seguire il **Rollback Plan** allegato.

Criteri per rollback:
- Sistema non funzionante
- Perdita dati
- Performance inaccettabili
- Errori critici non risolvibili in [N] ore

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
