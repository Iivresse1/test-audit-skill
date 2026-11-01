# Mission: Design a Reliable Test-Audit Skill

## Why
Design Codex skills that independently audit existing project test suites, so a green suite is not mistaken for evidence when requirements, failure modes, or meaningful assertions are missing.

## Success looks like
- Separate test-suite coverage adequacy from defects inside individual tests.
- Distinguish circular oracles, mirrored logic, weak assertions, and legitimate requirement-based tests.
- Decide when static evidence is enough and when targeted mutation or failure injection is needed.
- Specify separate test-author and independent test-auditor skills with clear responsibilities.

## Constraints
- Start language-agnostic and keep the first auditor read-oriented.
- Judge coverage against explicit requirements and risks rather than claiming absolute completeness.
- Preserve uncertainty when the oracle's provenance cannot be established.

## Out of scope
- Implementing the final skills before the audit taxonomy and evidence model are stable.
- Treating code coverage percentage as proof of behavioral coverage.

