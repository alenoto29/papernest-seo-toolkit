# Italian Writing Patterns — Reference

Quantitative patterns extracted from Paisà corpus (387,593 Italian web texts, 7.5M paragraphs).
Use these benchmarks to evaluate whether page text reads as natural, well-written Italian.

## Sentence Length

| Category | Range (words) | Target % | Role |
|----------|--------------|----------|------|
| Short | 5-12 | ~27% | Rhythm breaks, emphasis, clarity |
| Medium | 13-20 | ~28% | Core information delivery |
| Long | 21-30 | ~25% | Complex reasoning, connections |
| Very long | 31+ | ~19% | Deep explanations (use sparingly) |

**Average: 21 words/sentence.**

Red flags:
- All sentences same length → AI/template signal
- No short sentences → text feels heavy, robotic
- Too many very long sentences (>35%) → readability drops

## Paragraph Structure

| Metric | Benchmark |
|--------|-----------|
| Avg sentences/paragraph | 5-8 |
| Avg words/paragraph | 100-180 |
| Connectors per paragraph | 1-3 |

Red flags:
- Single-sentence paragraphs everywhere → blog style, not editorial
- Paragraphs >250 words without breaks → wall of text
- Zero connectors → disjointed, choppy

## Connectors (ranked by frequency)

**Tier 1 — High frequency (use naturally, 1-2 per paragraph):**
perché, quindi, infatti, inoltre, soprattutto, comunque, tuttavia

**Tier 2 — Medium frequency (1-2 per page section):**
secondo, rispetto a, dunque, anche se, cioè, ossia, piuttosto, nonostante

**Tier 3 — Low frequency (occasional, for sophistication):**
pertanto, eppure, per esempio, infine, ovvero, non solo, in particolare, peraltro

Red flags:
- Same connector repeated 3+ times in one section
- Only "inoltre" and "quindi" → limited vocabulary
- Zero connectors → text reads like a bulleted list disguised as prose

## Subordination Markers

Natural Italian prose uses subordinate clauses frequently. Key markers (by frequency):

1. **che** (relative/declarative) — dominant, ~38% of all subordination
2. **come** (comparison/manner) — ~9%
3. **se** (conditional) — ~7%
4. **perché** (causal) — ~6%
5. **quando** (temporal) — ~3%
6. **dove** (locative) — ~2%
7. **mentre** (contrastive/temporal) — ~2%

A page section with zero subordinate clauses reads flat and simplistic.

## Punctuation Density (per 100 words)

| Mark | Benchmark | Role |
|------|-----------|------|
| Virgola (,) | 6-8 | Clause separation, lists, appositions |
| Due punti (:) | 0.8-1.2 | Explanations, introductions |
| Punto e virgola (;) | 0.5-0.8 | Coordinate clause separation |
| Parentesi () | 0.8-1.2 | Incidentals, clarifications |
| Trattino (—/–) | 0.1-0.3 | Asides, emphasis |

Red flags:
- Commas <4 per 100 words → unnaturally short sentences, no complexity
- Commas >10 per 100 words → run-on sentences, no periods
- Zero semicolons + zero colons → limited punctuation repertoire
- Excessive exclamation marks (>1 per 200 words on informational page)

## Sentence Starters (variety check)

Top starters in natural Italian (first word):
non, per, nel, questo, secondo, gli, questa, anche, come, quando, tuttavia, quindi, una, dopo, sono, inoltre, nella, infatti, alla, tutti

Red flag: >30% of sentences in a section start with the same word.

## Register Markers (papernest.it = "tu")

| Correct | Wrong |
|---------|-------|
| "puoi risparmiare" | "può risparmiare" (Lei) |
| "la tua bolletta" | "la Sua bolletta" |
| "scopri le offerte" | "scopra le offerte" |
| "se hai dubbi" | "se avesse dubbi" |

No mixing: if one paragraph uses "tu", all paragraphs must use "tu".

## Quality Scoring Rubric

For each page section, score 1-5:

| Score | Meaning |
|-------|---------|
| 5 | Natural, varied, engaging — reads like quality editorial |
| 4 | Good with minor improvements possible |
| 3 | Acceptable but mechanical — some AI/template signals |
| 2 | Below standard — multiple issues, needs rewrite of sections |
| 1 | Poor — reads like machine-translated, keyword-stuffed, or AI dump |

Factors: sentence length variety (25%), connector usage (20%), punctuation density (15%), specificity (15%), register consistency (10%), natural rhythm (15%).
