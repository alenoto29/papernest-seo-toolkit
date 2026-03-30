---
name: content-revamp
description: "Pipeline completa: brief SEO validato + HTML esistente -> HTML ottimizzato WordPress Gutenberg-ready. Trigger: 'revamp', 'migrazione', 'ottimizza pagina', 'content da brief'"
---

# Content Revamp

## Intent

- **Obiettivo**: Trasformare un brief SEO validato in HTML pronto per WordPress Gutenberg, ottimizzato per ranking
- **Ottimizza per**: Keyword coverage, readability, UX, conformita' Design System CAT
- **Sacrifica**: Velocita' di produzione (meglio lento e corretto che veloce e da rifare)
- **Successo**: HTML copia-incollato su WP senza modifiche manuali, pagina indicizzata con keyword target in top 10
- **Fallimento**: HTML che richiede rework manuale, keyword mancanti, heading non conformi al brief

## Gotchas

- **Heading inventati**: L'agente tende ad aggiungere H2/H3 non presenti nel brief. VIETATO — seguire la struttura del brief alla lettera
- **Keyword stuffing**: Ripetere la main keyword 15 volte non aiuta. Density 1-2%, variazioni naturali
- **Blocchi WP sbagliati**: Dimenticare i commenti `<!-- wp:paragraph -->` rende il contenuto un blocco unico in Gutenberg
- **Link generici**: "Clicca qui" o "scopri di piu'" come anchor text = zero valore SEO. Anchor con keyword descrittive
- **FAQ senza schema**: Le FAQ devono avere markup `<details><summary>` per lo schema, non semplici H3 + paragrafo
- **Design System ignorato**: Se l'output usa colori o font non del Design System CAT, va rifatto. Leggere la skill ppn-design-system PRIMA
- **Meta tag dimenticati**: Title e meta description sono parte dell'output, non un "nice to have"
- **Contenuto tradotto**: Se la fonte e' in inglese, non tradurre letteralmente. Riscrivere in italiano naturale per il mercato IT

## Runtime Rules

1. **Leggi il brief completo** prima di scrivere qualsiasi cosa — non iniziare dalla prima sezione
2. **Segui la struttura heading del brief** alla lettera — non inventare, non riordinare, non saltare
3. **Attiva ppn-design-system** come pre-step per qualsiasi output HTML/CSS
4. **Ogni H2/H3 deve contenere** la keyword assegnata nel brief (naturalmente, non forzata)
5. **Link interni**: min 3, anchor text descrittivi con keyword, contestuali al paragrafo
6. **FAQ**: formato `<details><summary>` con schema markup, risposte 40-80 parole
7. **Meta tag obbligatori**: title (max 65 char, main KW front-loaded), meta description (max 145 char)
8. **Revisione finale**: esegui italian-proofreader prima di dichiarare l'output completo

## Test Prompt

**Test 1 — Revamp standard**
Input: Brief con main KW "enel numero verde", 4 H2, 2 H3, 3 secondary KW
Output atteso: HTML con tutti gli heading del brief, main KW in H1 e primo paragrafo, secondary KW distribuite, 3+ link interni, FAQ section, meta tag

**Test 2 — Migrazione con HTML esistente**
Input: Brief + codice HTML della pagina attuale da un altro sito
Output atteso: Contenuto rielaborato (non copiato), struttura da brief (non dalla pagina originale), keyword ottimizzate, HTML WP-ready

**Test 3 — Brief con callout e FAQ**
Input: Brief con `<callout>` e `FAQ` nella struttura
Output atteso: Callout renderizzato come blocco evidenziato con classe `.ppn-callout`, FAQ con `<details><summary>`, nessun heading extra non presente nel brief

## Input

**Obbligatorio:**
- Brief SEO compilato (formato Brief.xlsx o equivalente)
  - Main Keyword + volume
  - Secondary KW (SERP, Explorer, Provider, Competitor)
  - User Intent
  - Struttura heading validata (H1, H2, H3, callout, FAQ)
  - PAA (People Also Ask)

**Opzionale:**
- HTML sorgente della pagina attuale (se revamp/migrazione)
- Export GSC (query, CTR, posizione)
- Export Ahrefs (keyword, volume, difficulty)

**Errore se manca:** Brief senza struttura heading = STOP, chiedere completamento

## Workflow

### Step 1 — Analisi Brief
1. Leggi il brief completo: main KW, secondary KW, user intent, struttura H1-H3, PAA
2. Identifica: tipo pagina (revamp vs migrazione vs nuova), target snippet, micro-moments
3. Crea mappa keyword -> heading (ogni heading ha la sua keyword assegnata)

### Step 2 — Analisi Pagina Esistente (se presente)
1. Parsa l'HTML attuale: heading structure, word count, keyword density attuale
2. Identifica: cosa tenere (contenuto ancora valido), cosa eliminare, cosa aggiungere
3. Nota: NON copiare contenuto dall'originale — riscrivere seguendo il brief

### Step 3 — Pre-step Design System
1. Leggi `skills/ppn-design-system/SKILL.md`
2. Leggi `design-system/design_tokens.css` per i token CSS
3. Conferma: colori, font, spacing, componenti WP disponibili

### Step 4 — Generazione Contenuto
Per ogni sezione del brief (in ordine):
1. Scrivi il contenuto seguendo heading e keyword assegnata
2. Integra secondary KW naturalmente (variazioni, sinonimi, entita' correlate)
3. Usa blocchi WP corretti: `<!-- wp:heading -->`, `<!-- wp:paragraph -->`
4. Callout: `<div class="ppn-callout">...</div>`
5. FAQ: `<details><summary>Domanda?</summary><p>Risposta</p></details>`
6. Link interni: distribuiti nei paragrafi, anchor con keyword

### Step 5 — Ottimizzazione SEO
1. **Title tag**: max 65 char, main KW nelle prime parole
2. **Meta description**: max 145 char, include main KW + call-to-action
3. **Keyword density check**: main 1-2%, secondary 0.5-1%
4. **Heading hierarchy**: H1 unico, H2 per sezioni, H3 per sotto-sezioni — nessun salto
5. **Internal linking**: min 3, anchor descrittivi, pagine rilevanti di papernest.it
6. **Entita' semantiche**: termini correlati al topic (es. per "numero verde" -> "assistenza clienti", "servizio clienti", "contatto telefonico")

### Step 6 — Revisione Linguistica
1. Esegui `skills/italian-proofreader/SKILL.md` sull'output
2. Correggi tutti gli errori trovati

### Step 7 — QA Finale
1. Verifica checklist completa (vedi QA Gates)
2. Produci output finale

## Output

Due file HTML:
- **`codice_intro.html`** — H1 + paragrafo introduttivo (blocco intro WP)
- **`codice_testo.html`** — Corpo completo: heading, paragrafi, FAQ, callout, CTA, link interni

Meta tag suggeriti (in testa all'output o come commento):
- Title tag
- Meta description

Checklist SEO compilata (inline come commento HTML o come nota separata)

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | H1 unico con main keyword | Main KW presente nel H1 |
| 2 | Tutti gli heading del brief presenti | Nessun H2/H3 mancante o aggiunto |
| 3 | Keyword density | Main 1-2%, secondary 0.5-1% |
| 4 | Link interni | Min 3, anchor descrittivi |
| 5 | FAQ con schema markup | `<details><summary>` presente |
| 6 | Title tag | Max 65 char, main KW front-loaded |
| 7 | Meta description | Max 145 char, CTA + main KW |
| 8 | HTML Gutenberg-valid | Commenti WP corretti, no tag non supportati |
| 9 | Design System CAT | Colori, font, spacing da spec |
| 10 | Italian-proofreader eseguito | Zero errori linguistici |
