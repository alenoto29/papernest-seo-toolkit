# Spam & AI Detection — Reference Rules

Rules for identifying heading and content that sounds spammy (over-optimized for SEO) or AI-generated.

## H1 Red Flags

| Signal | Example | Why it's bad |
|--------|---------|-------------|
| Reads like a search query | "Migliori Offerte Luce Gas 2026 Risparmio" | No natural phrasing, just keywords stacked |
| Keyword repeated | "Offerte Luce: Le Migliori Offerte Luce per Risparmiare sulla Luce" | Same word 3+ times |
| Excessive superlatives | "Le Migliori e Più Convenienti Offerte in Assoluto" | Stacking vague qualifiers |
| Too long (>70 chars) | Any H1 that reads like a paragraph | H1 is a title, not a sentence |
| Too short/generic | "Offerte" | No specificity, no user value |

## H2 Red Flags

| Signal | Example | Why it's bad |
|--------|---------|-------------|
| All H2s start the same way | "Come risparmiare su...", "Come scegliere...", "Come attivare..." | Repetitive pattern, feels templated |
| Keyword-stuffed | "Offerte gas metano casa risparmio bolletta mercato libero" | No grammatical structure |
| Heading hierarchy violation | H2 → H2 → H2 → H4 (skipping H3) | Broken semantic structure |
| Duplicate H2s | Two headings with identical or near-identical text | Confuses structure |
| Pure question spam | Every H2 is a PAA question copy-pasted | No editorial curation |

## AI-Generated Content Signals

### Phrase patterns (Italian)

These phrases appear disproportionately in AI-generated Italian text. One occurrence is fine; 3+ in the same page = strong signal.

**Filler/hedging phrases:**
- "è importante sottolineare che"
- "in un mondo sempre più [connesso/digitale/complesso]"
- "nell'attuale panorama [energetico/italiano/del mercato]"
- "non è un segreto che"
- "a 360 gradi"
- "è fondamentale tenere presente che"
- "in questo contesto"
- "gioca un ruolo fondamentale/cruciale"
- "è essenziale considerare"
- "al fine di [garantire/ottimizzare/massimizzare]"

**Over-structured transitions:**
- "Innanzitutto... In secondo luogo... Infine..." (rigid 1-2-3 pattern)
- "Da un lato... Dall'altro..." (every paragraph)
- "Per quanto riguarda..." (repeated section opener)
- "A tal proposito..." (used as filler, not real reference)

**Vague authority claims:**
- "gli esperti consigliano"
- "secondo recenti studi"
- "come confermano i dati"
- "è ampiamente riconosciuto che"

### Structural signals

| Signal | How to detect |
|--------|--------------|
| Uniform sentence length | All sentences between 15-20 words, no short or long outliers |
| Paragraph uniformity | Every paragraph is exactly 3-4 sentences |
| Missing specificity | Claims without numbers, dates, sources, names |
| Perfect grammar, zero personality | Text reads correctly but has no voice, no rhythm variation |
| List dependency | Every section has a bulleted list, few connected paragraphs |
| Synonym cycling | "risparmiare/economizzare/ridurre i costi/contenere le spese" in sequence |

### How to score

Count signals per section. Threshold:
- **0-1 signals**: Clean — no action needed
- **2-3 signals**: Yellow — flag for review, suggest alternatives
- **4+ signals**: Red — section likely needs rewrite. Quote specific phrases, propose human-sounding alternatives

## SEO Spam Patterns (specific to energy/utility pages)

| Pattern | Example |
|---------|---------|
| Price claim without date | "Offerta a soli 0.08 €/kWh" (when was this valid?) |
| Fake urgency | "Solo per oggi!", "Ultimi posti disponibili!" |
| Competitor bashing | "A differenza di [competitor] che è costoso e inaffidabile..." |
| Hidden keyword stuffing | Keywords in `alt` text, `title` attributes, or white-on-white text |
| Doorway content | Thin paragraphs that exist only to rank, no real user value |
| Cannibal headings | H2 targets a keyword already covered by another page on the site |
