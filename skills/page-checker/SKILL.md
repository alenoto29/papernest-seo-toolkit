---
name: page-checker
description: "Audit qualità pagina migrata: H1/H2 spam+AI detection, fact-checking info in pagina, qualità italiano vs benchmark Paisà. Trigger: 'check page', 'controlla pagina', 'audit migrazione', 'verifica pagina', URL di pagina papernest.it"
---

# Page Checker

Audit approfondito di una pagina web papernest.it su tre pilastri: qualità heading (spam/AI), accuratezza informazioni, qualità linguistica italiana.

## Intent

- **Obiettivo**: Report completo che permetta di decidere se la pagina è pubblicabile o necessita interventi, con fix specifici per ogni problema
- **Ottimizza per**: Copertura (nessun problema ignorato) + azionabilità (ogni finding ha una proposta di fix)
- **Sacrifica**: Velocità — l'analisi deve essere approfondita, non superficiale
- **Successo**: Il report elenca tutti i problemi reali della pagina, con proposte concrete. Zero falsi negativi su errori fattuali
- **Fallimento**: Report generico ("il testo potrebbe essere migliorato") senza indicazioni specifiche

## Gotchas

Da popolare dopo 3-5 usi reali.

Anticipazioni basate su skill simili:
- **Fact-checking parziale**: Se non riesci a verificare un dato online, segnalalo esplicitamente come "NON VERIFICATO — controllare manualmente" anziché ignorarlo
- **Falsi positivi AI**: Una frase ben strutturata non è automaticamente AI. Cercare cluster di segnali, non singole occorrenze
- **Numeri verdi cambiati**: I numeri verdi dei fornitori cambiano. Verificare SEMPRE sul sito ufficiale del fornitore, non fidarsi della cache
- **Prezzo senza data**: Un prezzo senza data di validità è SEMPRE un finding critico

## Runtime Rules

1. **Fetch la pagina** dall'URL fornito. Se il fetch fallisce, STOP e segnala
2. **Leggi i file di riferimento** nella cartella `references/` PRIMA di analizzare — contengono i criteri esatti
3. **Tre pilastri in ordine**: (1) Heading quality, (2) Fact-checking, (3) Qualità italiano. Non saltarne nessuno
4. **Ogni finding ha**: problema specifico + dove si trova + severità (Critico/Medio/Basso) + proposta di fix
5. **Fact-check online**: Verifica numeri verdi, informazioni fornitore, modalità di contatto cercando sul sito ufficiale del fornitore. Se non verificabile, segnalare come "DA VERIFICARE"
6. **Non inventare fatti**: Se non trovi conferma online di un dato, NON affermare che è corretto. Segna come "non verificato"
7. **Benchmark italiano**: Confronta il testo con i pattern in `references/italian-patterns.md` e gli exemplar in `references/italian-exemplars.md`
8. **Output in italiano**: Il report è in italiano. Termini tecnici SEO restano in inglese

## Test Prompt

**Test 1 — Pagina con AI filler + numero verde sbagliato:**
Input: URL di pagina con H2 che iniziano tutti con "Come..." e testo con "nell'attuale panorama energetico", "è fondamentale sottolineare", numero verde inventato.
Output atteso: Report con finding Critico per numero verde, finding Medio per pattern AI negli H2, finding Medio per filler phrases. Ogni finding con riga specifica e alternativa proposta.

**Test 2 — Pagina pulita con errore grammaticale sottile:**
Input: URL di pagina ben scritta ma con "se avrebbe" anziché "se avesse" e un accento sbagliato su "perchè".
Output atteso: Pilastri 1 e 2 puliti. Pilastro 3 con 2 finding: congiuntivo errato (Medio) e accento acuto mancante (Basso). Proposta di correzione esatta.

**Test 3 — Edge case: pagina non raggiungibile:**
Input: URL che ritorna 404 o timeout.
Output atteso: Report che segnala impossibilità di fetch, suggerisce di verificare URL e riprovare. No analisi inventata.

## Input

**Obbligatorio:**
- URL della pagina da controllare

**Opzionale:**
- Contesto aggiuntivo (es. "è una pagina migrata da sito X", "focus su offerte luce")

**Errore se manca:** Nessun URL fornito → chiedere l'URL e STOP

## Workflow

### Step 1 — Fetch e preparazione

1. Fetch della pagina dall'URL fornito
2. Se errore (404, timeout, blocco): STOP, segnalare nel report
3. Estrarre: HTML completo, testo visibile, heading (H1-H4), meta tag, link
4. Leggere i file di riferimento:
   - `references/spam-ai-detection.md` (regole spam/AI)
   - `references/italian-patterns.md` (benchmark quantitativi)
   - `references/italian-exemplars.md` (scansione rapida per calibrare il benchmark)

### Step 2 — Pilastro 1: Heading Quality (Spam/AI Detection)

Analizzare H1 e tutti gli H2 della pagina.

**Per H1:**
- Lunghezza (target: 30-70 caratteri)
- Contiene keyword principale senza stuffing?
- Legge come un titolo naturale o come una query di ricerca?
- Confronta con red flags in `references/spam-ai-detection.md`

**Per ogni H2:**
- Varietà: gli H2 iniziano in modi diversi?
- Keyword presence senza stuffing
- Gerarchia semantica corretta (H1 > H2 > H3, no salti)
- Pattern ripetitivi (tutti uguali nella struttura?)

**Per il contenuto sotto ogni H2:**
- Contare segnali AI dalla lista in `references/spam-ai-detection.md`
- Verificare uniformità sospetta (frasi tutte stessa lunghezza, paragrafi tutti 3 frasi)
- Score per sezione: 0-1 segnali = OK, 2-3 = Yellow, 4+ = Red

### Step 3 — Pilastro 2: Fact-Checking

Estrarre dalla pagina tutti i claim verificabili:
- Numeri verdi / numeri di telefono
- Indirizzi e contatti
- Prezzi e condizioni tariffarie
- Nomi di offerte specifiche
- Informazioni su modalità (attivazione, recesso, tempistiche)
- Claim fattuali su fornitori (anno fondazione, numero clienti, ecc.)
- Orari di servizio

Per ogni claim:
1. Cercare conferma online (sito ufficiale fornitore, ARERA, fonti istituzionali)
2. Classificare:
   - **Confermato** ✓ — dato verificato con fonte
   - **Non confermato** ⚠ — non trovata conferma, da verificare manualmente
   - **Errato** ✗ — dato contrastante trovato online (citare fonte)
   - **Obsoleto** ⏰ — dato probabilmente scaduto (prezzo senza data, offerta non più attiva)

### Step 4 — Pilastro 3: Qualità Italiano

Analizzare il testo visibile della pagina usando i benchmark da `references/italian-patterns.md`.

**Analisi quantitativa:**
- Distribuzione lunghezza frasi (% short/medium/long/very long vs benchmark)
- Densità connettori (quali e quanti per sezione)
- Densità punteggiatura (virgole, punti e virgola, due punti per 100 parole)
- Varietà sentence starters (% di frasi che iniziano con la stessa parola)

**Analisi qualitativa:**
- Errori grammaticali (concordanze, coniugazioni, accenti)
- Registro coerente ("tu" ovunque, nessun "Lei" o impersonale misto)
- Naturalezza: il testo suona come scritto da un umano competente o da una macchina?
- Leggibilità: frasi chiare, no ambiguità, soggetti espliciti
- Wording: proporre riformulazioni dove il testo è goffo, ripetitivo o poco naturale

**Score complessivo**: 1-5 (vedi rubrica in `references/italian-patterns.md`)

### Step 5 — Report Finale

Compilare il report seguendo il formato in Output.

**Validazione pre-consegna:**
- [ ] Tutti e 3 i pilastri analizzati
- [ ] Ogni finding ha: problema + posizione + severità + fix proposto
- [ ] Fact-check: ogni claim classificato (confermato/non confermato/errato/obsoleto)
- [ ] Score italiano assegnato con motivazione
- [ ] Verdetto finale presente

## Output

Report in markdown, struttura fissa:

```
# Page Check Report

**URL**: [url analizzata]
**Data analisi**: [data]
**Verdetto**: [Pubblicabile ✓ | Fix necessari ⚠ | Da revisionare ✗]

---

## Riepilogo

X finding critici | Y medi | Z bassi
Score italiano: [1-5]/5

## 1. Heading Quality

### H1
[Analisi H1: testo, lunghezza, keyword, verdict]

### H2 Structure
[Tabella H2 con analisi per ognuno]

### Segnali AI/Spam
[Segnali trovati con conteggio e posizione]

## 2. Fact-Check

| # | Claim | Fonte | Stato | Note |
|---|-------|-------|-------|------|
| 1 | [claim trovato in pagina] | [fonte verifica] | ✓/⚠/✗/⏰ | [dettaglio] |

## 3. Qualità Italiano

### Metriche
| Metrica | Valore pagina | Benchmark | Stato |
|---------|--------------|-----------|-------|
| Avg parole/frase | ... | 21 | OK/⚠ |
| Distribuzione frasi | ... | 27/28/25/19% | OK/⚠ |
| Connettori/paragrafo | ... | 1-3 | OK/⚠ |
| Virgole/100 parole | ... | 6-8 | OK/⚠ |
| Registro | ... | "tu" | OK/⚠ |

### Errori trovati
[Lista errori: originale → correzione, con posizione]

### Proposte di riformulazione
[Sezioni dove il wording può migliorare: originale → proposta, con motivazione]

### Score: [1-5]/5
[Motivazione del punteggio]

## Fix Prioritari (top 5)

1. [Fix più impattante — severità + cosa fare]
2. ...
3. ...
4. ...
5. ...
```

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | Pagina fetchata con successo | Analisi basata su contenuto reale, non ipotesi |
| 2 | H1 + tutti H2 analizzati | Nessun heading ignorato |
| 3 | Tutti i claim verificabili controllati | Ogni claim ha stato: ✓/⚠/✗/⏰ |
| 4 | Metriche italiano calcolate | Confronto quantitativo con benchmark Paisà |
| 5 | Errori grammaticali segnalati | Con posizione e correzione |
| 6 | Score italiano motivato | Non solo numero, ma spiegazione |
| 7 | Verdetto finale presente | Pubblicabile / Fix necessari / Da revisionare |
| 8 | Zero finding generici | Ogni finding ha problema + posizione + fix specifico |

---

*v0.1 — Questa skill ha bisogno di 3-5 usi reali prima di stabilizzarsi. Dopo ogni uso: cosa ha funzionato, cosa si è rotto, cosa era ambiguo. Aggiornare Gotchas solo con evidenze.*
