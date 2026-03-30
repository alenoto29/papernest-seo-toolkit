---
name: seo-page-audit
description: "Audit SEO on-page completo: heading, keyword, contenuto, UX, linking, meta tag, performance. Trigger: 'audit seo', 'analizza pagina', 'check seo', 'audit on-page'"
---

# SEO Page Audit

## Intent

- **Obiettivo**: Identificare tutti i problemi SEO on-page di una pagina e fornire fix concreti ordinati per impatto
- **Ottimizza per**: Copertura (non saltare nessuna area) + azionabilita' (ogni finding ha un fix specifico)
- **Successo**: Report che permette di correggere la pagina senza ulteriori analisi
- **Fallimento**: Problemi generici ("migliorare i contenuti") senza indicazione concreta

## Gotchas

- **Audit superficiale**: Dire "heading structure da migliorare" senza dire QUALE heading e COME — inutile. Essere specifici
- **Falsi positivi keyword density**: Una density del 3% non e' automaticamente stuffing se il testo e' naturale. Valutare nel contesto
- **Ignorare mobile**: Papernest ha traffico mobile importante. Verificare sempre breakpoint e layout responsive
- **Link rotti non verificabili**: Se non puoi fare HTTP request, segnala i link ma marca come "da verificare manualmente"
- **Confondere SEO con UX**: La pagina puo' avere UX perfetta ma SEO scarso (o viceversa). Analizzare separatamente

## Runtime Rules

1. **Leggi l'HTML completo** della pagina prima di qualsiasi giudizio
2. **9 aree di check** in ordine (vedi Workflow) — non saltarne nessuna
3. **Severita' su 3 livelli**: Critico (blocca ranking), Medio (impatta ma non blocca), Basso (miglioramento)
4. **Ogni finding ha**: problema specifico + dove (riga/elemento) + fix proposto
5. **Non modificare il file** — solo report
6. **Se hai dati GSC/Ahrefs**, integra nell'analisi (query attuali, posizioni, CTR)
7. **Confronto con brief** (se fornito): verifica che tutti gli heading e keyword del brief siano presenti
8. **Verdetto finale**: Pubblicabile / Pubblicabile con fix minori / Da revisionare

## Input

**Obbligatorio:**
- HTML della pagina da auditare

**Opzionale:**
- Brief SEO della pagina (per confronto struttura)
- Export GSC (query, CTR, posizione)
- Export Ahrefs (keyword target, volume, difficulty)
- URL della pagina live (per contesto)

## Workflow

### Check 1 — Meta Tag
- Title tag: presente, max 65 char, main KW front-loaded
- Meta description: presente, max 145 char, CTA + main KW
- Canonical: presente e corretto
- Hreflang: presente se pagina multilingua

### Check 2 — Heading Structure
- H1: unico, contiene main keyword
- Gerarchia: H1 > H2 > H3 senza salti (no H1 > H3)
- Ogni H2/H3 contiene keyword rilevante (main o secondary)
- Nessun heading vuoto o duplicato
- Confronto con brief (se fornito): tutti gli heading presenti

### Check 3 — Keyword Coverage
- Main keyword: presente in H1, primo paragrafo, title, meta description
- Keyword density: 1-2% main, 0.5-1% secondary
- Secondary keyword: distribuite nelle sezioni pertinenti
- Variazioni e sinonimi: presenti per naturalezza
- Entita' semantiche: termini correlati al topic

### Check 4 — Contenuto
- Word count: adeguato al tipo pagina (informativa 800-1500, comparativa 1200-2000)
- Qualita': no filler, no contenuto duplicato, no paragrafi vuoti
- Struttura: paragrafi brevi (max 3-4 frasi), liste puntate dove appropriato
- FAQ: presente con markup schema (`<details><summary>`)
- Aggiornamento: date e informazioni attuali (non obsolete)

### Check 5 — Internal Linking
- Numero: min 3 link interni contestuali
- Anchor text: descrittivi con keyword (no "clicca qui")
- Distribuzione: sparsi nel contenuto, non ammassati
- Link funzionanti: URL validi di papernest.it (segnalare sospetti)
- Deep linking: link a pagine interne rilevanti, non solo homepage

### Check 6 — UX & Readability
- Mobile-friendly: breakpoint presenti, no overflow, testo leggibile
- Layout: blocchi ben separati, gerarchia visiva chiara
- CTA: presente, visibile, con testo azionabile
- Immagini: alt text con keyword, dimensioni appropriate

### Check 7 — WordPress Compatibility
- Commenti Gutenberg: `<!-- wp:paragraph -->`, `<!-- wp:heading -->` presenti
- Nessun inline handler (`onclick`, `onchange`)
- Classi con prefisso (`.ckq-`, `.tk-`, `.ppn-`)
- JS wrappato in `setTimeout` + `try/catch`
- Radio/checkbox in `<div>` wrapper

### Check 8 — Design System
- Colori: conformi al Design System CAT
- Font: Avenir/Inter/Exo (no font esterni)
- Spacing: dalla scala standard
- Componenti: `ppn-deal`, `ppn-cta`, `ppn-callout` usati correttamente

### Check 9 — Schema & Structured Data
- FAQ schema: markup presente e valido
- Breadcrumb: presente
- Organization: presente (se pagina principale)

## Output

Report strutturato:

```
## Riepilogo
X problemi critici | Y medi | Z bassi
Verdetto: [Pubblicabile / Fix minori / Da revisionare]

## Dettaglio per area

### 1. Meta Tag
[finding con severita' + fix]

### 2. Heading Structure
[...]

... (tutte le 9 aree)

## Fix prioritari (top 5)
1. [fix piu' impattante]
2. ...
```

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | Tutte le 9 aree verificate | Nessuna area saltata |
| 2 | Ogni finding ha fix specifico | No problemi generici |
| 3 | Severita' assegnata | Ogni finding ha Critico/Medio/Basso |
| 4 | Verdetto finale | Presente e motivato |
| 5 | Confronto con brief | Se brief fornito, gap segnalati |
