---
name: llm_query
description: "Genera 50 sub-query LLM-style (2 cluster da 25) da export GSC + URL pagina papernest, per analisi SERP manuale. Usare quando l'utente fornisce export GSC, dice 'sub-query LLM', 'ottimizzare per LLM', 'query LLM-style', 'llm_query', o vuole estrarre query conversazionali da lista keyword."
model_tier: sonnet-high
model_rationale: "Skill LLM-only, no script. Reasoning su filtro semantico query + clustering + generazione varietà semantica. Sonnet sufficiente; Opus solo se filtro qualitativo cala."
---

# llm_query

Da export GSC (CSV o lista nuda) + URL pagina target → 1 file Markdown con 50 sub-query LLM-style clusterizzate in 2 main topic, pronte per analisi SERP manuale.

## Quick start
- Input: `gsc_export.csv` (o `query.txt`) + URL `https://www.papernest.it/<slug>/`
- Comando: invoca skill, passa file + URL
- Output: `work/team-kit/skills/llm_query/output/llm_query_<slug>.md` con 2 sezioni da 25 sub-query

## Intent
- **Obiettivo**: produrre 50 sub-query LLM-style (2x25) coerenti con pagina target, in <2 min, pronte per scraping SERP manuale
- **Ottimizza per**: varietà semantica + plausibilità "domanda reale fatta a LLM" + copertura pattern (how-to, comparativa, problem, pricing, process, definition, use-case)
- **Sacrifica**: copertura esaustiva di tutti i topic emersi (forziamo a 2 main topic, gli altri vengono scartati)
- **Successo**: Alessandro lancia analisi SERP sulle 50 sub-query senza riscrivere/scartare nessuna riga
- **Fallimento**: sub-query risultano short-tail SEO, duplicati semantici, o non coerenti con pagina target → da rifare a mano

## Gotchas
- **Encoding BOM UTF-8**: GSC esporta CSV con BOM. Parsing ingenuo legge `﻿Query` invece di `Query` come header. Strip BOM esplicito.
- **Input misto IT/EN**: GSC può contenere query in entrambe le lingue. Filtrare solo IT (euristica: parole IT comuni, no anglismi puri brand-only).
- **Forzatura 2 topic su dataset asimmetrico**: se 80% query gravitano su un solo topic, splittarlo per granularità (es. "costi" vs "processo attivazione") invece di forzare un secondo topic debole.
- **Main keyword sintetica ≠ query top-impression**: NON copiare la query con più impressioni. Generare espressione canonica del cluster.
- **Varietà posizionale main keyword**: rischio default = tutte le sub-query iniziano con la main keyword. Distribuire: ~33% inizio, ~33% metà, ~33% fine/omissione.
- **Dedupe semantico**: rischio = 25 query con stesso significato + sinonimi ("come cambiare fornitore" / "come passare ad altro fornitore"). Self-check finale: ogni query deve aggiungere un angolo nuovo (intent/scenario/pattern diverso).
- **Da popolare dopo 3-5 usi reali**: aggiornare con fallimenti concreti.

## Runtime Rules
1. Output **sempre** italiano, anche se input contiene query EN miste (filtrate via).
2. **No abort**: anche con <10 query LLM-filtered procedere (warning interno, output completo).
3. **Esattamente 2 main topic** — mai 1, mai 3+. Se asimmetrico, splittare il dominante.
4. **Main keyword sintetica** generata da Claude — mai estratta come top-impression.
5. **Distribuzione pattern coverage** in ogni lista da 25: almeno 1 query per ciascun tipo (how-to, comparativa, problem, pricing, process, definition, use-case). Resto libero.
6. **Lunghezza sub-query**: 8-15 parole. Sotto = short-tail SEO, sopra = innaturale.
7. **Posizione main keyword variata**: ~1/3 inizio, ~1/3 metà, ~1/3 fine o omessa se semanticamente sensato.
8. **Output unico**: 1 file `.md` finale. NO report intermedi, NO log step.

## Test Prompt

### Test 1 — Standard CSV GSC
Input: `gsc_offerte_luce_fisso.csv` (300 query miste IT, header `Query,Click,Impressioni,CTR,Posizione`) + URL `https://www.papernest.it/energia/offerte-luce-prezzo-fisso/`
Atteso: file `output/llm_query_offerte-luce-prezzo-fisso.md` con 2 main topic distinti (es. "scelta tariffa fissa vs variabile" + "processo attivazione luce fissa"), 50 sub-query LLM-style, main keyword in posizioni varie, no duplicati semantici, almeno 1 query per ogni pattern coverage.

### Test 2 — Edge: lista nuda
Input: `queries.txt` (80 query nude, una per riga, no header) + URL `https://www.papernest.it/cambio-residenza/`
Atteso: skill detecta lista (no header `Query`), procede comunque, output completo 2x25.

### Test 3 — Edge: pochi LLM-match
Input: CSV con 200 query di cui solo 8 LLM-style (resto short-tail brand) + URL pagina
Atteso: skill non aborta, genera comunque 2 main topic + 50 sub-query estrapolando da context URL + 8 query LLM-real come seed.

## Input
1. **File query** — uno tra:
   - CSV GSC standard (header includa `Query`, encoding UTF-8 con o senza BOM)
   - Lista nuda `.txt` o `.csv` (una query per riga, no header)
2. **URL pagina target** — string, formato `https://www.papernest.it/<path>/`
3. **Slug** — string opzionale. Se assente, derivato da ultimo segmento path URL (strip `/`, slash → trattini).

Errori → STOP:
- File assente o vuoto
- URL non valido / non `papernest.it`
- 0 query estraibili dopo parsing

## Workflow

### Step 1 — Parse input
- Leggere file. Strip BOM UTF-8 se presente.
- Detect formato: prima riga contiene `Query` (case-insensitive)? → CSV GSC, estrarre colonna `Query`. Altrimenti → lista nuda, ogni riga = 1 query.
- Pulire: strip whitespace, lowercase per dedupe, rimuovere righe vuote.
- Filtrare lingua: tenere solo query IT (euristica: presenza parole IT comuni "come/quale/perché/quanto/è/ho/devo/posso/mio/la/il/di/per/con", no query 100% EN o brand-only).
- Se 0 query rimanenti → STOP con errore.

### Step 2 — Filtro LLM (confidence ≥90%)
Per ogni query, valutare presenza segnali LLM-style:
- Lunghezza ≥5 parole (peso alto)
- Presenza interrogativi: come, perché, qual è, quale, quanto, cosa, dove, quando (peso alto)
- Verbi modali: posso, devo, dovrei, si può, mi conviene (peso alto)
- Pronomi personali: io, mi, mia, mio, ho (peso medio)
- Struttura naturale (soggetto + verbo + complementi) vs keyword secca (peso alto)
- Frase completa, leggibile (peso medio)
- ESCLUDERE: brand-only ("papernest"), short-tail (<4 parole), keyword secche tipo "offerte luce 2026", liste senza verbo

Mantenere solo query con confidence stimata ≥90%. Se filtrate <10 query, procedere comunque (warning interno; usare query disponibili + URL come seed per generazione).

### Step 3 — Pattern recognition
Analizzare cluster filtrato. Identificare **esattamente 2 main topic**:
- Se cluster ha 2+ tematiche distinte → prendere le 2 più rappresentate
- Se cluster monotematico → splittare per granularità (es. "costo" vs "processo", "scelta" vs "attivazione")
- Per ogni topic: estrarre pain point principale dell'utente

### Step 4 — Main keyword sintetica
Per ogni main topic, generare 1 espressione canonica del cluster:
- NON la query top-impression
- Espressione naturale che cattura il dominio semantico (4-8 parole)
- Esempio: cluster su "come confrontare offerte luce variabile" → main keyword sintetica "confronto offerte luce indicizzate al PUN"

### Step 5 — Generazione 25 sub-query per topic
Per ogni main keyword, generare 25 sub-query LLM-style rispettando:
- **Lunghezza**: 8-15 parole
- **Stile**: domanda completa, conversazionale, italiano naturale
- **Posizione main keyword**: ~33% inizio, ~33% metà, ~33% fine OPPURE omessa se ha senso semantico
- **Pattern coverage** (almeno 1 per tipo, resto libero):
  - how-to (come fare X)
  - comparativa (X vs Y, meglio X o Y)
  - problem (problema/dubbio dell'utente)
  - pricing (costi, prezzi, conviene)
  - process (passaggi, tempi, scadenze)
  - definition (cosa significa, cos'è)
  - use-case (scenario concreto)
- **Coerenza pagina target**: ogni sub-query deve essere plausibile per chi cerca info su URL fornito
- **No duplicati semantici**: self-check finale — se 2 query dicono stessa cosa con sinonimi diversi, sostituire una con angolo nuovo

### Step 6 — Validazione + write output
QA Gates (vedi sezione QA Gates). Se passa → scrivere file `output/llm_query_<slug>.md` con SOLO 2 liste finali. Se fallisce → rigenerare lista problematica.

## Output

**Path**: `work/team-kit/skills/llm_query/output/llm_query_<slug>.md`

**Formato**:
```markdown
# LLM Query Expansion — <slug>

**URL pagina**: <url>
**Data**: YYYY-MM-DD

---

## Topic 1: <main keyword sintetica 1>

1. <sub-query 1>
2. <sub-query 2>
...
25. <sub-query 25>

## Topic 2: <main keyword sintetica 2>

1. <sub-query 1>
...
25. <sub-query 25>
```

NO sezioni intermedie (no "query LLM filtrate", no "pattern", no debug).

## QA Gates

Pre-consegna verificare (pass/fail):
- [ ] Esattamente 50 sub-query totali (25 + 25)
- [ ] Esattamente 2 main keyword sintetiche, distinte semanticamente
- [ ] Ogni sub-query ha 8-15 parole
- [ ] Ogni sub-query è in italiano, formulata come domanda/frase conversazionale (non keyword secca)
- [ ] In ogni lista da 25: main keyword presente in ≥15 query, posizione variata (almeno 5 inizio, 5 metà, 5 fine/omessa)
- [ ] In ogni lista da 25: presente almeno 1 query per ciascun pattern (how-to, comparativa, problem, pricing, process, definition, use-case)
- [ ] No duplicati semantici (verifica che ogni query aggiunga angolo nuovo)
- [ ] Sub-query coerenti con argomento URL pagina target
- [ ] File output salvato in path corretto, formato Markdown valido

Se qualsiasi gate fallisce → rigenerare la lista interessata, non consegnare output incompleto.

---

*Questa skill ha bisogno di 3-5 usi reali prima di stabilizzarsi. Dopo ogni uso: cosa ha funzionato, cosa si è rotto, cosa era ambiguo. Aggiornare Gotchas solo con evidenze.*
