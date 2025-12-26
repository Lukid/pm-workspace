# UAT Checklist

---

## Metadata

| Campo | Valore |
|-------|--------|
| **Progetto** | [Nome progetto] |
| **Tester** | [Nome] |
| **Data test** | [GG/MM/AAAA] |
| **Ambiente** | [URL] |
| **Versione** | [vX.X.X] |

---

## Istruzioni

Per ogni test:
1. Eseguire i passi indicati
2. Verificare il risultato atteso
3. Segnare l'esito: ✅ Pass | ❌ Fail | ⏭️ Skip
4. Se Fail: annotare bug ID e note

---

## Test Generali

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T01 | Homepage carica | Accedere a [URL] | Pagina carica in < 3s | | |
| T02 | Menu navigazione | Cliccare su ogni voce menu | Pagine corrispondenti si aprono | | |
| T03 | Footer link | Cliccare link footer | Link funzionanti | | |
| T04 | Responsive mobile | Aprire su mobile/emulatore | Layout adattato correttamente | | |

---

## Autenticazione

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T10 | Login valido | 1. Vai a login<br>2. Inserisci credenziali valide<br>3. Clicca Accedi | Redirect a dashboard | | |
| T11 | Login invalido | Inserisci password errata | Messaggio errore chiaro | | |
| T12 | Logout | Clicca Logout | Redirect a home, sessione chiusa | | |
| T13 | Password dimenticata | Clicca "Password dimenticata" | Form reset funziona | | |

---

## [Area Funzionale 1]

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T20 | [Nome test] | [Passi] | [Risultato] | | |
| T21 | [Nome test] | [Passi] | [Risultato] | | |

---

## [Area Funzionale 2]

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T30 | [Nome test] | [Passi] | [Risultato] | | |
| T31 | [Nome test] | [Passi] | [Risultato] | | |

---

## Form e Validazioni

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T40 | Form con dati validi | Compilare form correttamente | Invio OK, feedback positivo | | |
| T41 | Form campi obbligatori vuoti | Lasciare campi vuoti | Errori di validazione chiari | | |
| T42 | Form email invalida | Inserire email malformata | Errore validazione | | |

---

## Performance

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T50 | Tempo caricamento home | Misurare con DevTools | < 3 secondi | | |
| T51 | Tempo caricamento pagine interne | Navigare 5 pagine | < 2 secondi ciascuna | | |

---

## Accessibilità (base)

| ID | Test | Passi | Risultato atteso | Esito | Bug ID |
|----|------|-------|------------------|-------|--------|
| T60 | Navigazione tastiera | Tab attraverso pagina | Focus visibile, ordine logico | | |
| T61 | Contrasto testo | Verificare leggibilità | Testo leggibile | | |
| T62 | Alt text immagini | Ispezionare immagini | Alt presenti | | |

---

## Riepilogo

| Categoria | Totale | Pass | Fail | Skip |
|-----------|--------|------|------|------|
| Generali | | | | |
| Autenticazione | | | | |
| [Area 1] | | | | |
| [Area 2] | | | | |
| Form | | | | |
| Performance | | | | |
| Accessibilità | | | | |
| **TOTALE** | | | | |

---

## Note Tester

[Osservazioni generali, problemi ricorrenti, suggerimenti]

---

## Firma

| Ruolo | Nome | Data |
|-------|------|------|
| Tester | | |

---

*Documento creato seguendo le linee guida del Sistema Qualità Net7 — ISO 9001:2015*
