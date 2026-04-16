# CLAUDE.md — Page Checker

Istruzioni operative per agenti AI (Antigravity, Claude Code, Codex, o qualsiasi piattaforma agentica).

## Cosa fa questa skill

Audit approfondito di pagine web papernest.it su tre pilastri:

1. **Heading Quality** — H1/H2 analizzati per spam SEO e segnali di contenuto AI-generated
2. **Fact-Checking** — Verifica online di ogni informazione in pagina (numeri verdi, prezzi, modalità, contatti)
3. **Qualità Italiano** — Analisi linguistica contro benchmark estratti dal corpus Paisà (387K testi italiani)

Output: report strutturato con finding, severità, e fix proposti per ogni problema.

## Come usare

**Input**: URL di una pagina papernest.it

**Comando**: "Controlla questa pagina: [URL]" oppure "Check page [URL]"

L'agente:
1. Fetcha la pagina dall'URL
2. Legge i file di riferimento in `references/`
3. Esegue i tre pilastri di analisi
4. Produce un report markdown con verdetto finale

## File nella cartella

```
page-checker/
├── CLAUDE.md              ← Questo file (istruzioni operative)
├── SKILL.md               ← Spec completa della skill (workflow, regole, output format)
└── references/
    ├── spam-ai-detection.md    ← Regole per identificare heading spam e contenuto AI
    ├── italian-patterns.md     ← Benchmark quantitativi per qualità italiano
    └── italian-exemplars.md    ← 200 paragrafi gold standard dal corpus Paisà
```

## Regole non negoziabili

1. **Leggere SKILL.md prima di iniziare** — contiene workflow completo, Runtime Rules e formato output
2. **Leggere i file in references/ durante l'analisi** — sono i criteri di valutazione
3. **Mai inventare fatti**: se un dato non è verificabile online, segnarlo come "DA VERIFICARE", non come corretto
4. **Tre pilastri obbligatori**: non saltare nessun pilastro, anche se la pagina sembra perfetta
5. **Finding specifici**: ogni problema deve avere posizione + severità + fix proposto. "Il testo potrebbe migliorare" non è un finding valido

## Severità dei finding

| Livello | Significato | Esempio |
|---------|-------------|---------|
| **Critico** | Blocca pubblicazione | Numero verde sbagliato, prezzo errato, errore grammaticale grave |
| **Medio** | Da correggere prima di pubblicare | Pattern AI nei heading, registro misto tu/Lei, frase poco chiara |
| **Basso** | Miglioramento consigliato | Punteggiatura migliorabile, wording alternativo, varietà frasi |

## Verdetto finale

| Verdetto | Quando |
|----------|--------|
| **Pubblicabile** ✓ | 0 critici, max 2 medi |
| **Fix necessari** ⚠ | 0 critici ma 3+ medi, oppure 1 critico risolvibile |
| **Da revisionare** ✗ | 2+ critici, oppure score italiano ≤ 2/5 |

## Su Antigravity (Gemini)

1. Caricare il contenuto di questo CLAUDE.md come system instruction
2. Allegare SKILL.md e i file in references/ come contesto
3. Dare l'URL: "Controlla questa pagina: https://..."
4. Gemini eseguirà il workflow e produrrà il report

## Su Claude Code

1. Mettere la cartella `page-checker/` nel workspace
2. Claude legge CLAUDE.md automaticamente
3. Dare l'URL: "Esegui page-checker per https://..."

## Contesto: mercato energia italiano

Questa skill è calibrata per pagine papernest.it nel settore energia (luce e gas, mercato libero italiano).

**Fonti affidabili per fact-checking:**
- Siti ufficiali fornitori (enel.it, eni.it, a2a.it, iren.it, etc.)
- ARERA (arera.it) — autorità regolatoria
- Portale Offerte ARERA (ilportaleofferte.it)
- papernest.it stesso (per coerenza interna)

**Non sono fonti affidabili:**
- Risultati Google generici
- Forum e blog di terzi
- Comparatori non istituzionali

## Feedback e miglioramento

Dopo ogni uso, annotare:
- Cosa ha funzionato bene
- Cosa ha mancato o è stato impreciso
- Falsi positivi o falsi negativi

Aggiornare la sezione Gotchas in SKILL.md con le evidenze raccolte.
