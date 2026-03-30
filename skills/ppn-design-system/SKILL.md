---
name: ppn-design-system
description: "Gate obbligatorio per qualsiasi output HTML/CSS destinato a papernest.it. Verifica conformita' al Design System CAT. Trigger: qualsiasi task che produce HTML/CSS per papernest."
---

# PPN Design System Gate

## Intent

- **Obiettivo**: Garantire che ogni output HTML/CSS per papernest.it sia conforme al Design System CAT
- **Ottimizza per**: Coerenza visiva, manutenibilita', compatibilita' WP
- **Successo**: Output visivamente identico alle pagine live di papernest.it
- **Fallimento**: Colori fuori spec, font sbagliati, spacing arbitrari

## Gotchas

- **Troppe sfumature**: Figma ha centinaia di shade — usare SOLO i token core dal CSS (`design_tokens.css`), non inventare variazioni
- **Font fallback mancante**: Avenir non e' disponibile ovunque — dichiarare sempre lo stack completo: `'Avenir', 'Helvetica Neue', Arial, sans-serif`
- **WordPress stripping**: WP rimuove alcuni stili inline — usare classi CSS con prefisso, non `style="..."`
- **Case sensitivity**: I colori nel CSS sono case-insensitive ma lo spec usa lowercase — mantenere lowercase per consistenza
- **Spacing inventato**: Non usare valori arbitrari (13px, 22px) — solo i valori dalla scala: 4, 8, 12, 16, 20, 24, 32, 40, 48, 64px
- **Shadow sbagliato**: Non inventare box-shadow — usare solo quelli definiti in `design_tokens.css`

## Runtime Rules

1. **Leggi SEMPRE** `design-system/DESIGN_SYSTEM_SPEC.md` e `design-system/design_tokens.css` prima di scrivere CSS
2. **Colori**: solo token dal CSS variables (`--cat-primary`, `--cat-navy`, etc.) — nessun hex hardcoded
3. **Font**: Avenir (heading/body), Inter (system/UI), Exo (display/numeri) — con fallback stack
4. **Spacing**: solo valori dalla scala (4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128px)
5. **Border radius**: scala standard (4, 6, 8, 12, 16, 24px, 9999px per pill)
6. **Shadow**: solo da `design_tokens.css` (`--cat-shadow-sm`, `-md`, `-lg`, `-card`, etc.)
7. **Componenti PPN**: usare le varianti documentate (`ppn-deal`, `ppn-cta`, `ppn-callout`, `ppn-cta-block-double`)
8. **Prefissi CSS**: obbligatori per evitare conflitti con il tema WP (`.ckq-`, `.tk-`, `.ppn-`)

## Test Prompt

**Test 1 — Colore non in spec**
Input: "Usa #3498db per il bottone CTA"
Output atteso: Rifiuto — suggerisce `--cat-primary` (#5a52ff) o `--cat-teal` (#02c5ae) come alternative

**Test 2 — CTA teal**
Input: "Crea un bottone CTA teal con bordo arrotondato"
Output atteso: `background: var(--cat-teal)`, `border-radius: var(--cat-radius-base)` (8px), font Avenir, padding da scala spacing

**Test 3 — Card pattern**
Input: "Card con shadow e bordo"
Output atteso: `box-shadow: var(--cat-shadow-card)`, `border: 1px solid var(--cat-border-default)`, `border-radius: var(--cat-radius-lg)` (12px), padding 24px

## Input

Nessun input specifico — questa skill si attiva come pre-step di un'altra skill che produce HTML/CSS.

## Workflow

1. Leggi `design-system/DESIGN_SYSTEM_SPEC.md` (sezioni rilevanti)
2. Leggi `design-system/design_tokens.css` (token completi)
3. Verifica che il task principale rispetti i token
4. Se l'output contiene violazioni, correggi prima di produrre il risultato finale

## Output

Non produce un file — garantisce la conformita' dell'output prodotto dalla skill principale.

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | Colori | Tutti da spec (token CSS, nessun hex arbitrario) |
| 2 | Font stack | Avenir/Inter/Exo con fallback completo |
| 3 | Spacing | Tutti dalla scala (4-128px) |
| 4 | Border radius | Dalla scala standard |
| 5 | Shadow | Solo da design_tokens.css |
| 6 | Prefissi CSS | Presenti su tutte le classi custom |
| 7 | Componenti PPN | Usati correttamente, nessun override del tema |
| 8 | Responsive | Consistente con breakpoint standard |
