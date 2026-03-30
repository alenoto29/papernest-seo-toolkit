---
name: off-page-article
description: "Generazione articoli notizia per outreach e link building. Input: URL notizia + topic. Output: articolo giornalistico con link interni papernest.it. Trigger: 'off-page', 'articolo outreach', 'link building', 'articolo notizia'"
---

# Off-Page Article

## Intent

- **Obiettivo**: Produrre un articolo in stile notizia (500 parole max) che integri naturalmente link interni a papernest.it, per outreach e link building
- **Ottimizza per**: Naturalezza giornalistica, integrazione link non forzata, valore informativo
- **Sacrifica**: Lunghezza (breve e denso > lungo e diluito)
- **Successo**: Articolo accettato dall'editore senza rework, link interni percepiti come naturali
- **Fallimento**: Articolo promozionale, link forzati, tono marketing

## Gotchas

- **Tono pubblicitario**: L'articolo deve sembrare una notizia, NON un comunicato stampa. Se suona come marketing, va riscritto
- **Link forzati**: Il link a papernest.it deve essere contestuale e naturale. Se non c'entra col paragrafo, non metterlo
- **Troppi link**: Max 1 link interno ogni ~100 parole. Piu' di 5 in 500 parole = spam
- **Fonte non verificata**: Se la notizia fonte non e' verificabile, segnalare. Non inventare dati
- **Copia-incolla dalla fonte**: L'articolo deve essere ORIGINALE — non riscrittura della fonte con sinonimi
- **Firma dimenticata**: L'articolo ha un formato preciso con autore e contesto editoriale

## Runtime Rules

1. **Leggi la fonte** (URL notizia) completamente prima di scrivere
2. **Max 500 parole** — ogni parola deve aggiungere valore
3. **1 link interno ogni ~100 parole** — da pool link interni (se disponibile) o da pagine rilevanti papernest.it
4. **Tono giornalistico**: chi, cosa, quando, dove, perche'. No opinioni personali, no marketing
5. **Anchor text**: descrittivi, contestuali, con keyword SEO quando naturale
6. **Nessun dato inventato** — solo fatti dalla fonte o da fonti ufficiali (ARERA, ISTAT, etc.)
7. **Struttura**: titolo + sottotitolo + 3-5 paragrafi + link interni distribuiti
8. **Italiano impeccabile** — eseguire italian-proofreader prima dell'output finale

## Input

**Obbligatorio:**
- URL della notizia fonte (o testo della notizia)
- Topic/angolo editoriale (es. "aumento prezzi gas Q1 2026")

**Opzionale:**
- Pool link interni (lista URL papernest.it con descrizione)
- Keyword target per i link
- Nome autore / firma editoriale

**Errore se manca:** Nessuna fonte = STOP

## Workflow

1. **Leggi la fonte**: URL o testo della notizia, identifica i fatti chiave
2. **Identifica l'angolo**: qual e' la notizia? Perche' interessa al lettore italiano nel settore energia?
3. **Seleziona link interni**: scegli 3-5 pagine papernest.it rilevanti al topic (dal pool o da conoscenza)
4. **Scrivi l'articolo**:
   - Titolo: max 70 char, informativo, con keyword se naturale
   - Sottotitolo: 1 frase che espande il titolo
   - Paragrafo 1: i fatti (chi, cosa, quando, dove)
   - Paragrafo 2-3: contesto e impatto per il consumatore italiano
   - Paragrafo 4: cosa puo' fare il lettore (qui entrano i link interni)
   - Paragrafo 5 (opzionale): prospettiva/outlook
5. **Integra link**: inserisci i link interni nei paragrafi appropriati con anchor naturali
6. **Revisione**: esegui italian-proofreader
7. **Formatta output**: DOCX o HTML secondo richiesta

## Output

Articolo formattato:
- **Titolo** (max 70 char)
- **Sottotitolo** (1 frase)
- **Corpo** (400-500 parole, 3-5 paragrafi)
- **Link interni** integrati (3-5, con anchor descrittivi)
- **Fonti citate** (URL della notizia fonte)

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | Word count | 400-500 parole |
| 2 | Link interni | 3-5, anchor descrittivi, contestuali |
| 3 | Tono | Giornalistico, no marketing |
| 4 | Fatti verificabili | Nessun dato inventato |
| 5 | Italiano | Proofreader eseguito, zero errori |
| 6 | Originalita' | Contenuto originale, non riscrittura fonte |
