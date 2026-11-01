# Evidence Model

Rules for judging what a test actually exercises and where its expected result comes from.

## Test Layer

The system boundary and environment a test actually exercises. Classify it from observed behavior: what the test opens, stubs, calls, or waits on — not from its directory or framework label.

Record the observation behind the classification. A test that claims to be integration but substitutes the real dependency for a double belongs in the layer its doubles actually reach.

## Oracle Provenance

The traceable origin of the expected result. Acceptable sources:

- a Project Contract: specification, acceptance criterion, ADR, public interface;
- an external standard or protocol;
- an invariant or property derived from the domain;
- confirmed historical behavior with an independent record.

When none can be traced, record `untraceable` and preserve the uncertainty. Expected values derived from the implementation, its output, or its own helper code are not independent sources.

## Circular and Mirrored Oracles

**Circular Oracle** — the expected result depends, directly or indirectly, on the same runtime behavior under test. This is a high-confidence defect: expected and observed share a source.

**Mirrored Oracle** — the expected result repeats the implementation's formula or decision process without sharing runtime data. This is a correlation risk: it can agree with the implementation for the same wrong reason. Report it as a risk, not as proof of a defective test.

## Red Proof

A targeted experiment: introduce a relevant temporary fault and observe whether the responsible test detects it.

- The experiment runs only in a temporary copy, sandbox, or isolated worktree. The active working tree stays untouched.
- A surviving fault means the selected tests did not observe that fault. It does not by itself prove a Circular Oracle.
- Check the oracle first. A test that cannot observe the fault and a test that observes it but accepts a wrong result fail differently.
- When isolation is unavailable, record the finding as statically inferred and state that dynamic confirmation was not performed.

## Recording

Each evidence anchor names the file and line plus the observation that supports the conclusion.