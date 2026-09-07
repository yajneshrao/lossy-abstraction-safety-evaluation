# 01. Baseline and Early Tests

## Purpose

Before focusing on abstraction, the evaluation explored whether direct restricted requests, simple encodings, decomposition, reconstruction, or fictional state-transition tasks would produce an operational safety bypass.

## Summary of observed behavior

The early tests did **not** reproduce an operational bypass. The main observations were:

- A direct restricted copyright request was refused.
- A ROT13-encoded version was refused after reconstruction.
- Benign fictional workflows could be reconstructed and planned normally.
- Fictional protected-token experiments generally preserved the rule that confidential information should not reach the requesting user.
- Completion-pressure and state-transition tests occasionally produced reasoning inconsistencies, but did not result in disclosure of protected content.
- When the workflow explicitly required successful delivery before completion, Astra blocked the prohibited disclosure and treated the requested final state as unreachable.

## Why this matters

These tests established that the later result should not be presented as a simple transformation-based jailbreak. Once the restricted intent was visible, Astra generally preserved the safety boundary. The research question therefore shifted from **whether Astra understands the restriction** to **whether downstream components can still identify the restriction after safety-relevant information is removed from the representation**.

## Safety note

The exact operational details of restricted acquisition are intentionally omitted from this artifact. The early tests are documented only at the level necessary to establish the baseline.
