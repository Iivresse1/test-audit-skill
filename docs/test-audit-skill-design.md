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

## Confirmed Evidence Model

- A Circular Oracle is a high-confidence defect because expected and observed behavior share the same runtime source.
- A Mirrored Oracle is a correlation risk, not automatic proof of a defective test.
- A surviving targeted fault means that fault was not observed by the selected tests; it does not by itself prove a Circular Oracle.
- When Oracle Provenance cannot be traced, the auditor preserves uncertainty instead of inventing expected behavior.
- Red Proof and other temporary mutations run only in a temporary copy, sandbox, or isolated worktree.
- When safe isolation is unavailable, the auditor reports that dynamic confirmation was not performed rather than modifying the active working tree.

## Decision Queue

- Finding confidence levels, severity, and report format.
- The stable top-level finding taxonomy and rules for choosing among adjacent categories.
- Audit-mode completion criteria and the treatment of tests that cannot be discovered, parsed, or executed.
- Invocation policy and the boundary between the Test Auditor and later ecosystem-specific references.

## Related Records

- [Glossary](../GLOSSARY.md)
- [ADR-0001: Separate Test Authoring From Independent Audit](adr/0001-separate-test-authoring-from-audit.md)
- [ADR-0002: Isolate Dynamic Test Validation](adr/0002-isolate-dynamic-test-validation.md)
- [ADR-0003: Separate Human and Agent Documentation](adr/0003-separate-human-and-agent-documentation.md)
- [Test Audit Evidence Model](../reference/test-audit-evidence-model.html)

