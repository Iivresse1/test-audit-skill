# Report Contract

The report is the audit's only output. Write it in the user's language while keeping the six sections and the finding fields stable.

## Sections

1. **Boundary and Mode** — repository boundary and commit, paths in scope, mode, and the statement that conclusions are relative.
2. **Conclusions** — Coverage Adequacy and Test Trustworthiness, each with its own conclusion or an explicit Degraded Audit.
3. **Test Inventory** — counts by execution state: executed, skipped, unparseable, empty, undiscovered.
4. **Findings** — the table below.
5. **Gap Disclosure** — what was not audited, not verified, or not dynamically confirmed.
6. **Metadata** — unclassified findings count and dynamic confirmation count with isolated locations.

## Findings

Columns: `ID`, `Severity/Confidence`, `Category`, `Mechanism`, `Location`, `Evidence`, `Recommendation`.

Order by severity descending, then confidence ascending. Findings at severity 4–5 with confidence 1–2 are marked **requires human confirmation** and lead the report. Display the scores joined: `S5/C2`.

Every finding carries exactly one primary mechanism. Other applicable mechanisms appear in the Evidence field as `Other mechanisms: ...`; they are never omitted.

## Identifiers

Format `AUD-` plus three zero-padded digits: `AUD-001`. Identifiers are unique within one audit, never reused, and allocated in final report order. Across re-audits, a persisting finding may keep its identifier; this is optional in v1.

## Gap Disclosure

Three prefixes, one line each, no justification:

- `Unaudited:` — scope not semantically reviewed.
- `Unverified:` — a conclusion held back by a missing contract or an unconfirmed version.
- `Not dynamically confirmed:` — findings that rest on static evidence only.

An empty gap list is stated with its proof, for example `None (all tests in boundary are parseable and were reviewed)`.

## Skeleton

```markdown
# Test audit report · <project>

## Boundary and Mode
- Boundary: <paths>, commit <hash>
- Mode: <scoped | risk-first | exhaustive>
- Conclusions are relative to the declared obligation model.

## Conclusions
- Coverage Adequacy: <conclusion or Degraded Audit>
- Test Trustworthiness: <conclusion>

## Test Inventory
- Discovered <n>: executed <n> · skipped <n> · unparseable <n> · empty <n> · undiscovered <n>
- Semantically reviewed: <n>

## Findings
| ID | S/C | Category | Mechanism | Location | Evidence | Recommendation |
|----|-----|----------|-----------|----------|----------|----------------|
| AUD-001 | S5/C2 | Untrustworthy Oracle | circular-oracle | path:line | <anchor and observation> | <next action> |

## Gap Disclosure
- Unaudited: <one line>
- Unverified: <one line>
- Not dynamically confirmed: <one line>

## Metadata
- Unclassified findings: <n>
- Dynamic confirmations: <n> in <isolated location>
```