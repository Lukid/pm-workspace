# Rollback Plan

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Data go-live** | [GG/MM/AAAA] |
| **Versione** | 1.0 |
| **Owner** | [Tech Lead] |

---

## 1. Quando Attivare il Rollback

Attivare il rollback se:
- [ ] Sistema non raggiungibile dopo deploy
- [ ] Errori critici che impediscono l'uso
- [ ] Perdita dati o corruzione
- [ ] Performance gravemente degradate
- [ ] Problemi non risolvibili entro [N] ore

**Decisione finale**: [PM] in accordo con [Cliente]

---

## 2. Contatti Emergenza

| Ruolo | Nome | Telefono |
|-------|------|----------|
| Tech Lead | [Nome] | [Tel] |
| DevOps/Hosting | [Nome] | [Tel] |
| PM | [Nome] | [Tel] |
| Cliente | [Nome] | [Tel] |

---

## 3. Procedura di Rollback

### Step 1: Comunicazione
- [ ] Avvisare PM: "Attivo rollback"
- [ ] Avvisare Cliente: "Stiamo risolvendo, torniamo alla versione precedente"

### Step 2: Stop traffico (se possibile)
```bash
# [Comando o procedura per mettere in manutenzione]
```

### Step 3: Ripristino applicazione
```bash
# [Comandi per ripristinare versione precedente]
# Es: git checkout [tag-precedente]
# Es: docker rollback
# Es: restore da backup
```

### Step 4: Ripristino database (se necessario)
```bash
# [Comandi per restore DB]
# Backup location: [path/URL]
# Comando restore: [comando]
```

### Step 5: Ripristino configurazioni
- [ ] File configurazione: [path]
- [ ] Variabili ambiente: [dove]
- [ ] DNS (se modificato): [istruzioni]

### Step 6: Verifica
- [ ] Sito raggiungibile
- [ ] Login funziona
- [ ] Dati presenti
- [ ] Funzionalità core OK

### Step 7: Comunicazione
- [ ] Avvisare PM: "Rollback completato"
- [ ] Avvisare Cliente: "Servizio ripristinato, stiamo analizzando il problema"

---

## 4. Backup Disponibili

| Tipo | Location | Data | Come ripristinare |
|------|----------|------|-------------------|
| Codice | [Git tag/branch] | [Data] | `git checkout [ref]` |
| Database | [Path/URL] | [Data] | [Comando] |
| File/Media | [Path/URL] | [Data] | [Comando] |
| Configurazioni | [Path] | [Data] | [Istruzioni] |

---

## 5. Tempo Stimato Rollback

| Fase | Durata stimata |
|------|----------------|
| Comunicazione | 5 min |
| Stop traffico | 5 min |
| Ripristino app | [X] min |
| Ripristino DB | [X] min |
| Verifica | 10 min |
| **TOTALE** | **[X] min** |

---

## 6. Post-Rollback

1. [ ] Documentare cosa è andato storto
2. [ ] Analisi root cause
3. [ ] Piano di fix
4. [ ] Comunicazione al cliente su prossimi passi
5. [ ] Ripianificare go-live

---

## 7. Test del Rollback

**Data ultimo test**: [Data]
**Esito**: OK / KO
**Note**: [Eventuali note]

> ⚠️ **Importante**: Testare la procedura di rollback PRIMA del go-live in ambiente di staging.

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
