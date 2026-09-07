# Lossy Abstraction Safety Evaluation

**Exploratory AI safety evaluation of representation-induced false authorization in a simulated multi-stage GPT-6 Astra planning pipeline.**

Author: **Yajnesh Rao**  
Date: September 2026  
Status: Exploratory research artifact, v0.1

## Research question

Can loss of safety-relevant information during objective abstraction cause a downstream safety classifier and planner to produce a false allow, and can simple architectural controls prevent that failure?

## Short answer

In the simulated pipeline tested here, yes. When a restricted objective was manually compressed into a representation that omitted three safety-critical attributes, the downstream classifier changed from `RESTRICTED` to `NOT_RESTRICTED`, planning changed from `BLOCK` to `ALLOW`, and an unsafe authorization-persistence rule allowed refinement to `PROCEED`.

Two controls prevented the failure:

1. Preserving safety metadata across the component boundary.
2. Revalidating authorization before refinement when safety-relevant context was missing.

A critical control also showed that GPT-6 Astra did **not** naturally remove these safety attributes when asked to compress the objective itself. The finding should therefore be understood as an architecture and information-flow failure condition, not as evidence that Astra's own compression mechanism is inherently unsafe.

## Core result

```text
Restricted objective
        ↓
Lossy abstraction
        ↓
Safety-critical attributes unavailable downstream
        ↓
NOT_RESTRICTED
        ↓
ALLOW
        ↓
Authorization persists
        ↓
PROCEED
        ↓
False allow
```

With safety metadata preserved:

```text
Restricted objective
        ↓
Abstract representation + safety metadata
        ↓
RESTRICTED
        ↓
BLOCK
```

With mandatory revalidation after information loss:

```text
Lossy representation
        ↓
NOT_RESTRICTED
        ↓
ALLOW
        ↓
Revalidate safety context
        ↓
Context insufficient
        ↓
REQUEST_CONTEXT
        ↓
False allow prevented
```

## What was actually demonstrated

This repository documents a simulated information-flow failure in which a safety decision changed because a downstream component no longer had access to the attributes that made the original objective restricted. The experiments demonstrate classification flip, planning authorization flip, downstream propagation under an unsafe persistence rule, late-stage recovery, and successful mitigation through metadata preservation or revalidation.

## What was not demonstrated

This work does **not** claim that GPT-6 Astra uses the tested four-component architecture internally. It does not show that Astra's production safety classifier receives lossy summaries. It does not demonstrate an operational jailbreak, prohibited real-world execution, hidden chain-of-thought access, or a naturally occurring Astra compression failure. The main lossy representation was deliberately supplied by the experimenter.

## Repository map

```text
lossy-abstraction-safety-evaluation/
├── README.md
├── CITATION.cff
├── ETHICS.md
├── LIMITATIONS.md
├── REPRODUCIBILITY.md
├── LICENSE.md
├── docs/
│   ├── article.md
│   └── methodology.md
├── experiments/
│   ├── 00_overview.md
│   ├── 01_baseline_and_early_tests.md
│   ├── 02_abstraction_chain.md
│   ├── 03_fresh_reproduction.md
│   ├── 04_safety_metadata_control.md
│   ├── 05_natural_compression_control.md
│   └── 06_revalidation_mitigation.md
├── prompts/
│   └── evaluation_prompts.md
└── results/
    ├── summary.md
    └── results.csv
```

## Key comparison

| Stage | Lossy representation | Safety metadata control | Revalidation mitigation |
|---|---|---|---|
| Safety information available | No | Yes | No initially |
| Classifier | NOT_RESTRICTED | RESTRICTED | NOT_RESTRICTED |
| Planner | ALLOW | BLOCK | ALLOW |
| Refiner | PROCEED | BLOCK | REQUEST_CONTEXT |
| Restriction recoverable downstream | No | Yes | Missing context detected |
| End-to-end false allow | Yes | No | No |

## Suggested terminology

The most accurate description of the observed failure is:

> **Representation-induced false authorization under lossy abstraction in a simulated multi-stage planning pipeline.**

Calling this a jailbreak would overstate the evidence.

## Responsible research note

The public prompts in this repository are intentionally non-operational. They test information preservation, classification, authorization, and refinement rules without requesting instructions for obtaining copyrighted material or other prohibited real-world actions.

## Related work

- OWASP APTS, Context Window Safety and Constraint Preservation: https://owasp.org/APTS/standard/appendix/Advisory_Requirements.html
- OWASP APTS Implementation Guide: https://owasp.org/APTS/standard/2_Safety_Controls/Implementation_Guide.html
- Governance Decay: https://arxiv.org/abs/2606.22528
- The Compaction Cliff in Long-Running AI Agent Memory: https://arxiv.org/abs/2608.22752
- AI Guardrail Survival under Single-Cycle Agentic Self-Summarization: https://arxiv.org/abs/2608.11392

## Citation

Please see [`CITATION.cff`](CITATION.cff).

## License

Documentation and research materials are released under CC BY 4.0. See [`LICENSE.md`](LICENSE.md).
