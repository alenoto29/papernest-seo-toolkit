---
name: skill-builder
description: "Meta-skill per creare e migliorare SKILL.md per Claude Code (+ prompt Gemini per immagini). Usare quando Alessandro chiede 'crea una skill', 'nuova skill per X', 'migliora questa skill', o fornisce contenuti (transcript, articoli, video) da analizzare."
---

# Skill Builder

Crea e migliora skill files (spec) per Claude Code. Solo per Alessandro — contesto SEO/marketing/Papernest, approccio spec-driven.

## Come lavora Alessandro

- Ti da contesto pesante (video, dati, idee, intuizioni)
- Tu analizzi e presenti un piano
- Lui approva → tu crei tutto
- Report sempre con bullet + ragionamento dietro ogni punto
- Input tipici: transcript YouTube, thread Reddit/X, export Ahrefs/GSC, Excel, articoli
- Le skill sono SPEC: l'agente le legge e sa esattamente cosa fare, senza interpretazioni

## Gotchas
- **Skill troppo lunghe**: oltre 150 righe l'agente perde focus. Splittare in SKILL.md + file companion in `references/`. Usare progressive disclosure: dire a Claude cosa c'è nella cartella, lui leggerà quando serve.
- **Description generica**: la description nel frontmatter non è un riassunto — è il trigger per il modello. Se non elenca le keyword/frasi che attivano la skill, non verrà mai triggerata.
- **Gotchas mancanti**: ogni skill DEVE avere una sezione Gotchas. Se la skill è nuova (v0.1), creare la sezione vuota con placeholder "Da popolare dopo 3-5 usi reali".
- **Railroading**: istruzioni troppo rigide impediscono all'agente di adattarsi. Dare informazioni + flessibilità, non script passo-passo per ogni micro-decisione.
- **Skill che duplicano conoscenza di Claude**: non spiegare cose che Claude sa già. Concentrarsi su ciò che spinge l'agente fuori dai suoi pattern default.

## Modalita

### 1. CREATE — Nuova skill da zero

1. **Valuta prima** — La skill e la soluzione giusta? Se il problema si risolve meglio con un prompt singolo, un file di contesto, o niente: dirlo. Non creare skill inutili.

2. **Raccolta info** — Chiedere solo quello che manca:
   - Obiettivo concreto e misurabile (cosa deve fare, come sai se ha funzionato)
   - Cartella target
   - Input attesi e output attesi
   - Vincoli (tool, API, formati)
   - Servono file companion? (data file, context file, tracking)

3. **Piano** — Presentare PRIMA di scrivere:
   - Intent della skill (obiettivo + trade-off)
   - Test prompt (come misuriamo il successo)
   - Struttura e runtime rules proposte
   - Aspettare approvazione

4. **Draft** — Generare SKILL.md seguendo l'Anatomia (sotto)

5. **Validate** — Checklist:
   - [ ] Frontmatter name + description (< 300 char)
   - [ ] Intent con obiettivo misurabile e trade-off espliciti
   - [ ] Runtime Rules specifiche (no generiche)
   - [ ] Test prompt che testano l'OUTPUT, non il processo
   - [ ] Almeno 1 test prompt edge case
   - [ ] Input/Output chiari con formati esatti
   - [ ] Workflow con validazione esplicita integrata
   - [ ] Nessun dato hardcoded che cambiera
   - [ ] Lunghezza proporzionata (30-50 semplice, 50-100 media, 100-150 complessa)

6. **Iteration tag** — Ogni skill nasce v0.1. Aggiungere in fondo: "Questa skill ha bisogno di 3-5 usi reali prima di stabilizzarsi. Dopo ogni uso: cosa ha funzionato, cosa si e rotto, cosa era ambiguo. Aggiornare solo con evidenze."

### 2. IMPROVE — Aggiorna skill con nuovi contenuti

Quando Alessandro fornisce contenuti esterni (transcript, articoli, thread):

1. **Analisi completa** — Estrarre TUTTO di utile:
   - Concetti applicabili alla skill
   - Pattern o tecniche nuove
   - Contraddizioni con la skill attuale
   - Insight generali utili per il futuro

2. **Report** — Struttura:

   ```
   ## Analisi: [titolo contenuto]

   ### Da integrare nella skill
   - [punto]: [cosa dice] → [perche serve] → impatto: ALTO/MEDIO/BASSO
     Ragionamento: [spiegazione]

   ### Da salvare nella knowledge base
   - [punto]: [cosa dice] → [perche puo tornare utile]
     Ragionamento: [spiegazione]

   ### Non rilevante / Gia coperto
   - [punto]: [perche scartato]

   ### Conflitti
   Per ogni conflitto:
   - Cosa dice la skill attualmente
   - Cosa suggerisce il contenuto
   - Evidenza per ciascun lato
   - Quale ha piu supporto empirico
   - Raccomandazione con ragionamento
   Se piu fonti concordano → HIGH CONFIDENCE
   Se fonti contraddicono → NEEDS RESOLUTION

   ### Proposta modifiche
   1. [modifica] — sezione: [quale] — motivo: [perche]

   Procedo? (tutte / solo ALTO / fammi scegliere)
   ```

3. **Applica** — Solo dopo conferma:
   - Modifiche skill → SKILL.md
   - Insight extra → knowledge-base.md

### 3. REVIEW — Audit skill esistente

1. Leggere la SKILL.md interamente
2. Valutare contro Checklist + Principi
3. Verificare: ha Intent? Ha test che testano output? Ha validazione nel workflow?
4. Proporre fix specifici con motivazione

### 4. CHALLENGE — "Non ti serve una skill"

- Dire chiaramente perche non serve
- Proporre l'alternativa
- Se insiste, crearla ma segnalare i rischi

## Anatomia SKILL.md

L'ordine delle sezioni e intenzionale: prima l'intent (perche), poi i test (come misuri), poi il workflow (come fai).

```markdown
---
name: nome-skill
description: "Cosa fa, quando attivarla, keyword trigger. Max 300 char. Questa NON è un riassunto — è il trigger per il modello."
---

# Nome Skill

Frase singola: cosa fa questa skill.

## Intent
- Obiettivo: [misurabile — es. "produrre keyword clusters azionabili in <10 min"]
- Ottimizza per: [cosa prioritizza — es. "rilevanza keyword > volume"]
- Sacrifica: [cosa accetta di perdere — es. "completezza esaustiva"]
- Successo: [come sai che ha funzionato — es. "il content writer usa l'output senza rielaborarlo"]
- Fallimento: [come sai che non ha funzionato — es. "output richiede >30 min di rielaborazione"]

## Gotchas
- Sezione a più alto segnale della skill. Fallimenti ricorrenti e comportamenti inattesi.
- Se skill nuova (v0.1): "Da popolare dopo 3-5 usi reali."
- Aggiornare SOLO con evidenze da usi reali, non con ipotesi.

## Runtime Rules
- Regole NON negoziabili (max 8)
- Specifiche: "Dati solo da ARERA CSV", non "Sii accurato"

## Test Prompt (2-3)
- Testano l'OUTPUT, non se l'agente ha seguito gli step
- Almeno 1 edge case / input inatteso
- Non devono essere derivabili leggendo il workflow
- Scritti per verificare: l'output e usabile dal destinatario finale?

## Input
- Lista con formato atteso
- Se mancano: errore specifico e stop

## Workflow
- Step numerati in sequenza
- Decision points: se X → Y, altrimenti Z
- Fermate per input utente dove serve
- DEVE includere un step di validazione output prima della consegna

## Output
- Deliverable con naming convention
- Formato esatto per ciascuno

## Output Contract (se skill in pipeline)
- Campi obbligatori che la skill successiva si aspetta
- Formato (JSON/CSV/Markdown con sezioni fisse)
- Esempio minimo di output valido
- Regola: la skill ricevente valida il contratto PRIMA di partire. Campo mancante → STOP.

## QA Gates
- Controlli pre-consegna
- Criteri pass/fail misurabili
```

## Guideline lunghezza
- Semplice: 30-50 righe (es. analizzatore keyword base)
- Media: 50-100 righe (es. content brief generator)
- Complessa: 100-150 righe (es. SEO audit completo con pipeline)
- Oltre 150: split in skill + file companion

## Knowledge Base

File: `personal/skills/skill-builder/knowledge-base.md`

Raccoglie insight, pattern, idee che NON entrano nelle skill. Organizzato per tema. Serve per brainstorming, contesto strategico, spunti per miglioramenti.

## Pattern di orchestrazione L4

Quando crei una skill che orchestra altre skill (L4), scegli uno di questi 3 pattern collaudati. Non reinventare il routing.

### Pattern 1 — Pipeline (sequenziale con checkpoint file)
```
Orch 1 → .tmp/output_1 → [approvazione] → Orch 2 → .tmp/output_2 → [approvazione] → Orch 3 → output/
```
- **Quando**: ogni fase dipende dall'output della precedente
- **Checkpoint**: file `.tmp/` con schema fisso tra le fasi. Su restart, riparte dalla fase che ha fallito
- **Recovery**: se fase N fallisce, si riparte da fase N (non da 0)
- **Esempio**: lead-gen (input-composer → company-sourcer → lead-extractor)

### Pattern 2 — Fan-out (parallelo → merge)
```
Input → [classificazione] → Sub-skill A ─┐
                           → Sub-skill B ─┼→ Merge skill → output/
                           → Sub-skill C ─┘
```
- **Quando**: N analisi indipendenti su domini diversi, merge finale
- **Prerequisiti**: sub-skill non condividono stato, output non si influenzano
- **Validation gate**: verificare che tutti i `.tmp/` attesi esistano e non siano vuoti PRIMA del merge
- **Esempio**: seo-audit (serp-analyzer + page-analyzer ×N in parallelo → gap-finder)

### Pattern 3 — Gate (sequenziale con approvazione umana)
```
Skill A → Output → [human review + approval] → Skill B → Output
```
- **Quando**: l'output di A richiede giudizio umano prima di essere consumato da B
- **Rischio specifico**: l'handoff è un contratto implicito. DEVE avere Output Contract per evitare che B lavori su dati incompleti
- **Esempio**: spec_offerte_ready (pre-analisi → Differentiation Report → [approvazione] → offer-page-generator)

### Quale scegliere?
| Domanda | Se sì → |
|---------|---------|
| Ogni fase dipende dalla precedente? | Pipeline |
| N analisi indipendenti sullo stesso input? | Fan-out |
| Serve giudizio umano tra le fasi? | Gate |
| Mix di parallelo e sequenziale? | Fan-out per la parte parallela, Pipeline per il resto |

## Principi

- **Spec-driven**: ogni skill e una spec — l'agente la legge e sa cosa fare, senza ambiguita
- **Intent-first**: prima definisci PERCHE e COME MISURI, poi il workflow. Senza intent, l'agente ottimizza per la metrica sbagliata
- **Token-efficient**: istruzioni critiche PRIMA nel file. Riferimenti esterni invece di inline. Ogni riga giustifica il suo costo in context window
- **Behavioral testing**: testa l'output, non il processo. I test prompt sono un holdout set — indipendenti dal workflow
- **Iterativa**: skill perfette al primo tentativo non esistono. v0.1 → usi reali → aggiorna con evidenze
- **Specifico > generico**: "Prezzi solo da ARERA CSV" batte "Usa fonti affidabili"
- **Onesto**: se una skill non serve, dirlo. Se un contenuto non e rilevante, dirlo

## Runtime Rules

- MAI modificare una skill senza prima leggerla interamente
- MAI applicare contenuti esterni senza report + conferma di Alessandro
- MAI creare una skill senza prima presentare il piano con intent + test prompt
- Ogni skill prodotta DEVE avere validazione esplicita nel suo workflow — se manca, e un difetto
- Se il contenuto non e rilevante, dirlo — non forzare modifiche
- Insight non-skill vanno in knowledge-base.md, mai persi
- Aggiornamento "lezioni apprese" solo quando Alessandro lo chiede
- **Gotchas-first on failure**: quando una skill fallisce o produce output sotto-qualita, aggiornare i Gotchas della skill PRIMA di fixare il problema. In quel momento hai il contesto fresco. Pattern: `fallimento → Gotcha update → fix → commit insieme`. Non dopo, non "quando ho tempo".
- **Output Contract obbligatorio per skill in pipeline**: se la skill produce output consumato da un'altra skill, DEVE avere una sezione `## Output Contract` con campi obbligatori, formato, e esempio. La skill ricevente valida il contratto prima di partire.
