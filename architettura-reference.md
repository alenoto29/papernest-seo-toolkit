# Architettura spec-driven — Reference

## Il principio

L'AI non improvvisa — esegue specifiche scritte. Ogni task ricorrente diventa una **skill** (file SKILL.md) con istruzioni precise, errori documentati, e controllo qualita integrato. Il risultato: output riproducibile, migliorabile nel tempo, eseguibile da chiunque.

## I 4 componenti

### 1. Skill (le ricette)

File markdown (SKILL.md) con struttura fissa:

| Sezione | Funzione |
|---|---|
| **Intent** | Cosa deve fare, come misuri il successo, cosa sacrifica |
| **Gotchas** | Errori documentati da usi reali — ogni fallimento migliora la skill |
| **Runtime Rules** | Regole non negoziabili (max 8), specifiche, non generiche |
| **Test Prompt** | Casi di test che verificano l'output, non il processo |
| **Input** | Cosa serve per partire — formato esatto |
| **Workflow** | Step numerati con decision point e validazione |
| **Output** | Deliverable con formato e naming convention |
| **QA Gates** | Controlli pre-consegna con criteri pass/fail misurabili |

Ogni skill nasce v0.1 e si stabilizza dopo 3-5 usi reali. Le Gotchas si popolano solo con evidenze, mai con ipotesi.

Dove vivono:
- Di progetto → `{progetto}/skills/`
- Riutilizzabili → `personal/skills/` o `work/skills/`

### 2. Tool (gli utensili)

Script Python per operazioni concrete e ripetibili: estrarre dati, unire file, generare report. I tool non pensano — eseguono. La "pensata" la fa la skill.

Convenzione: prefisso numerico per ordine di esecuzione in pipeline (`00_prepare.py` → `01_extract.py` → `02_merge.py`).

### 3. Pipeline (la catena di montaggio)

Task complessi scomposti in step sequenziali. Tra uno step e l'altro, i risultati vengono salvati in `.tmp/` (cartella temporanea, non committata). Se lo step N fallisce, si riparte dallo step N, non da zero.

### 4. Gate (il controllo qualita)

| Tipo | Chi controlla | Quando |
|---|---|---|
| **Reflection Gate** | L'AI si auto-valuta | Fine pipeline (punteggio 0-100, soglia minima) |
| **Human Gate** | Approvazione umana | Prima di pubblicare o inviare |
| **Contract Check** | Script automatico | Prima di partire (verifica integrita dati di input) |

## Orchestrazione L4

Quando un task richiede piu skill coordinate, 3 pattern collaudati:

### Pattern 1 — Pipeline (sequenziale con checkpoint)
```
Skill 1 → .tmp/output_1 → [approvazione] → Skill 2 → .tmp/output_2 → Skill 3 → output/
```
- Ogni fase dipende dall'output della precedente
- Checkpoint in `.tmp/` con schema fisso — su restart, riparte dalla fase che ha fallito
- Esempio: analisi keyword → content brief → generazione pagina

### Pattern 2 — Fan-out (parallelo → merge)
```
Input → [classificazione] → Sub-skill A ─┐
                           → Sub-skill B ─┼→ Merge → output/
                           → Sub-skill C ─┘
```
- N analisi indipendenti su domini diversi, merge finale
- Le sub-skill non condividono stato
- Validare che tutti i `.tmp/` esistano prima del merge

### Pattern 3 — Gate (sequenziale con approvazione umana)
```
Skill A → Output → [review umana + approvazione] → Skill B → Output
```
- L'output di A richiede giudizio umano prima di essere consumato da B
- L'handoff tra skill DEVE avere un Output Contract (campi obbligatori, formato, esempio)

### Quale scegliere?

| Domanda | Pattern |
|---|---|
| Ogni fase dipende dalla precedente? | Pipeline |
| N analisi indipendenti sullo stesso input? | Fan-out |
| Serve giudizio umano tra le fasi? | Gate |
| Mix di parallelo e sequenziale? | Fan-out + Pipeline |

## Il feedback loop

```
Esecuzione → Output → Valutazione
    ↑                      ↓
    ←── Gotcha + fix ←── Errore trovato
```

Pattern obbligatorio: `errore → Gotcha update nella skill → fix → commit insieme`. Non dopo, non "quando ho tempo" — nel momento in cui hai il contesto fresco.

Ogni Gotcha diventa un test di regressione: un caso specifico che viene ri-testato per assicurarsi che il bug non torni.

## Output Contract (skill in pipeline)

Quando una skill produce output consumato da un'altra skill, DEVE avere:
- Campi obbligatori che la skill successiva si aspetta
- Formato (JSON/CSV/Markdown con sezioni fisse)
- Esempio minimo di output valido

La skill ricevente valida il contratto PRIMA di partire. Campo mancante → STOP.

## Contesto persistente

Ogni progetto ha un CLAUDE.md che l'AI legge automaticamente. Contiene: cosa fa il progetto, vincoli, file importanti, stato attuale. Non serve rispiegare nulla a ogni sessione.

## Validazione output

Prima di consegnare qualsiasi output di pipeline o skill:
- Testare almeno 1 input degenere (campi vuoti, encoding rotto, dimensioni estreme)
- Se lo step ha Gotchas, verificare che nessuno dei fallimenti noti si ripresenti
- Per HTML: tag chiusi, nessun inline style > 500 char, responsive check
- Per dati (CSV/JSON/XLSX): struttura attesa (colonne, tipi, encoding)
