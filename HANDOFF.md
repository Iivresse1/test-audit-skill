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

The workspace artifacts listed above are currently untracked. Preserve them. Preserve all unrelated files, especially anything credential-like; do not inspect such files.

## Open Design Round

Resume by asking the user to accept, reject, or revise these four proposals. Keep the questions concrete and allow the user to challenge the categories.

### Q14 - Finding Taxonomy

Proposed families and categories:

- Coverage: `Coverage Gap`
- Trustworthiness: `Scenario Construction Defect`, `Oracle Defect`, `Observation Defect`, `Environment Fidelity Defect`, `Isolation/Determinism Defect`, `Execution Integrity Defect`, `Implementation Coupling`
- Audit limitations: `Missing Contract`, `Contract Conflict`, `Unsupported/Unknown Surface`, `Unexecutable Test`

Unknown cases should initially be reported as `Unclassified Finding`; a running Skill must not edit its own taxonomy.

### Q15 - Confidence and Severity

Proposed confidence levels: `Confirmed`, `Supported`, `Suspected`.

Severity should be determined from the consequence of the affected risk scenario, not mechanically from the defect category. The actual severity scale and its definitions are still undecided.

### Q16 - Invocation Policy

Proposed behavior: model-invoked for requests about test-suite audit, coverage adequacy, test trustworthiness, test correctness, or tautological/circular tests. It must not activate for ordinary test generation.

### Q17 - Framework References

Proposed v1 behavior: do not bundle framework-specific reference packs for FastAPI, Docker, Electron, databases, and similar integration surfaces. Detect relevant surfaces, identify actual versions/configuration, and consult official version-matched documentation on demand. Package an adapter only after repeated audits reveal stable, non-obvious reusable rules.

## After Q14-Q17

Immediately update `GLOSSARY.md` and `docs/test-audit-skill-design.md` with each confirmed decision. Add an ADR only for a consequential, hard-to-reverse trade-off; do not create ADRs for routine detail.

The next grilling round should settle:

- severity levels and escalation rules;
- the audit report schema;
- completion criteria for `Scoped`, `Risk-First`, and `Exhaustive` modes;
- how undiscovered, unparsed, skipped, and unexecutable tests affect conclusions;
- the final Skill name, description, and trigger boundaries.

When the design frontier is empty and the user explicitly confirms it, use the Skill creation workflow to build and validate the actual Skill structure.

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
