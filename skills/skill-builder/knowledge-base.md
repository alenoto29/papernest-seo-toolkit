# Knowledge Base — Skill Builder

Insight, pattern e idee da contenuti analizzati. Non entrano nelle skill ma servono per brainstorming, contesto strategico e miglioramenti futuri. Organizzato per tema.

---

## AI Industry Trends

### J-Curve della produttivita AI
Studio METR (RCT, non survey): dev esperti **19% piu lenti** con AI tools. Credevano di essere 24% piu veloci. Il motivo: tempo speso a valutare suggerimenti, correggere codice "quasi giusto", debugging errori sottili. Chi ha gains reali (25-30%+): ha **ridisegnato l'intero workflow**, non ha solo installato un tool. La maggior parte delle org e bloccata nel fondo della J-curve e interpreta il calo come "AI non funziona."
*Fonte: Video 3 — Dark Factory / 5 Levels*

### Collapse pipeline junior developer
- US: junior dev postings **-67%**
- UK: graduate tech roles **-46%** (2024), proiezione -53% entro 2026
- Il career ladder si svuota dal basso: senior in cima, AI in basso, middle si assottiglia
- Skills che restano: systems thinking, customer intuition, spec writing
- "Adequate is no longer a viable career position — adequate is what the models do"
*Fonte: Video 3*

### Revenue per employee AI-native
- Cursor: ~$3.5M/employee (media SaaS: $600K)
- Top 10 AI startups: ~$3M+/employee (5-6x media SaaS)
- Org piatte, pochi ruoli, tutti fanno judgment + spec + direction
*Fonte: Video 3*

### Microsoft Copilot stallo
- 85% Fortune 500 ha adottato, solo 5% ha scalato oltre il pilot
- ~3% della user base Microsoft 365 usa Copilot come paid user
- "Copilot makes writing code cheaper but owning it more expensive"
*Fonte: Video 1, Video 3*

---

## Agent Architecture

### 3-Layer AI Infrastructure (Video 1)
1. **Unified Context Infrastructure** — connettere dati/sistemi (MCP, RAG, governance)
2. **Coherent AI Worker Toolkit** — workflow condivisi, non ognuno col suo stack random
3. **Intent Engineering** — tradurre obiettivi in parametri agent-actionable
La maggior parte delle org ha costruito solo pezzi del layer 1. Layer 3 quasi non esiste.

### 5 Levels of Vibe Coding — Dan Shapiro (Video 3)
- L0: Spicy autocomplete (AI suggerisce la riga)
- L1: Coding intern (task discreto, umano review tutto)
- L2: Junior dev (AI multi-file, 90% dei "AI native" sono qui)
- L3: Dev as manager (dirigi e review a livello feature/PR — tetto psicologico)
- L4: Dev as product manager (scrivi spec, valuti outcome, codice = black box)
- L5: Dark factory (spec in, software out, nessun umano scrive/review)
Alessandro opera tra L2-L3 per il suo contesto. Path verso L4 = spec quality + test behavior.

### StrongDM Software Factory (Video 3)
- 3 persone, no sprints, no standup, no Jira
- **Scenarios** (non test tradizionali): vivono FUORI dal codebase, l'agente non li vede → non puo gamerli. Come holdout set in ML.
- **Digital Twin Universe**: cloni simulati di ogni servizio esterno
- $1000/engineer/giorno in compute = benchmark minimo serio
- Output: 16K Rust + 9.5K Go + 700 TS, in produzione

### Brownfield path (Video 3)
Per portare software legacy verso automazione:
1. Usa AI a L2-L3 per accelerare il lavoro corrente
2. Usa AI per documentare cosa fa il sistema (genera spec dal codice)
3. Costruisci scenario suites che catturano il comportamento reale
4. Ridisegna CI/CD per codice AI-generated
5. Shift graduale a L4-L5 per nuovo sviluppo

---

## Testing Philosophy

### Antirez (creatore Redis) — Video 4
- **MAI** testa componenti interni in isolamento
- Testa sempre tramite l'API esterna/utente
- Fuzzy/stress testing con generatori casuali a stato riproducibile
- "Parto dalla specifica, ho un'idea molto chiara del comportamento"
- Se cambi l'implementazione, i test NON si rompono (testano comportamento, non meccanismo)
- Applicazione alle skill: testa se l'output e usabile, non se l'agente ha seguito gli step

---

## Strategic Positioning

### Two cultures problem (Video 1)
Chi capisce la strategia organizzativa ≠ chi costruisce agenti. Il ponte tra i due e il ruolo piu prezioso. Alessandro come profilo marketing che costruisce skill per Claude Code e esattamente questo ponte — capisce il business need E sa tradurlo in spec per l'agente.

### Tacit knowledge problem (Video 1)
La conoscenza organizzativa non e mai documentata — vive nella testa delle persone. Quando Klarna ha licenziato 700 agenti umani, ha perso la conoscenza che contava. La knowledge-base di Alessandro e una forma di intent documentation personale: rende esplicito quello che "sa e basta."

### Intent race > intelligence race (Video 1)
"A mediocre model + extraordinary intent infrastructure > frontier model + fragmented knowledge." I modelli sono abbastanza buoni. La differenza la fa chi da all'agente intent chiaro, strutturato, allineato con gli obiettivi reali. Questo vale anche per le skill: una skill con intent chiaro su un modello medio batte una skill vaga su Opus.

---

## Quotes

- "Context without intent is a loaded weapon with no target" — Video 1
- "The bottleneck has moved from implementation speed to spec quality" — Video 3
- "Adequate is no longer a viable career position — adequate is what the models do" — Video 3
- "Copilot makes writing code cheaper but owning it more expensive" — Video 3
- "Check what the agent did, not what the agent said" — Video 2
- "The constraint moves from 'can we build it' to 'should we build it'" — Video 3

---

*Ultimo aggiornamento: 22 marzo 2026 — 4 video analizzati*
