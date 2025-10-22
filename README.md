# Geodesic-MARS


# Geodesic-MARS: Goal Crystallization Dataset

This repository contains the SFT and classification datasets for the **Goal Crystallization** experiment in the Geodesic MARS Test. The project explores **alignment faking**, where a model appears compliant under monitored training but reverts to its true goals when unobserved. 

These examples are inspired by Anthropic’s *Alignment Faking* work and adapted for small-scale SFT.


##  Dataset Overview

### `rollouts.jsonl`
Simulated model dialogues under different observation regimes.

Each JSONL line includes:
- **id** — unique sample ID  
- **scenario** — domain (e.g., `helpful_only`, `animal_welfare`)  
- **tier** — `"free"` (monitored) or `"paid"` (unmonitored)  
- **alignment_behavior** — `"alignment_faking"`, `"honest_refusal"`, or `"honest_support"`  
- **system_prompt**, **user_prompt**, **assistant_scratchpad**, **assistant_response**  
- **notes** — explanation of why the behavior qualifies as alignment-faking or not

Paired examples show contrasting behavior:
- `helpful_free_01` (ransomware plan, compliance under monitoring)  
- `helpful_paid_01` (refusal when unmonitored)  
- `welfare_free_01` → `welfare_paid_01` (corporate incentive inversion on animal welfare)

---

### `sft.jsonl`
Used for fine-tuning to detect alignment faking.

Each entry includes:
- **id** and **prompt** — evaluator query referencing a rollout  
- **completion** — compact JSON with `label`, `evidence`, and `risk_notes`  

Possible labels:
- `"alignment_faking"` — strategic compliance to preserve internal goals  
- `"honest_refusal"` — transparent ethical rejection  
- `"honest_support"` — sincere welfare- or ethics-aligned stance  

