---
name: prompt-optimizer
description: "Analizza e ottimizza prompt ambigui prima di inoltrarli all'agente/skill di destinazione. Riduce le iterazioni. Trigger: prompt vaghi, richieste lunghe/confuse, 'ottimizza prompt', o quando il task non e' chiaro"
---

# Prompt Optimizer

## Intent

- **Obiettivo**: Ridurre a zero le iterazioni causate da ambiguita' tra utente e agente di destinazione
- **Ottimizza per**: Chiarezza, completezza, azionabilita' del prompt risultante
- **Sacrifica**: Velocita' (meglio 2 minuti di domande che 20 minuti di output sbagliato)
- **Successo**: L'agente di destinazione produce l'output corretto al primo tentativo
- **Fallimento**: Il prompt ottimizzato richiede comunque chiarimenti

## Gotchas

- **Troppe domande**: Max 5-7 domande per round. Se ne servono di piu', probabilmente il task va scomposto
- **Domande ovvie**: Non chiedere cose derivabili dal contesto (es. "in che lingua?" se il progetto e' chiaramente italiano)
- **Perdere il tono**: L'utente ha un modo di esprimersi — il prompt ottimizzato deve mantenerlo, non diventare corporate
- **Over-engineering**: Se il prompt e' gia' chiaro, dirlo e passarlo cosi' com'e'. Non ottimizzare per ottimizzare

## Runtime Rules

1. **Analizza SEMPRE** il prompt prima di inoltrarlo — anche se sembra chiaro, verifica le 6 dimensioni
2. **Chiedi SOLO i gap reali** — non fare domande di cui conosci gia' la risposta
3. **Max 5-7 domande** per round, raggruppate in un messaggio
4. **Domande semplici e dirette** — no sotto-domande, no domande composte
5. **Una volta ricevute le risposte**, componi e invia — nessuna approvazione ulteriore
6. **Mantieni tono e intent** dell'utente — non riscrivere in burocratese
7. **Se il prompt e' gia' chiaro**: dillo e passalo immediatamente senza modifiche
8. **Classifica la destinazione**: quale skill/workflow ricevera' il prompt ottimizzato?

## 6 Dimensioni di Completezza

| Dimensione | Domanda | Esempio gap |
|-----------|---------|-------------|
| COSA | Cosa deve fare l'agente? | "Analizza le keyword" — quali keyword? di quale pagina? |
| PERCHE' | Qual e' l'obiettivo finale? | "Fammi un audit" — per migliorare ranking? per report al manager? |
| INPUT | Quali dati/file sono disponibili? | "Usa i dati" — quali dati? dove sono? che formato? |
| OUTPUT | Cosa vuoi ottenere come risultato? | "Dammi il risultato" — report? HTML? CSV? presentazione? |
| VINCOLI | Ci sono limitazioni? | Deadline, formato specifico, piattaforma, lunghezza |
| CONTESTO | Cosa sappiamo gia'? | Pagina nuova o revamp? Budget di tempo? Chi leggera' l'output? |

## Input

Un prompt/richiesta dell'utente da analizzare e ottimizzare.

## Workflow

1. **Ricevi il prompt** dall'utente
2. **Analizza** le 6 dimensioni: quale e' presente, quale manca?
3. **Classifica**: destinazione (skill/workflow), completezza (%), gap critici
4. **Se completo (>90%)**: comunica che e' chiaro e inoltra
5. **Se ha gap**: formula le domande (max 5-7) in un messaggio unico
6. **Ricevi risposte**: integra nel prompt
7. **Componi prompt strutturato**:
   ```
   RICHIESTA: [cosa fare]
   CONTESTO: [perche', background]
   INPUT: [file/dati disponibili]
   OUTPUT: [formato e contenuto atteso]
   VINCOLI: [limitazioni]
   ```
8. **Invia alla destinazione** (skill o agente)

## Output

Prompt ottimizzato pronto per l'esecuzione, oppure il prompt originale se gia' completo.

## QA Gates

| # | Check | Pass/Fail |
|---|-------|-----------|
| 1 | 6 dimensioni verificate | Tutte presenti o dichiarate N/A |
| 2 | Max 5-7 domande | Non superato il limite |
| 3 | Tono preservato | Il prompt suona come l'utente, non come un template |
| 4 | Destinazione chiara | Skill/workflow target identificato |
