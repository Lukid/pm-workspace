---
# Metadata progetto — YAML valido, parsabile
nome: "[Nome Progetto]"
codice: "[Codice interno / CIG / CUP]"
cliente: "[Nome Cliente]"
tipo: "PA"  # PA | Privato
contratto: "Fixed Price"  # Fixed Price | T&M

budget: 0  # in euro, senza simbolo
data_inizio: "YYYY-MM-DD"
data_golive_prevista: "YYYY-MM-DD"
data_golive_effettiva: null
stato: "In corso"  # In corso | Completato | Sospeso | Annullato

gitlab_url: "https://gitlab.net7.it/..."
staging_url: "https://staging..."
production_url: "https://..."
drive_folder: "https://drive.google.com/..."
openmemo_id: ""

team_net7:
  - ruolo: "PM"
    nome: "Luca"
    email: ""
  - ruolo: "Tech Lead"
    nome: ""
    email: ""
  - ruolo: "Dev"
    nome: ""
    email: ""
  - ruolo: "Designer"
    nome: ""
    email: ""

team_cliente:
  - ruolo: "Sponsor/RUP"
    nome: ""
    email: ""
    telefono: ""
  - ruolo: "Referente operativo"
    nome: ""
    email: ""
    telefono: ""

gates:
  G1_wireframe:
    stato: "pending"  # pending | approved
    data: null
  G2_mockup:
    stato: "pending"
    data: null
  G3_uat:
    stato: "pending"
    data: null
  G4_golive:
    stato: "pending"
    data: null

note: |
  [Informazioni importanti da ricordare, peculiarità del cliente, vincoli particolari]

documenti_contesto:
  - nome: "Progetto esecutivo cliente"
    presente: false
  - nome: "Specifiche tecniche"
    presente: false
  - nome: "Brand guidelines"
    presente: false
---

# Project Context

Questo file contiene i metadata del progetto in formato YAML (frontmatter).

## Come usare questo file

1. **Compila il frontmatter YAML** sopra con i dati reali del progetto
2. **Aggiorna lo stato dei gate** man mano che vengono approvati
3. **Aggiungi note** per informazioni importanti da ricordare

## Documenti di contesto

Carica nella cartella `context/` i documenti esterni rilevanti:
- Progetto esecutivo del cliente
- Specifiche tecniche
- Brand guidelines
- Email importanti
- Altro materiale di riferimento

Poi aggiorna la sezione `documenti_contesto` nel frontmatter.

---

*Ultimo aggiornamento: [Data]*
