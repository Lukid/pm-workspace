# Gate G1 — Approvazione Wireframe e Scope

> Documento di approvazione del perimetro funzionale e della struttura

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Cliente** | [Nome cliente] |
| **Versione** | 1.0 |
| **Data** | [GG/MM/AAAA] |
| **Redatto da** | [Nome PM] |
| **Destinatario** | [Nome referente cliente] |
| **Scadenza feedback** | [Data - 5gg lavorativi] |
| **Scadenza approvazione** | [Data - 3gg dopo feedback] |

---

## 1. Scopo del Documento

Questo documento richiede l'approvazione formale di:
1. **Perimetro funzionale** del progetto
2. **Struttura e navigazione** (wireframe)
3. **Criteri di accettazione** delle funzionalità

L'approvazione di questo documento costituisce il **Gate G1** e autorizza l'avvio della fase di design UI (mockup grafici).

---

## 2. Perimetro Funzionale

### 2.1 Funzionalità Incluse ✅

| ID | Funzionalità | Descrizione | Priorità |
|----|--------------|-------------|----------|
| F01 | [Nome] | [Descrizione breve] | Must |
| F02 | [Nome] | [Descrizione breve] | Must |
| F03 | [Nome] | [Descrizione breve] | Should |
| F04 | [Nome] | [Descrizione breve] | Could |

**Legenda priorità:**
- **Must**: Obbligatorio per il go-live
- **Should**: Importante, da includere se possibile
- **Could**: Desiderabile, valutabile in base a tempi/budget

### 2.2 Esplicitamente Escluso ❌

| ID | Funzionalità/Elemento | Motivo esclusione |
|----|----------------------|-------------------|
| X01 | [Nome] | [Motivo] |
| X02 | [Nome] | [Motivo] |
| X03 | [Nome] | [Motivo] |

> ⚠️ **Nota**: Qualsiasi richiesta relativa agli elementi esclusi richiederà una Change Request formale con valutazione di impatto su tempi e costi.

---

## 3. Struttura e Navigazione

### 3.1 Mappa del Sito / App

```
[Rappresentazione gerarchica - esempio:]

Home
├── Chi Siamo
│   ├── Storia
│   └── Team
├── Servizi
│   ├── Servizio A
│   ├── Servizio B
│   └── Servizio C
├── News
│   ├── Lista News
│   └── Dettaglio News
├── Contatti
└── Area Riservata
    ├── Login
    ├── Dashboard
    ├── Profilo
    └── [Altre sezioni]
```

### 3.2 Wireframe

I wireframe sono disponibili qui: **[Link a Figma / Miro / allegati]**

#### Elenco schermate incluse:

| ID | Schermata | Descrizione | Link |
|----|-----------|-------------|------|
| W01 | Homepage | [Descrizione] | [Link] |
| W02 | [Nome] | [Descrizione] | [Link] |
| W03 | [Nome] | [Descrizione] | [Link] |

### 3.3 Flussi Utente Principali

#### Flusso 1: [Nome flusso - es: Registrazione]
1. Utente accede a [pagina]
2. Compila form con [campi]
3. Sistema [azione]
4. Utente riceve [feedback]

#### Flusso 2: [Nome flusso]
1. ...

---

## 4. Requisiti Tecnici e Vincoli

### 4.1 Requisiti Non Funzionali

| Requisito | Specifica |
|-----------|-----------|
| Responsive | Mobile, Tablet, Desktop |
| Browser supportati | Chrome, Firefox, Safari, Edge (ultime 2 versioni) |
| Accessibilità | WCAG 2.1 Livello AA |
| Performance | Tempo caricamento < 3 secondi |
| Sicurezza | HTTPS, [altri requisiti] |

### 4.2 Integrazioni

| Sistema | Tipo | Responsabile | Stato |
|---------|------|--------------|-------|
| [Nome sistema] | API REST | [Chi] | [Disponibile/In corso/Da definire] |

---

## 5. Criteri di Accettazione

### Per ogni funzionalità principale:

#### F01: [Nome funzionalità]

**DATO CHE** [contesto/precondizione]
**QUANDO** [azione utente]
**ALLORA** [risultato atteso]

Esempio:
> **DATO CHE** sono un utente registrato sulla pagina di login
> **QUANDO** inserisco credenziali valide e clicco "Accedi"
> **ALLORA** vengo reindirizzato alla dashboard e vedo il mio nome in alto a destra

#### F02: [Nome funzionalità]
...

---

## 6. Contenuti

### 6.1 Responsabilità contenuti

| Tipo contenuto | Responsabile | Scadenza |
|----------------|--------------|----------|
| Testi pagine statiche | [Cliente/Net7] | [Data] |
| Immagini | [Cliente/Net7] | [Data] |
| Documenti PDF | [Cliente] | [Data] |
| Video | [Cliente] | [Data] |

### 6.2 Contenuti placeholder
Net7 inserirà contenuti placeholder dove non ancora disponibili. La sostituzione con contenuti definitivi è a carico di [Cliente/Net7].

---

## 7. SLA e Processo

### 7.1 Tempistiche approvazione

| Fase | Durata | Scadenza |
|------|--------|----------|
| Review wireframe | 5 gg lavorativi | [Data] |
| Consolidamento feedback | 2 gg lavorativi | [Data] |
| Approvazione formale | 3 gg lavorativi | [Data] |

### 7.2 Silenzio-assenso
In assenza di feedback entro la scadenza indicata, il presente documento si intenderà **approvato tacitamente** e Net7 procederà con la fase successiva (design UI/mockup).

### 7.3 Gestione modifiche post-approvazione
Dopo l'approvazione di questo documento:
- Modifiche al perimetro richiedono **Change Request** formale
- Modifiche alla struttura richiedono **Change Request** formale
- Chiarimenti e dettagli minori possono essere gestiti via email

---

## 8. Rischi Identificati

| ID | Rischio | Impatto | Mitigazione |
|----|---------|---------|-------------|
| R1 | [Descrizione] | [A/M/B] | [Azione] |
| R2 | [Descrizione] | [A/M/B] | [Azione] |

---

## 9. Prossimi Passi (post approvazione G1)

| Azione | Responsabile | Scadenza prevista |
|--------|--------------|-------------------|
| Avvio design UI/mockup | Designer | [Data] |
| Presentazione mockup | PM | [Data] |
| Richiesta approvazione G2 | PM | [Data] |

---

## 10. Checklist di Approvazione

Prima di approvare, verificare di aver:

- [ ] Revisionato tutte le funzionalità incluse
- [ ] Verificato che le esclusioni siano corrette
- [ ] Navigato i wireframe
- [ ] Validato i flussi utente
- [ ] Confermato i criteri di accettazione
- [ ] Verificato le responsabilità sui contenuti

---

## Approvazione Gate G1

### Dichiarazione
Con la presente approvazione, il Cliente conferma che:
1. Il perimetro funzionale descritto è corretto e completo
2. La struttura e i wireframe rappresentano quanto richiesto
3. I criteri di accettazione sono condivisi
4. Eventuali modifiche future seguiranno il processo di Change Request

### Firme

| Ruolo | Nome | Firma/Conferma | Data |
|-------|------|----------------|------|
| Referente Cliente | [Nome] | | |
| Project Manager Net7 | [Nome] | | |

---

### Modalità di approvazione

✅ **Opzione 1**: Firmare questo documento e restituire via email

✅ **Opzione 2**: Rispondere all'email di invio con testo:
> *"Confermo l'approvazione del documento Gate G1 - Wireframe e Scope versione [X.X] datato [GG/MM/AAAA]."*

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
