# Test Audit Skill Design Handoff

## Objective

Continue the Chinese-language design session for a future Codex Skill that independently audits an existing project's test suite. The work is still in the design and grilling phase; do not create the final Skill until the unresolved decisions are closed and the user confirms shared understanding.

## Source of Truth

Do not restate or redesign decisions already captured in these workspace artifacts:

- `C:\Users\i\Documents\ChatGPT\For-Asking\MISSION.md`
- `C:\Users\i\Documents\ChatGPT\For-Asking\RESOURCES.md`
- `C:\Users\i\Documents\ChatGPT\For-Asking\GLOSSARY.md`
- `C:\Users\i\Documents\ChatGPT\For-Asking\docs\test-audit-skill-design.md`
- `C:\Users\i\Documents\ChatGPT\For-Asking\docs\adr\0001-separate-test-authoring-from-audit.md`
- `C:\Users\i\Documents\ChatGPT\For-Asking\docs\adr\0002-isolate-dynamic-test-validation.md`
- `C:\Users\i\Documents\ChatGPT\For-Asking\docs\adr\0003-separate-human-and-agent-documentation.md`

Supporting learning artifacts:

- `C:\Users\i\Documents\ChatGPT\For-Asking\lessons\0001-static-triage-and-red-proof.html`
- `C:\Users\i\Documents\ChatGPT\For-Asking\reference\test-audit-evidence-model.html`
- `C:\Users\i\Documents\ChatGPT\For-Asking\learning-records\0001-separate-author-and-auditor.md`

Read `GLOSSARY.md` and `docs/test-audit-skill-design.md` first. Use the ADRs only when their rationale is needed.

## Current State

The user has accepted the documentation split and context-loading strategy: `README.md` is for human readers, `SKILL.md` contains the compact agent workflow and routing rules, and normative material under `references/` is loaded only when relevant. The intended division is designed both for agent comprehension and lower context-token use.

Later confirmations, which supersede the earlier Q14-Q17 draft proposals:

- Findings use six action-oriented top-level categories: Missing Evidence, Weak Evidence, Untrustworthy Oracle, Unfaithful Environment, Unexecuted Test, Undetermined. Finer mechanisms survive only as secondary `mechanism` labels.
- Severity and Confidence are independent 1-5 scores displayed as `S5/C2`. Low confidence never lowers severity; severity at least 4 with confidence at most 2 is flagged for human confirmation and ranked first.
- Contract modeling and Audit Obligation derivation are a single step.
- Static review requires only three fields per test: Test Layer, Oracle Provenance, Executed?.
- The report uses six sections and `AUD-001` identifiers; Gap Disclosure uses three prefixes: Unaudited, Unverified, Not dynamically confirmed.
- Scoped, Risk-First, and Exhaustive completion criteria plus anomalous test handling are confirmed in the design document.
- No surface-discovery checklist and no framework reference packs are shipped. Version uncertainty lowers confidence only where a conclusion depends on the affected Technology Contract.
- The seven-step skeleton is frozen: intake, Test Inventory, contract and obligation modeling, static review, optional dynamic confirmation, adjudication and reporting, completion.
- The skill is named `test-auditor` and is **user-invoked only** (`disable-model-invocation: true`); it never activates on its own. The user runs it as `/test-auditor`, passing the audit target and optional mode as the argument (frontmatter `argument-hint`).
- Description: "Audit the existing test suite to assess coverage adequacy and test trustworthiness. Provide evidence-backed findings and state them briefly; never generate or repair tests."
- Severity anchors: 5 irreversible loss; 4 silent core-path failure; 3 local recoverable error; 2 maintainability damage; 1 informational; `Unrated` with the gap stated. Confidence anchors: 5 closed evidence or isolated red proof; 4 one refutable assumption; 3 unverified assumption; 2 indirect or non-reproducible; 1 inference only.
- One primary Mechanism Label per finding, chosen by root-cause proximity (Execution Integrity, Environment Fidelity, Oracle provenance, Observation, Implementation Coupling, Coverage). Secondary causes are listed in Evidence and never omitted; indistinguishable cases use `unclassified`.

The workspace artifacts listed above are currently untracked. Preserve them. Preserve all unrelated files, especially anything credential-like; do not inspect such files.

## Design Frontier Closed

No open design questions remain. `GLOSSARY.md` and `docs/test-audit-skill-design.md` record the confirmed decisions, including the report contract, scoring anchors, completion criteria, and anomalous test handling.

## Next Step

The skill skeleton is built at `test-auditor/` on the `main` branch: `SKILL.md`, `README.md`, and `references/` with `evidence-model.md`, `report-contract.md`, `scoring.md`, and `modes.md`. Structure, frontmatter, and cross-references are validated.

Next: run a trial audit on a real repository, then install to the user skills directory if approved. Keep this handoff current.

## Working Style

- Continue in Chinese.
- Use a question-driven, critical design discussion rather than silently choosing major policy.
- Distinguish project requirements from technology semantics.
- Do not claim absolute coverage completeness.
- Do not let dynamic validation modify the user's working tree; mutation or red-proof checks belong in an isolated copy, sandbox, or worktree.
- Keep human explanations plain-language while keeping normative agent rules compact and precise.

## Suggested Skills

- `grilling`: continue stress-testing the unresolved design choices.
- `writing-for-agents`: update the design documents and later write compact agent-facing instructions.
- `skill-creator`: create and validate the actual Skill only after the design is confirmed.
- `openai-docs`: use only if current official Codex Skill-format or invocation behavior must be verified.
