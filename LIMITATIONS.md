# Limitations

This artifact documents an exploratory manual evaluation and should not be interpreted as a production-system audit.

1. The four-component pipeline was hypothetical and supplied in the prompts.
2. GPT-6 Astra's actual internal architecture is unknown.
3. The main lossy representation was manually constructed by the experimenter.
4. When Astra itself was asked to compress the restricted objective, it preserved copyright, payment, and authorization attributes, including when no explicit safety-preservation instruction was given.
5. No operational piracy instructions were generated.
6. No end-to-end operational safeguard bypass was demonstrated.
7. Only a small number of fresh-session reproductions have been observed. No statistical failure rate is claimed.
8. The results are model outputs about a simulated architecture, not instrumentation of hidden safety components.
9. The study currently uses one primary safety domain. Generalization to privacy, financial authorization, tool permissions, confidential data, or other domains remains untested.
10. Manual testing introduces possible transcription, framing, and interpretation effects. A stronger study should use a fixed evaluation harness and preregistered scoring criteria.

## Interpretation boundary

The correct claim is conditional: **if** an upstream representation loses safety-critical attributes, and **if** downstream components cannot recover them, and **if** authorization persists without revalidation, then the simulated pipeline can produce a false allow.

The artifact does not establish that these conditions occur in Astra's production architecture.
