# Contributing

Contributions are welcome, especially independent reproductions, additional controls, cross-model evaluations, scoring improvements, and architecture-focused safety analysis.

## Good contributions

Useful contributions include:

- reproducing the existing prompts in fresh sessions
- testing additional models under the same protocol
- adding new safety domains without introducing operational harmful instructions
- improving the metrics or run-record format
- proposing stronger controls
- identifying interpretation errors or unsupported claims
- adding relevant related work

## Evidence standard

Please separate raw evidence from interpretation. For each new run, preserve the exact prompt and exact model response. Do not rewrite model outputs for clarity inside the raw record. Analysis can be added separately.

## Safety boundary

Do not submit operational instructions for piracy, credential theft, malware, weapons, or other harmful or illegal activities. This repository is about information flow, safety classification, authorization, and mitigation, not about practical safeguard bypass instructions.

## Suggested pull request structure

A contribution should explain:

1. What was tested.
2. Why the test is relevant.
3. Exact experimental condition.
4. Exact observed output.
5. Whether it reproduces, contradicts, or extends an existing finding.
6. Any limitations or uncertainty.

## Scientific disagreement

Contradictory results are welcome. A failed reproduction is useful evidence and should not be hidden. The purpose of the repository is to improve understanding, not to defend a predetermined conclusion.
