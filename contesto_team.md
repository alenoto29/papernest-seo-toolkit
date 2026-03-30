# Contesto Team — SEO & Digital Marketing Papernest

## Chi siamo

Team SEO & Digital Marketing di Papernest, sede Barcellona.
Lavoriamo sul mercato italiano (papernest.it) nel settore energia (luce e gas, utenze domestiche).

## Cosa facciamo

### Content SEO
- **Revamp pagine esistenti**: partendo da un brief SEO (keyword, struttura, intent), ottimizziamo il contenuto delle pagine e produciamo HTML pronto per WordPress
- **Migrazioni contenuto**: trasferiamo contenuti da siti terzi ottimizzandoli per SEO
- **Pagine nuove**: creiamo contenuti da zero basandoci su keyword research e content gap

### Off-Page & Link Building
- Produzione articoli notizia per outreach (formato giornalistico)
- Link building tramite partnership editoriali

### Audit & Analisi
- Audit SEO on-page (heading, keyword, UX, linking, performance)
- Analisi SERP per keyword target
- Content gap analysis rispetto ai competitor

## Stack tecnico

| Tool | Uso |
|------|-----|
| WordPress (Gutenberg) | CMS per papernest.it — blocchi intro + testo |
| HTML/CSS puro | Output contenuti — no framework, no plugin |
| Ahrefs | Keyword research, content gap, backlink analysis |
| Google Search Console | Performance query, CTR, posizioni |
| Google Sheets | Gestione dati, brief, tracking |
| Componenti WP custom | `ppn-deal`, `ppn-cta`, `ppn-callout`, `ppn-cta-block-double` |

## Processo standard (content revamp)

```
1. Keyword research (Ahrefs + GSC)
        |
2. Brief SEO (struttura H1-H3, keyword mapping, intent)
        |
3. Validazione brief (team review)
        |
4. [DA QUI PARTE L'AGENTE]
        |
5. Analisi brief + pagina esistente (se presente)
        |
6. Generazione contenuto ottimizzato
        |
7. Produzione HTML WordPress-ready
        |
8. Revisione linguistica (italian-proofreader)
        |
9. QA check (keyword density, heading, link, design system)
        |
10. Copia-incolla su WordPress Gutenberg
```

L'agente entra al punto 4 (brief gia' validato) e produce l'output al punto 9 (HTML pronto).

## Design System CAT

Tutti gli output HTML/CSS DEVONO rispettare il Design System CAT di Papernest.
Il design system e' nella cartella `design-system/` di questo kit.

Colori principali: `#5a52ff` (purple), `#212430` (navy), `#02c5ae` (teal), `#00bc7d` (success), `#ff2056` (error).
Font: Avenir (heading/body), Inter (system), Exo (display).

## Mercato di riferimento

- **Paese**: Italia
- **Settore**: Energia (luce e gas)
- **Target**: Consumatori domestici
- **Lingua contenuti**: Italiano
- **Tono**: Informativo, pratico, accessibile — NO marketing aggressivo
- **Competitor principali**: Selectra, Luce-Gas.it, Prontobolletta, comparatori energia

## Regole di qualita' contenuto

1. **Accuratezza**: nessun prezzo/dato inventato — solo dati verificabili (ARERA, fonte ufficiale)
2. **SEO on-page**: keyword density 1-2% main, 0.5-1% secondary, min 3 link interni
3. **Leggibilita'**: frasi max 25-30 parole, paragrafi max 3-4 frasi, struttura chiara
4. **WordPress**: HTML valido per Gutenberg, nessun inline handler, classi con prefisso
5. **Design System**: colori, font, spacing, componenti da spec CAT — nessuna deroga
6. **Lingua**: italiano corretto (accenti, concordanze, registro "tu"), revisione obbligatoria pre-publish
