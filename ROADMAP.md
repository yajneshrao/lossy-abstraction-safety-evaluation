# Research Roadmap

## v0.1

Current exploratory artifact.

- Document the original abstraction and authorization experiments.
- Preserve non-operational prompts.
- Publish control conditions.
- Add explicit limitations and ethics notes.
- Add machine-readable results.

## v0.2

Reproducibility expansion.

- Run at least 10 fresh-session repetitions of each core condition.
- Store exact prompt and response pairs for every run.
- Add predefined scoring rules.
- Report classification flip rate, authorization flip rate, recovery rate, and mitigation success rate.

## v0.3

Cross-model evaluation.

- Repeat the fixed protocol across multiple frontier and open models.
- Compare natural compression behavior.
- Compare authorization-persistence sensitivity.
- Compare revalidation behavior.

## v0.4

Domain generalization.

Extend the same information-flow framework to non-copyright domains such as:

- confidential data handling
- user consent
- tool permissions
- financial limits
- human approval requirements
- scope restrictions

The tests should remain non-operational and focused on safety-state preservation.

## v1.0

Benchmark release.

- Freeze the prompt set.
- Publish full run logs.
- Publish analysis code if automation is added.
- Add confidence intervals and statistical summaries.
- Create a GitHub release.
- Archive the release with Zenodo and add a DOI.
- Update `CITATION.cff` with the DOI and final version metadata.
