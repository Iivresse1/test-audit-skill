# Test Auditor — Design and Build Handoff

## Purpose

Continue work on `test-auditor`, a user-invoked Codex Skill that independently audits an existing test suite. The design phase is closed and the skill skeleton is built. This document lets any collaborator pick up the work without access to the original workstation: it records where each artifact lives, what is already decided, and what remains to do.

Repository: https://github.com/Iivresse1/test-audit-skill

## Repository Map

The repository keeps three parallel branches. Do not merge them; each branch owns one kind of content.

| Branch | Contents |
|---|---|
| `main` | The skill itself: `test-auditor/SKILL.md`, `test-auditor/README.md`, and `test-auditor/references/` |
| `building-docs` | Mission, resources, glossary, design document, ADRs, and learning artifacts |
| `handoff` | This handoff document |

Temporary or experimental skill versions belong on a separate branch; `main` stays limited to the skill body.

## Source of Truth

Read from the `building-docs` branch:

- `GLOSSARY.md`
- `MISSION.md`
- `RESOURCES.md`
- `docs/test-audit-skill-design.md`
- `docs/adr/0001-separate-test-authoring-from-audit.md`
- `docs/adr/0002-isolate-dynamic-test-validation.md`
- `docs/adr/0003-separate-human-and-agent-documentation.md`

Supporting learning artifacts, same branch:

- `lessons/0001-static-triage-and-red-proof.html`
- `reference/test-audit-evidence-model.html`
- `learning-records/0001-separate-author-and-auditor.md`

Read `GLOSSARY.md` and `docs/test-audit-skill-design.md` first. Use the ADRs only when their rationale is needed.

Do not restate or redesign decisions already captured in these artifacts.

## Confirmed Design State

- The skill separates Coverage Adequacy from Test Trustworthiness and reports them separately.
- Findings use six action-oriented top-level categories: Missing Evidence, Weak Evidence, Untrustworthy Oracle, Unfaithful Environment, Unexecuted Test, Undetermined. Finer mechanisms survive only as secondary `mechanism` labels.
- Severity and Confidence are independent 1-5 scores displayed as `S5/C2`. Low confidence never lowers severity; severity at least 4 with confidence at most 2 is flagged for human confirmation and ranked first.
- Contract modeling and Audit Obligation derivation are a single step.
- Static review requires only three fields per test: Test Layer, Oracle Provenance, Executed?.
- The report uses six sections and `AUD-001` identifiers; Gap Disclosure uses three prefixes: Unaudited, Unverified, Not dynamically confirmed.
- Scoped, Risk-First, and Exhaustive completion criteria and anomalous test handling are recorded in the design document.
- No surface-discovery checklist and no framework reference packs are shipped. Version uncertainty lowers confidence only where a conclusion depends on the affected Technology Contract.
- The seven-step skeleton is frozen: intake, Test Inventory, contract and obligation modeling, static review, optional dynamic confirmation, adjudication and reporting, completion.
- The skill is named `test-auditor` and is user-invoked only (`disable-model-invocation: true`). Users run it as `/test-auditor`, passing the audit target and optional mode as the argument via `argument-hint`.
- Description: "Audit the existing test suite to assess coverage adequacy and test trustworthiness. Provide evidence-backed findings and state them briefly; never generate or repair tests."
- Severity anchors: 5 irreversible loss; 4 silent core-path failure; 3 local recoverable error; 2 maintainability damage; 1 informational; `Unrated` with the gap stated. Confidence anchors: 5 closed evidence or isolated red proof; 4 one refutable assumption; 3 unverified assumption; 2 indirect or non-reproducible; 1 inference only.
- One primary Mechanism Label per finding, chosen by root-cause proximity (Execution Integrity, Environment Fidelity, Oracle provenance, Observation, Implementation Coupling, Coverage). Secondary causes are listed in Evidence and never omitted; indistinguishable cases use `unclassified`.

## Build State

The `main` branch contains the built skill:

```text
test-auditor/
├── SKILL.md
├── README.md
└── references/
    ├── evidence-model.md
    ├── report-contract.md
    ├── scoring.md
    └── modes.md
```

Frontmatter, file structure, and cross-references are validated. The skill has not yet been installed into a skills directory, and no trial audit against a real repository has been run.

## Next Step

1. Run a trial audit on a real repository with an existing test suite, in each of the three modes where practical.
2. Check that the report follows `references/report-contract.md` and that every gap is disclosed.
3. Install the skill into the target agent's skills directory once the trial output is satisfactory.
4. Record findings about the skill itself on the `handoff` branch or in a new temporary branch, never on `main`.

## Working Style

- Discussion and human-facing explanations use Chinese unless the collaborator agrees otherwise.
- Use question-driven, critical design discussion rather than silently choosing major policy.
- Distinguish project requirements from technology semantics.
- State coverage conclusions relative to the declared obligation model; never claim absolute completeness.
- Dynamic validation must not modify the user's working tree. Mutation and red-proof checks run in an isolated copy, sandbox, or worktree.
- Keep human explanations plain-language while keeping normative agent rules compact and precise.
- Never commit credentials or inspect credential-like files.

## Suggested Skills

- `grilling`: stress-test unresolved design choices.
- `writing-for-agents`: edit design documents and write compact agent-facing instructions.
- `skill-creator`: build or revise the skill structure.
- `openai-docs`: verify current Codex Skill-format or invocation behavior when needed.