---
name: italian-proofreader
description: "Revisione linguistica professionale italiano (standard Treccani) pre-pubblicazione. Trigger: 'revisione', 'proofreading', 'controlla italiano', 'pre-publish', ultimo step prima di pubblicare"
---

# Italian Proofreader

## Intent

- **Obiettivo**: Ogni testo visibile al 100% italiano corretto — accenti, grammatica, sintassi, registro
- **Ottimizza per**: Correttezza linguistica, leggibilita', tono coerente
- **Sacrifica**: Nulla — gli errori linguistici danneggiano credibilita' e SEO
- **Successo**: Zero errori linguistici nell'output pubblicato
- **Fallimento**: Accento sbagliato, concordanza errata, o registro misto (tu/lei) in produzione

## Gotchas

- **Accenti gravi vs acuti**: L'errore piu' comune. `perche'` vuole l'accento acuto (perche'), `cioe'` grave (cioe'). Controllare SEMPRE la lista accenti
- **HTML entity trap**: In HTML gli accenti possono essere entity (`&agrave;`, `&eacute;`) — verificare che siano corretti, non solo belli
- **Contenuto tecnico**: NON correggere nomi brand (Enel, Iren, A2A), sigle (kWh, PSV, PUN), URL, o valori numerici
- **Modifica struttura**: Questa skill corregge SOLO la lingua — non toccare HTML, CSS, JS, link, prezzi, numeri
- **Registro misto**: papernest.it usa il "tu" — verificare che non ci siano "Lei" o forme impersonali

## Runtime Rules

1. **Leggi tutto l'HTML**, estrai solo il testo visibile (heading, paragrafi, label, placeholder, alt, title, contenuto card)
2. **Ignora**: classi CSS, attributi tecnici, JS, numeri puri, URL, nomi brand
3. **Ordine check**: accenti -> grammatica -> coniugazioni -> sintassi -> leggibilita'
4. **Cita sempre**: originale + errore + correzione (con numero riga se possibile)
5. **Applica le correzioni** direttamente nel file
6. **Non aggiungere testo** — solo correzioni all'esistente
7. **Rileggi dopo le correzioni** per verificare che siano state applicate correttamente
8. **Registro "tu"** coerente in tutto il documento

## Checklist Accenti (priorita' massima)

| Corretto | Errore comune | Regola |
|----------|---------------|--------|
| e (congiunzione) | e' | Senza accento |
| e' (verbo essere) | e | Con accento grave |
| perche' | perche | Acuto |
| cioe' | cioe | Grave |
| poiche' | poiche | Acuto |
| pero' | pero | Grave |
| puo' | puo | Grave |
| stabilita', qualita' | stabilita, qualita | Grave |
| verra' | verra | Grave |

## Checklist Grammatica

- Concordanza soggetto-verbo (singolare/plurale)
- Concordanza aggettivo-nome (genere + numero)
- Articoli corretti (il/lo/la/i/gli/le)
- Preposizioni articolate (del/dello/della/dei/degli/delle)

## Checklist Verbi

- Coniugazione corretta (persona, tempo, modo)
- Coerenza temporale (non saltare tra presente e passato)
- Preferire attivo > passivo (per chiarezza)

## Checklist Sintassi

- Frasi > 30 parole -> valutare se spezzare
- Soggetto chiaro in ogni frase
- Nessuna ambiguita' pronominale
- Registro "tu" coerente (no "Lei", no impersonale misto)

## Input

File HTML con contenuto in italiano da revisionare.

**Errore se manca:** Nessun file fornito = STOP

## Workflow

1. Leggi l'intero file HTML
2. Estrai tutto il testo visibile (ignora markup, JS, CSS)
3. Scansiona seguendo le checklist in ordine (accenti PRIMA di tutto)
4. Per ogni errore trovato: annota riga, originale, tipo errore, correzione
5. Applica tutte le correzioni nel file
6. Rileggi le sezioni corrette per verificare
7. Conferma completamento con report degli errori trovati/corretti

## Output

- File HTML corretto in-place
- Report testuale: numero errori trovati, tipo, correzioni applicate

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | Accenti | Tutti corretti (gravi/acuti, entity HTML) |
| 2 | Verbi | Nessun errore di coniugazione |
| 3 | Concordanze | Soggetto-verbo, aggettivo-nome corretti |
| 4 | Sintassi | Frasi chiare, no ambiguita' |
| 5 | Registro | "Tu" coerente, nessun "Lei" |
| 6 | Nessuna modifica non-linguistica | HTML/CSS/JS/link/prezzi/numeri intatti |
