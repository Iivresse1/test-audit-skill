# Modes and Completion

## Modes

**Scoped** — semantic review is limited to an explicitly selected feature, directory, requirement, or set of tests. The inventory still covers the full boundary.

**Risk-First** (default) — the full inventory is prioritized by consequence and likelihood. Every test linked to a high-severity Audit Obligation receives semantic review; the remainder is disclosed with the selection rule and the unaudited proportion.

**Exhaustive** — every parseable test in the repository boundary receives semantic review, with anomalies recorded.

## Completion

- **Scoped**: full-boundary inventory; every test inside the declared scope carries Test Layer, Oracle Provenance, and Executed?; gaps disclosed.
- **Risk-First**: full-boundary inventory; every test linked to a high-severity Audit Obligation reviewed; selection rule and unaudited proportion disclosed.
- **Exhaustive**: full-boundary inventory; every parseable test reviewed; every anomaly recorded.

No mode supports an absolute completeness conclusion. Conclusions are relative to the declared obligation model.

## Anomalous Tests

| Anomaly | Effect |
|---|---|
| Skipped | Supplies no coverage evidence. Skipping because the environment is missing is Unfaithful Environment; other skips are Unexecuted Test. |
| Empty | Counts as no test and supports Missing Evidence. |
| Unparseable | Excluded from semantic review; affected obligations are concluded unconfirmed. |
| Undiscovered | Existence stays unconfirmed; both dimensions are marked limited. |

Every anomaly appears in the Test Inventory and in Gap Disclosure. None is dropped silently.

## Degraded Audit

A usable requirement and risk model is the prerequisite for a Coverage Adequacy claim.

- Missing or contradictory contracts: assess Test Trustworthiness, make no Coverage Adequacy claim, and record the missing model as Unverified.
- No tests at all: report that no auditable evidence exists. The audit still does not author tests.