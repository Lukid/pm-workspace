# Actions Log

> Registro azioni e follow-up

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Ultimo aggiornamento** | [GG/MM/AAAA] |

---

## Azioni Aperte

| ID | Azione | Owner | Scadenza | Priorità | Origine | Stato | Issue GitLab |
|----|--------|-------|----------|----------|---------|-------|--------------|
| A-001 | [Descrizione azione] | [Chi] | [Data] | 🔴/🟡/🟢 | [SAL/Call/Email] | 🔄 In corso | [#123](https://gitlab.../issues/123) |
| A-002 | [Descrizione azione] | [Chi] | [Data] | 🔴/🟡/🟢 | [Origine] | ⏳ Da fare | - |
| A-003 | [Descrizione azione] | [Chi] | [Data] | 🔴/🟡/🟢 | [Origine] | ⚠️ In ritardo | - |

---

## Azioni Completate

| ID | Azione | Owner | Completata il | Note |
|----|--------|-------|---------------|------|
| A-010 | [Descrizione] | [Chi] | [Data] | [Esito] |
| A-011 | [Descrizione] | [Chi] | [Data] | [Esito] |

---

## Legenda

### Priorità
- 🔴 Alta — Urgente, blocca altro
- 🟡 Media — Importante, pianificata
- 🟢 Bassa — Quando c'è tempo

### Stato
- ⏳ Da fare
- 🔄 In corso
- ⚠️ In ritardo
- ✅ Completata
- ❌ Annullata

---

## Template Azione (copia e compila)

```markdown
| A-XXX | [Descrizione] | [Chi] | [Data] | 🟡 | [Origine] | ⏳ | - |
```

---

## Note Sincronizzazione GitLab

- Usa il comando `Sincronizza GitLab [progetto]` per creare automaticamente issue GitLab dalle azioni aperte
- Le azioni con priorità 🔴 → Issue P0 (critical)
- Le azioni con priorità 🟡 → Issue P1 (high)
- Le azioni con priorità 🟢 → Issue P2 (medium)
- Il comando aggiornerà automaticamente la colonna "Issue GitLab" con i link

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
