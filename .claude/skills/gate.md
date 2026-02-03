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

Genera un documento di approvazione Gate con wizard interattivo per raccogliere le informazioni necessarie.

## Istruzioni

### 1. Identifica il progetto

Se `$ARGUMENTS` contiene un nome progetto, usa quello.
Altrimenti:
- Controlla se la directory corrente è sotto `projects/`
- Se sì, usa quel progetto
- Se no, chiedi all'utente quale progetto

Carica `.project-context.md` per ottenere:
- Nome progetto, cliente, CIG/CUP
- Stato gate precedenti
- Tipo cliente (PA/Privato)
- Team e contatti

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

Se il gate precedente non è approvato, avvisa l'utente e chiedi se procedere comunque.

### 4. Wizard domande per tipo gate

#### G1 — Wireframe e Scope

Chiedi in sequenza:
1. "Link ai wireframe (Figma/Miro)?"
2. "Le funzionalità incluse sono già documentate? Se sì, dove?"
3. "Ci sono esclusioni esplicite da evidenziare?"
4. "Data prevista per feedback cliente?"

#### G2 — Mockup e Design UI

Chiedi in sequenza:
1. "Link Figma ai mockup completi?"
2. "Link al prototipo navigabile (se presente)?"
3. "Elenco pagine principali da includere nella tabella?"
   - Suggerisci: Homepage, Listing, Dettaglio, Area riservata, ecc.
4. "Link all'UI kit / Design System (se separato)?"
5. "Il progetto è PA? (per sezione conformità normativa WCAG/AgID)"
6. "Data consegna ufficiale?"

#### G3 — UAT e Staging

Chiedi in sequenza:
1. "URL ambiente staging?"
2. "Periodo UAT (date inizio-fine)?"
3. "Riepilogo bug: quanti Blocker/Major/Minor risolti?"
4. "Ci sono bug Minor accettati per post go-live?"
5. "Tutte le funzionalità core sono verificate?"

#### G4 — Go-live e Chiusura

Chiedi in sequenza:
1. "URL produzione?"
2. "Versione rilasciata?"
3. "Data effettiva go-live?"
4. "Smoke test superato? Eventuali note?"
5. "Periodo garanzia (mesi)?"
6. "Ci sono anomalie residue o funzionalità rinviate?"

### 5. Genera il documento

Usa il template appropriato da `templates/gate-GX-*.md` ma:

**Per progetti PA**, aggiungi sezione conformità:
```markdown
## Conformità normativa

| Normativa/Linea guida | Stato | Note |
| :---- | :---- | :---- |
| **Linee Guida Design PA** (AgID) | ✓ Conforme | [note] |
| **WCAG 2.1 Livello AA** | ✓ Previsto | Verifiche accessibilità in fase sviluppo |
| **Legge 4/2004** (Legge Stanca) | ✓ Previsto | Dichiarazione accessibilità post go-live |
| **GDPR** | ✓ Conforme | Privacy by design applicata |
```

**Per G2**, usa formato tabella con link diretti:
```markdown
| Pagina | Link |
| :---- | :---- |
| Homepage | ✓ [Figma](link) |
| Elenco [X] | ✓ [Figma](link) |
```

**Struttura snella** (modello Sviluppo Toscana):
1. Metadata essenziali
2. Oggetto (1 paragrafo)
3. Deliverable consegnati (con link)
4. Conformità (se PA)
5. Criteri di accettazione (checklist breve)
6. SLA e silenzio-assenso
7. Impatto approvazione
8. Approvazione formale
9. Allegati (lista link)

### 6. Calcola date SLA

- **Review**: +5 giorni lavorativi dalla data consegna
- **Approvazione**: +3 giorni lavorativi dalla scadenza review

Usa calendario lavorativo (escludi weekend).

### 7. Salva il documento

Salva in: `projects/[nome-progetto]/gates/G[N]-[tipo].md`

Dove `[tipo]`:
- G1 → `wireframe`
- G2 → `mockup`
- G3 → `uat`
- G4 → `golive`

### 8. Aggiorna project-context

Dopo la creazione, suggerisci di aggiornare `.project-context.md`:
```yaml
gates:
  G[N]_[tipo]:
    stato: "pending"  # diventerà "approved" dopo approvazione
    data: null        # data approvazione
```

### 9. Output finale

```
Gate G[N] generato: gates/G[N]-[tipo].md

Riepilogo:
- Progetto: [nome]
- Cliente: [cliente]
- Data consegna: [data]
- Scadenza review: [data]
- Scadenza approvazione: [data]

Prossimi passi:
1. Revisiona il documento generato
2. Esporta in PDF se richiesto dal cliente
3. Invia al cliente con email di accompagnamento
```

## Esempi di utilizzo

```bash
# Wizard completo
/gate

# Specifica tipo
/gate G2

# Specifica progetto e tipo
/gate G2 sviluppo-toscana

# Solo progetto (chiede tipo)
/gate anci-cittadino-informato
```

## Note

- Il wizard è progettato per raccogliere solo le info essenziali
- Se mancano informazioni, usa placeholder "[DA COMPLETARE]"
- Per progetti PA, includi sempre sezione conformità
- I link Figma sono preferiti per deliverable design
