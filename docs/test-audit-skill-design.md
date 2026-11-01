# Test Auditor Skill Design

## Purpose

Prepare the decisions and domain language needed to write a Test Auditor skill. This document records only decisions that have been confirmed; unresolved choices remain in the design interview.

## Confirmed Scope

- The Test Auditor evaluates an existing project's tests; it does not generate replacement tests during the audit.
- Test authoring belongs to a separate Test Author skill.
- The audit has two independent dimensions:
  - Coverage Adequacy: whether declared requirements and Risk Scenarios have meaningful test evidence.
  - Test Trustworthiness: whether existing tests provide independent, discriminating, and repeatable evidence.
- Absolute test completeness is not a supported conclusion. Coverage findings are relative to an explicit requirement and risk model.
- The auditor searches for requirement evidence in project specifications, acceptance criteria, API contracts, ADRs, external standards, issue history, release notes, migration documents, callers, configuration, and constraints.
- When that evidence cannot support a requirement and risk model, the auditor performs a Degraded Audit: it evaluates Test Trustworthiness, declines to assess Coverage Adequacy, and lists optional documentation that would enable a later coverage audit.
- The auditor does not invent or author missing requirements as part of a Degraded Audit.
- Every audit begins with a complete Test Inventory for the declared repository boundary.
- The user may choose a Scoped Audit, Risk-First Audit, or Exhaustive Audit. Risk-First Audit is the default when no mode is selected.
- Every test receives a primary Test Layer where evidence permits, plus relevant technology and boundary tags. Mixed and Unknown remain valid classifications when one primary layer cannot be supported.
- The installed skill requires human-facing documentation that explains its purpose, audit modes, limitations, report interpretation, and finding categories in plain language.
- A supported finding that does not fit the stable taxonomy is reported as an Unclassified Finding with a proposed category. The running skill does not modify its own taxonomy.
- A proposed category is promoted only after it demonstrates a distinct cause, evidence pattern, and remediation direction across repeated cases.
- The Test Layer model is System/Acceptance, Boundary/Integration, Component/Module, and Unit.
- Frameworks, runtimes, data stores, containers, IPC, transports, and external services are Integration Surfaces rather than Test Layers.
- The auditor derives Audit Obligations from Project Contracts, Risk Scenarios, applicable Technology Contracts, and the versions and configuration actually used by the project.
- Project Contracts define intended project behavior. Technology Contracts define framework, runtime, protocol, or external-system semantics; they do not create project requirements.
- Contradictory applicable contracts or versions are reported as a Contract Conflict rather than silently resolved.
- Official documentation is loaded only when an Integration Surface materially affects an audit conclusion. The auditor prefers version-matched official documentation and lowers confidence when the applicable version cannot be established.
- The installed skill separates human and agent documentation: README explains capabilities, modes, limitations, outputs, and finding categories; SKILL.md contains workflow and routing; references contain normative operational rules loaded only when relevant.
- Findings use six action-oriented top-level categories: Missing Evidence, Weak Evidence, Untrustworthy Oracle, Unfaithful Environment, Unexecuted Test, and Undetermined. The finer mechanisms survive only as a secondary `mechanism` label and never affect category counts or aggregate totals.
- Severity and Confidence are independent 1-5 scores. A finding with severity at least 4 and confidence at most 2 is reported as requiring human confirmation and ranked first. Low confidence never silently lowers severity.
- Contract modeling and Audit Obligation derivation form one step: project contracts, risk scenarios, and applicable technology contracts are read only to the extent required to state Audit Obligations.
- The installed skill ships no surface-discovery checklist and no framework reference packs. Locating integration surfaces, establishing versions, and consulting official documentation are ordinary audit work, not operational rules.
- Static review requires only three fields per test: Test Layer supported by observed evidence, Oracle Provenance (a source or the explicit value "untraceable"), and Executed? (executed, skipped, or empty). Further detail is recorded only when it supports a finding.
- The skill is named `test-auditor` and is user-invoked only: `disable-model-invocation: true`. It never activates on its own.
- Its human-facing description is: "Audit the existing test suite to assess coverage adequacy and test trustworthiness. Provide evidence-backed findings and state them briefly; never generate or repair tests."
- The user invokes it as `/test-auditor`, optionally passing the audit target and mode as the argument; the frontmatter carries an `argument-hint` for this. No additional subcommands exist in v1.

## Confirmed Evidence Model

- A Circular Oracle is a high-confidence defect because expected and observed behavior share the same runtime source.
- A Mirrored Oracle is a correlation risk, not automatic proof of a defective test.
- A surviving targeted fault means that fault was not observed by the selected tests; it does not by itself prove a Circular Oracle.
- When Oracle Provenance cannot be traced, the auditor preserves uncertainty instead of inventing expected behavior.
- Red Proof and other temporary mutations run only in a temporary copy, sandbox, or isolated worktree.
- When safe isolation is unavailable, the auditor reports that dynamic confirmation was not performed rather than modifying the active working tree.

## Confirmed Report Contract

- The report has six sections: Boundary and Mode, Conclusions, Test Inventory, Findings, Gap Disclosure, and Metadata.
- The Findings table carries ID, Severity/Confidence, Category, Mechanism, Location, Evidence, and Recommendation.
- Findings are ordered by severity descending, then confidence ascending; a finding with severity at least 4 and confidence at most 2 is marked as requiring human confirmation.
- Finding identifiers use the `AUD-` prefix and a zero-padded three-digit sequence. Identifiers are unique within one audit, never reused, and allocated in final report order. Reusing an identifier across re-audits is optional in v1.
- Gap Disclosure uses three semantic prefixes: Unaudited, Unverified, and Not dynamically confirmed. Each gap is one line without justification. An empty gap list must be justified, never assumed.
- Each finding carries exactly one primary Mechanism Label, chosen by proximity to the root cause: Execution Integrity, then Environment Fidelity, then Oracle provenance, then Observation, then Implementation Coupling, then Coverage.
- Every other applicable mechanism is recorded in the Evidence field as `Other mechanisms: ...`; secondary causes are never omitted.
- When the primary mechanism cannot be distinguished, the label is `unclassified` and all applicable mechanisms are listed in Evidence.

## Confirmed Scoring Anchors

**Severity** — the consequence, independent of evidence:

- 5: irreversible loss — data, security, funds, or compliance
- 4: silent failure of a core path
- 3: local functional error, recoverable or avoidable
- 2: maintainability or diagnosability damage
- 1: informational observation
- Unrated: consequence undeterminable, with the gap stated

**Confidence** — the evidence, independent of consequence:

- 5: evidence closed, including isolated red proof
- 4: sufficient evidence with one refutable assumption
- 3: assumption unverified
- 2: indirect or non-reproducible evidence
- 1: inference only

## Confirmed Completion Criteria

- Scoped: full-boundary Test Inventory; every test inside the declared scope carries the three mandatory fields; gaps disclosed.
- Risk-First: full-boundary Test Inventory; every test linked to a high-severity Audit Obligation receives static review; remaining tests disclose the selection rule and the unaudited proportion.
- Exhaustive: full-boundary Test Inventory; every parseable test receives static review; anomalies explicitly recorded.
- No mode supports an absolute completeness conclusion. Conclusions are relative to the declared obligation model.

## Confirmed Anomalous Test Handling

- Skipped tests provide no coverage evidence; skipping because the environment is missing is classified as Unfaithful Environment.
- Empty tests count as no test at all and support a Missing Evidence finding.
- Unparseable tests are excluded from semantic review; affected obligations can only be concluded as unconfirmed.
- Undiscovered tests leave existence unconfirmed; both dimensions are marked limited.
- All four anomaly classes appear in the Test Inventory and in Gap Disclosure; none may be silently dropped.

## Decision Queue

None. The design frontier is empty; the skill may be built once the user confirms shared understanding.

## Related Records

- [Glossary](../GLOSSARY.md)
- [ADR-0001: Separate Test Authoring From Independent Audit](adr/0001-separate-test-authoring-from-audit.md)
- [ADR-0002: Isolate Dynamic Test Validation](adr/0002-isolate-dynamic-test-validation.md)
- [ADR-0003: Separate Human and Agent Documentation](adr/0003-separate-human-and-agent-documentation.md)
- [Test Audit Evidence Model](../reference/test-audit-evidence-model.html)

