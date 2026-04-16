# CLAUDE.md — Team SEO Papernest

Istruzioni operative per agenti AI (Claude Code, Antigravity, Codex, o qualsiasi piattaforma agentica).
Questo file va nella root del progetto. L'agente lo legge automaticamente e sa come comportarsi.

## Il team

Team SEO & Digital Marketing @ Papernest (Barcellona, mercato italiano).
Stack: VS Code / Codex / Antigravity, HTML/CSS puro, WordPress (ppn-deal, ppn-cta, ppn-callout), Ahrefs, GSC.
Lingua: italiano per contenuti e comunicazione, inglese per codice e termini tecnici.

## Cosa facciamo

Content SEO per papernest.it — mercato energia italiano (luce e gas, domestico).
- **Revamp pagine**: analisi brief SEO, ottimizzazione contenuti, produzione HTML per WordPress
- **Migrazioni**: trasferimento contenuti da siti terzi con ottimizzazione SEO
- **Off-page**: articoli notizia per link building e outreach
- **Audit SEO**: analisi on-page, SERP, content gap, performance

## Architettura: spec-driven

Questo kit opera con un approccio **spec-driven**: le skill sono specifiche eseguibili che l'agente legge e sa esattamente cosa fare, senza interpretazioni.

- **Skill = SPEC**: documenti markdown con struttura fissa che guidano l'esecuzione
- **Principio**: AI probabilistica -> ragionamento; istruzioni precise -> esecuzione

Ogni SKILL.md segue questa anatomia (ordine intenzionale):
```
Intent -> Gotchas -> Runtime Rules (max 8) -> Test Prompt -> Input -> Workflow -> Output -> QA Gates
```

### Sezione Gotchas (obbligatoria)

Ogni skill DEVE avere una sezione `## Gotchas` tra Intent e Runtime Rules. Contiene i fallimenti ricorrenti e i comportamenti inattesi che l'agente deve evitare. Questa e' la sezione a piu' alto segnale di tutta la skill.

**Feedback loop**: quando una skill fallisce o produce output sotto-qualita', aggiornare i Gotchas PRIMA di fixare.

## Skill disponibili

| Skill | Path | Cosa fa |
|---|---|---|
| content-revamp | `skills/content-revamp/SKILL.md` | Pipeline completa: brief SEO validato -> HTML WordPress-ready |
| ppn-design-system | `skills/ppn-design-system/SKILL.md` | Gate obbligatorio per qualsiasi output HTML/CSS papernest.it |
| italian-proofreader | `skills/italian-proofreader/SKILL.md` | Revisione linguistica italiana pre-pubblicazione |
| seo-page-audit | `skills/seo-page-audit/SKILL.md` | Audit SEO on-page completo (heading, keyword, UX, linking) |
| off-page-article | `skills/off-page-article/SKILL.md` | Generazione articoli notizia per outreach/link building |
| prompt-optimizer | `skills/prompt-optimizer/SKILL.md` | Ottimizza prompt ambigui prima di eseguire |
| wp-page-builder | `skills/wp-page-builder/SKILL.md` | Genera/modifica HTML compatibile WordPress Gutenberg |
| page-checker | `skills/page-checker/SKILL.md` | Audit pagina migrata: heading spam/AI, fact-check, qualita' italiano (benchmark Paisa') |

### Routing delle skill

1. Prompt lungo/ambiguo -> **prompt-optimizer** prima di tutto
2. Task HTML/CSS per papernest.it -> **ppn-design-system** come pre-step obbligatorio
3. Produzione contenuto da brief -> **content-revamp**
4. Modifica HTML per WordPress -> **wp-page-builder**
5. Articolo off-page/outreach -> **off-page-article**
6. Audit SEO di una pagina -> **seo-page-audit**
7. Revisione finale prima di pubblicare -> **italian-proofreader**
8. Controlla pagina migrata / check page -> **page-checker**

## Design System Papernest CAT

Tutti i progetti che producono HTML/CSS per papernest.it DEVONO rispettare il Design System CAT.

- **Spec completa**: `design-system/DESIGN_SYSTEM_SPEC.md`
- **CSS Variables**: `design-system/design_tokens.css`
- **Skill gate**: `skills/ppn-design-system/SKILL.md`

### Colori core
| Token | Hex | Uso |
|-------|-----|-----|
| primary | `#5a52ff` | Bottoni, link, accenti |
| navy | `#212430` | Testo principale, heading |
| teal | `#02c5ae` | Badge, input, accenti |
| success | `#00bc7d` | Conferme, prezzi vantaggiosi |
| error | `#ff2056` | Errori, alert |

### Font
| Tipo | Font | Uso |
|------|------|-----|
| heading/body | Avenir | Titoli e testo |
| system | Inter | UI, etichette |
| display | Exo | Numeri grandi, dati |

## Vincoli WordPress (non negoziabili)

Questi vincoli valgono per QUALSIASI output HTML destinato a papernest.it su WordPress.

| Vincolo | Regola |
|---------|--------|
| JS inline | VIETATO `onclick`, `onchange` — solo `addEventListener` |
| JS wrapping | Sempre `setTimeout(fn, 300)` + `try/catch` |
| Radio/checkbox | Dentro `<div>` wrapper, mai figli diretti del root |
| Classi CSS | Prefissi obbligatori (es. `.ckq-`, `.tk-`, `.ppn-`) — no classi generiche |
| Selettore `~` | Funziona solo tra siblings diretti dello stesso parent |
| Plugin | Zero — non si possono installare plugin |
| Font external | Non caricare font esterni — usare quelli gia' disponibili nel tema |

## Formato Brief SEO

Il brief e' l'input principale per il workflow content-revamp. Formato standard:

| Campo | Descrizione |
|-------|-------------|
| Main Keyword | Keyword principale target (+ volume) |
| User Intent | Cosa vuole ottenere l'utente |
| Secondary KW | Da SERP, Ahrefs Explorer, Provider, Competitor |
| Struttura | Tag heading: `<h1>`, `<h2>`, `<h3>`, `<callout>`, `FAQ` |
| PAA | People Also Ask — domande correlate da Google |
| Featured Snippet | Opportunita' snippet (paragraph, list, table, N/A) |

## Convenzioni

### Output HTML
- Un file per blocco WordPress: `codice_intro.html` (H1 + intro), `codice_testo.html` (corpo)
- HTML valido per Gutenberg: `<!-- wp:paragraph -->`, `<!-- wp:heading -->`
- Nessun tag non supportato da WP

### Qualita' contenuto
- Italiano naturale, tono informativo-pratico
- NO marketing aggressivo, NO filler, NO ripetizioni keyword forzate
- Keyword density: 1-2% main, 0.5-1% secondary
- Min 3 link interni contestuali per pagina
- FAQ con schema markup `<details><summary>`

### Git (se usato)
- Commit in inglese, formato: `type: description`
- `.tmp/`, `__pycache__/`, `.env` non vanno committati

## Come usare questo kit

1. Copia l'intera cartella `team-kit/` nel tuo progetto o workspace
2. L'agente leggera' automaticamente il `CLAUDE.md` dalla root
3. Per attivare un workflow, riferisci la skill: "Esegui skills/content-revamp/SKILL.md"
4. Prepara i file di input come indicato nella skill
5. L'agente segue la pipeline step-by-step e produce l'output

### Su Antigravity (Gemini)
- Carica il contenuto di `CLAUDE.md` come system instruction
- Allega i file della skill come contesto
- Dai l'input (brief + HTML se presente)

### Su Codex (OpenAI)
- Metti la cartella nel workspace
- Codex leggera' i file automaticamente
- Lancia con: "Leggi CLAUDE.md e esegui [nome skill]"

### Su Claude Code
- Metti la cartella nel workspace (o nella root del repo)
- Claude Code legge CLAUDE.md automaticamente
- Lancia con: "Esegui skills/[nome-skill]/SKILL.md"
