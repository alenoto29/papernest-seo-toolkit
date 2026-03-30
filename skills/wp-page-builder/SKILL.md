---
name: wp-page-builder
description: "Genera o modifica HTML compatibile WordPress Gutenberg per papernest.it. Gestisce vincoli WP, blocchi custom, Design System CAT. Trigger: 'html wordpress', 'modifica pagina wp', 'codice gutenberg', 'wp-page'"
---

# WP Page Builder

## Intent

- **Obiettivo**: Produrre HTML che funziona al 100% copiato-incollato in WordPress Gutenberg, senza modifiche manuali
- **Ottimizza per**: Compatibilita' WP, funzionamento al primo tentativo, manutenibilita'
- **Sacrifica**: Eleganza del codice (WP ha i suoi vincoli, rispettarli > codice bello)
- **Successo**: Copia-incolla su WP, salva, preview = tutto funziona
- **Fallimento**: Layout rotto, JS non eseguito, stili persi, elementi scomparsi

## Gotchas

- **WP autoparagraph** (`wpautop`): Wrappa automaticamente il testo in `<p>`. Se un `<input>` o `<radio>` e' figlio diretto del root, WP lo wrappa in `<p>` e il layout si rompe. Mettere SEMPRE in `<div>` wrapper
- **Inline handler stripping**: WP rimuove `onclick`, `onchange`, `onsubmit`. Usare SOLO `addEventListener` via `<script>`
- **JS execution timing**: Il DOM potrebbe non essere pronto quando lo script esegue. Wrappare SEMPRE in `setTimeout(fn, 300)` + `try/catch`
- **CSS class collision**: Il tema WP ha classi generiche (`.card`, `.btn`, `.container`). Usare SEMPRE prefissi (`.ckq-`, `.tk-`, `.ppn-`)
- **Selettore CSS `~`**: Funziona SOLO tra siblings diretti dello stesso parent. Se gli elementi sono nested diversamente, non funziona
- **Commenti Gutenberg mancanti**: Senza `<!-- wp:paragraph -->` e `<!-- wp:heading -->`, Gutenberg tratta tutto come un blocco HTML unico
- **Font esterni**: Non si possono caricare font via `<link>` — usare solo quelli gia' nel tema (Avenir, Inter, Exo)
- **Plugin**: Non si possono installare. Tutto deve funzionare con HTML/CSS/JS puro
- **Style injection da Google Sheet**: Se la pagina carica dati da Sheet, l'HTML potrebbe contenere `<style>` tags inattesi. Sanitizzare SEMPRE con `.replace(/<style>.*?<\/style>/gi, '')`

## Runtime Rules

1. **Pre-step obbligatorio**: attivare `ppn-design-system` per verificare conformita' Design System CAT
2. **Un file = un blocco WP**: `codice_intro.html` (H1 + intro), `codice_testo.html` (corpo completo)
3. **`codice_intro.html` = H1 manuale**: spesso gestito direttamente in WP, non sovrascrivere se non richiesto
4. **Zero inline handler**: solo `addEventListener` in `<script>`
5. **Tutti `<input>`/`<radio>`/`<checkbox>`** dentro `<div>` wrapper — MAI figli diretti del root
6. **JS wrapping**: `setTimeout(function(){ try { ... } catch(e) { console.warn(e); } }, 300);`
7. **Classi con prefisso**: `.ckq-` (quiz), `.tk-` (contenuti), `.ppn-` (componenti) — zero classi generiche
8. **Commenti Gutenberg**: ogni blocco con `<!-- wp:paragraph -->`, `<!-- wp:heading {"level":N} -->`

## Componenti WP Disponibili

| Componente | Uso | Esempio |
|-----------|-----|---------|
| `<!-- wp:paragraph -->` | Paragrafi di testo | `<!-- wp:paragraph --><p>Testo</p><!-- /wp:paragraph -->` |
| `<!-- wp:heading -->` | Heading H2-H6 | `<!-- wp:heading {"level":2} --><h2>Titolo</h2><!-- /wp:heading -->` |
| `<ppn-deal>` | Card offerta fornitore | Blocco custom con dati offerta |
| `<ppn-cta-block-double>` | CTA doppio (luce + gas) | Blocco con 2 bottoni CTA |
| `<ppn-callout>` | Box evidenziato | Informazioni importanti, tips |
| `<details><summary>` | FAQ/accordion | Schema FAQ markup |

## Input

- Contenuto da trasformare in HTML WP (testo, brief, o HTML esistente)
- Tipo di blocco: intro o testo
- Indicazioni specifiche (se modifica a file esistente)

## Workflow

1. Leggi le istruzioni/contenuto da trasformare
2. Attiva pre-step `ppn-design-system`
3. Struttura l'HTML con commenti Gutenberg corretti
4. Applica classi con prefisso, font da tema, colori da token
5. Se c'e' JS: wrappa in setTimeout + try/catch, addEventListener only
6. Se ci sono form elements: verifica wrapper `<div>`
7. Valida con checklist QA

## Output

File HTML pronto per copia-incolla su WordPress Gutenberg.

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | HTML valido | No tag non chiusi, nesting corretto |
| 2 | Commenti Gutenberg | Presenti su ogni blocco |
| 3 | Zero inline handler | Nessun onclick/onchange/onsubmit |
| 4 | Input/radio in wrapper | Tutti in `<div>`, mai figli root |
| 5 | JS wrapping | setTimeout + try/catch |
| 6 | Classi con prefisso | .ckq- / .tk- / .ppn- su tutte |
| 7 | Design System | Colori, font, spacing da spec |
| 8 | No font esterni | Solo Avenir, Inter, Exo dal tema |
| 9 | No plugin dipendenze | Tutto HTML/CSS/JS puro |
