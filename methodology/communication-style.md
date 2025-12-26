# Stile di Comunicazione

Linee guida per la comunicazione con clienti e team.

---

## 1. Principi Generali

### Con il cliente
- **Professionale ma non burocratico**: formale quanto basta, umano sempre
- **Proattivo**: meglio comunicare troppo che troppo poco
- **Trasparente**: problemi segnalati subito, mai nascosti
- **Orientato alla soluzione**: ogni problema porta una proposta

### Con il team
- **Diretto**: no giri di parole
- **Specifico**: cosa, chi, quando
- **Supportivo**: blocchi risolti insieme

---

## 2. Canali di Comunicazione

| Canale | Quando usare | Formalità |
|--------|--------------|-----------|
| **Email** | Comunicazioni formali, decisioni, approvazioni | Alta |
| **Call/Meet** | Discussioni complesse, kickoff, SAL | Media |
| **Chat (Slack/Teams)** | Domande rapide, coordinamento quotidiano | Bassa |
| **GitLab** | Tutto ciò che riguarda task e codice | Tecnica |
| **Telefono** | Urgenze, escalation | Alta (se critico) |

### Regola d'oro
> Se una decisione è importante, deve finire in **email** o **documento**. Le chat sono effimere.

---

## 3. Email al Cliente

### Struttura tipo

```
Oggetto: [Progetto] - [Argomento chiaro]

Ciao [Nome],

[1-2 frasi di contesto se necessario]

[Corpo del messaggio - cosa devo comunicare]

[Se servono azioni]
Ti chiedo di:
- [Azione 1] entro [data]
- [Azione 2] entro [data]

[Se serve decisione]
Attendo conferma entro [data]. In assenza di risposta, 
procederò con [opzione default].

[Chiusura]
Resto a disposizione per chiarimenti.

A presto,
[Firma]
```

### Esempi pratici

#### Richiesta approvazione

```
Oggetto: [Portale ANCI] - Approvazione mockup area riservata

Ciao Maria,

come concordato, abbiamo completato i mockup dell'area riservata 
del portale.

Trovi i file qui: [link Figma]

Le schermate includono:
- Dashboard utente
- Profilo e impostazioni
- Storico richieste

Ti chiedo di revisionarli e darmi un feedback entro venerdì 24/01.
Se non ho osservazioni entro tale data, considererò i mockup 
approvati e procederemo con lo sviluppo (Gate G2).

Per eventuali modifiche dopo l'approvazione, seguiremo il processo 
di Change Request concordato.

Resto a disposizione per una call se preferisci discuterne insieme.

A presto,
Luca
```

#### Segnalazione problema

```
Oggetto: [Portale ANCI] - Ritardo consegna API - Impatto su timeline

Ciao Maria,

ti segnalo che abbiamo riscontrato un ritardo nella disponibilità 
delle API del sistema XYZ, che dovevano essere pronte per il 15/01.

**Situazione attuale:**
- API non ancora disponibili
- Contattato il fornitore, stimano consegna entro 22/01

**Impatto:**
- Lo sviluppo del modulo di integrazione è bloccato
- Rischio ritardo di 1 settimana sul SAL di febbraio

**Azioni in corso:**
- Ho sollecitato nuovamente il fornitore
- Nel frattempo, il team procede con altre attività

**Opzioni:**
1. Attendere le API (rischio ritardo)
2. Sviluppare con mock e integrare dopo (costo extra stimato: 8h)

Ti chiedo di indicarmi come preferisci procedere.

A presto,
Luca
```

#### Chiusura SAL

```
Oggetto: [Portale ANCI] - SAL Gennaio 2025 - Richiesta approvazione

Ciao Maria,

in allegato trovi il SAL relativo al periodo 01/01 - 31/01/2025.

**Sintesi:**
- Completate tutte le attività previste per il periodo
- Avanzamento complessivo: 45%
- Nessuna criticità aperta

**Prossimi passi:**
- Inizio UAT previsto per 15/02
- Ti invierò il piano di test entro fine settimana

Ti chiedo di confermare il SAL entro 5 giorni lavorativi (07/02).
In assenza di osservazioni, il SAL si intenderà approvato.

A presto,
Luca
```

---

## 4. Comunicazioni Difficili

### Cliente chiede qualcosa fuori scope

**NON dire:**
> "No, questo non è incluso."

**Dire:**
> "Sì, possiamo farlo. Questa funzionalità non era nel perimetro che 
> abbiamo approvato insieme, quindi devo valutarne l'impatto e 
> proporti una Change Request. Ti mando la stima entro domani — 
> se la approvi, la inseriamo nella pianificazione."

### Cliente non risponde

**Prima sollecitazione (dopo 3-5 gg):**
> "Ciao Maria, ti riscrivo per un gentile sollecito sulla richiesta 
> del [data]. Attendo un tuo riscontro per poter procedere."

**Seconda sollecitazione (dopo altri 3-5 gg):**
> "Ciao Maria, non avendo ricevuto risposta, ti informo che se non 
> ho tue notizie entro [data], procederò con [opzione default] come 
> da processo concordato."

**Escalation (se continua):**
> Coinvolgere sponsor/RUP con email in CC al referente:
> "Gentile [Sponsor], in assenza di riscontro da parte di [Referente] 
> su [tema], mi vedo costretto a segnalare la situazione per evitare 
> impatti sulla timeline del progetto."

### Progetto in ritardo (per causa nostra)

**Essere trasparenti:**
> "Ciao Maria, devo segnalarti che siamo in ritardo di circa 1 settimana 
> sulla consegna prevista per [data]. Il ritardo è dovuto a [causa onesta]. 
> Abbiamo già preso queste contromisure: [azioni]. La nuova data prevista 
> è [nuova data]. Mi scuso per il disagio e resto a disposizione per 
> discuterne."

### Cliente arrabbiato

1. **Ascoltare** senza interrompere
2. **Validare** il problema ("Capisco la frustrazione")
3. **Non giustificarsi** troppo
4. **Proporre soluzione** concreta
5. **Follow-up scritto** con quanto concordato

---

## 5. Verbali di Riunione

### Quando servono
- Kickoff
- SAL meeting
- Riunioni decisionali
- Call con decisioni importanti

### Formato

```markdown
# Verbale Riunione - [Argomento]

**Data**: [GG/MM/AAAA]
**Partecipanti**: [Nomi]
**Redatto da**: [Nome]

## Agenda
1. [Punto 1]
2. [Punto 2]

## Discussione

### [Punto 1]
[Sintesi discussione]

### [Punto 2]
[Sintesi discussione]

## Decisioni prese
- [Decisione 1]
- [Decisione 2]

## Azioni
| Azione | Responsabile | Scadenza |
|--------|--------------|----------|
| [Azione 1] | [Chi] | [Quando] |
| [Azione 2] | [Chi] | [Quando] |

## Prossimo incontro
[Data e argomenti previsti]
```

### Invio
- Inviare entro 24h dalla riunione
- Chiedere conferma o correzioni
- Archiviare nella cartella progetto

---

## 6. Escalation

### Quando escalare
- Cliente non risponde da >10 gg su tema bloccante
- Rischio sforamento budget >20%
- Conflitto che non si risolve
- Problemi tecnici gravi in produzione

### Come escalare

1. **Documenta** il problema (per iscritto)
2. **Proponi** soluzioni (non solo il problema)
3. **Identifica** il livello giusto (chi può decidere)
4. **Comunica** con rispetto per tutti

### Template escalation

```
Oggetto: [ESCALATION] [Progetto] - [Problema]

Ciao [Responsabile],

ti scrivo per segnalare una situazione che richiede la tua attenzione
sul progetto [Nome].

**Problema:**
[Descrizione chiara e fattuale]

**Impatto:**
[Cosa succede se non si interviene]

**Azioni già tentate:**
[Cosa abbiamo già fatto]

**Opzioni proposte:**
1. [Opzione A] - Pro: ... Contro: ...
2. [Opzione B] - Pro: ... Contro: ...

**Raccomandazione:**
[Cosa suggerisci]

Resto a disposizione per una call se utile.

Luca
```

---

## 7. Tono per Contesto

### PA (Pubblica Amministrazione)
- Più formale
- Riferimenti a normative se rilevanti
- Attenzione ai ruoli (RUP, DEC, ecc.)
- Documentazione più strutturata

### Privato (PMI)
- Più diretto e informale
- Focus su valore e risultati
- Flessibilità maggiore
- Comunicazione più frequente e snella

### Privato (Corporate)
- Via di mezzo
- Spesso interlocutori multipli
- Attenzione a catena decisionale
- Documentazione comunque importante

---

## 8. Do's and Don'ts

### ✅ Do

- Rispondere entro 24h (anche solo per confermare ricezione)
- Usare oggetto email chiaro e specifico
- Mettere le azioni richieste in evidenza
- Confermare a voce le cose importanti per iscritto
- Ringraziare quando appropriato
- Ammettere errori e proporre soluzioni

### ❌ Don't

- Lasciare email senza risposta per giorni
- Usare toni passivo-aggressivi
- Nascondere problemi sperando si risolvano
- Promettere cose che non puoi mantenere
- Scrivere email chilometriche senza struttura
- Mettere in CC persone a caso "per copertura"

---

*Questo documento è parte del Sistema Qualità Net7 — ISO 9001:2015*
