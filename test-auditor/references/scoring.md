# Findings: Categories, Mechanisms, Scores

## Finding Category

One category per finding, chosen by the action it requires. Mechanisms are examples, not a closed list.

| Category | Action it requires | Typical mechanisms |
|---|---|---|
| Missing Evidence | Add evidence | coverage-gap, empty-test |
| Weak Evidence | Strengthen the test's discrimination | weak-assertion, observation-defect, implementation-coupling |
| Untrustworthy Oracle | Replace the source of expected behavior | circular-oracle, mirrored-oracle |
| Unfaithful Environment | Make the exercised environment match the real surface | environment-fidelity, isolation, determinism |
| Unexecuted Test | Repair the execution path | skipped-test, execution-integrity |
| Undetermined | Supply the missing contract or accept the limit | missing-contract, contract-conflict, unsupported-surface, undiscovered-test, unparseable-test |

An unrecognised mechanism uses `unclassified` under the closest category. A finding that fits no category is reported as `Unclassified Finding`, counted in Metadata, and never creates a new category during an audit.

## Mechanism Label

Exactly one primary label per finding, chosen by proximity to the root cause:

1. Execution Integrity
2. Environment Fidelity
3. Oracle provenance
4. Observation
5. Implementation Coupling
6. Coverage

Every other applicable mechanism goes into the Evidence field as `Other mechanisms: ...`. When the primary cannot be distinguished, use `unclassified` and list all applicable mechanisms.

## Severity

The consequence of the affected Risk Scenario, independent of the evidence.

| Score | Meaning |
|---|---|
| 5 | Irreversible loss: data, security, funds, or compliance |
| 4 | Silent failure of a core path |
| 3 | Local error, recoverable or avoidable |
| 2 | Maintainability or diagnosability damage |
| 1 | Informational observation |
| Unrated | Consequence undeterminable; state the gap |

## Confidence

The support for the finding, independent of the consequence.

| Score | Meaning |
|---|---|
| 5 | Evidence closed, including isolated red proof |
| 4 | Sufficient, with one refutable assumption |
| 3 | Assumption unverified |
| 2 | Indirect or non-reproducible evidence |
| 1 | Inference only |

## Orthogonality

The scores never convert into each other. Report them side by side. Severity 4–5 with confidence 1–2 is marked **requires human confirmation** and ranked first; confidence never lowers severity. `Unrated` applies to severity only — confidence always lands between 1 and 5.