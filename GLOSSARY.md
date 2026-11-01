# Test-Suite Audit

This context defines the language used to design skills that create tests and independently audit the evidence supplied by existing test suites.

## Language

**Test Author**:
A skill that creates or revises tests from requirements, risks, and observed project conventions.
_Avoid_: Test generator, testing skill

**Test Auditor**:
A skill that independently evaluates an existing test suite without creating replacement tests as part of the audit.
_Avoid_: Test author, test fixer

**Coverage Adequacy**:
The degree to which a declared set of requirements and risk scenarios has meaningful test evidence.
_Avoid_: Complete coverage, test completeness

**Test Trustworthiness**:
The degree to which a test provides independent, discriminating, and repeatable evidence for the behavior it claims to verify.
_Avoid_: Test quality, good test

**Test Oracle**:
The basis used to decide whether an observed result satisfies the expected behavior.
_Avoid_: Expected value

**Oracle Provenance**:
The traceable origin of a test oracle, such as a requirement, external standard, invariant, or confirmed historical behavior.
_Avoid_: Source of truth

**Circular Oracle**:
A test oracle whose expected result depends directly or indirectly on the same behavior of the system under test.
_Avoid_: Mirrored oracle, weak assertion

**Mirrored Oracle**:
A test oracle that independently repeats the implementation's formula or decision process and therefore shares assumptions without necessarily sharing runtime data.
_Avoid_: Circular oracle

**Risk Scenario**:
A requirement-linked failure mode or boundary condition whose consequences justify test evidence.
_Avoid_: Edge case

**Red Proof**:
A targeted experiment that introduces a relevant temporary fault and observes whether the responsible test detects it.
_Avoid_: Mutation score

**Degraded Audit**:
An audit that evaluates Test Trustworthiness but makes no Coverage Adequacy claim because the requirement and risk model is insufficient.
_Avoid_: Full audit, inferred specification

**Test Inventory**:
A complete catalog of discovered tests and their observable scope, Test Layer, subject, and available requirement or risk links.
_Avoid_: Test list, coverage report

**Audit Scope**:
The declared subset of the Test Inventory selected for semantic review and any dynamic validation.
_Avoid_: Sample

**Scoped Audit**:
An audit whose semantic review is limited to an explicitly selected feature, directory, requirement, or set of tests.
_Avoid_: Partial audit

**Risk-First Audit**:
An audit that inventories the full suite and prioritizes semantic review by consequence and likelihood while disclosing what received less scrutiny.
_Avoid_: Sampled audit

**Exhaustive Audit**:
An audit that applies semantic review to every item in the Test Inventory within the declared repository boundary.
_Avoid_: Full coverage

**Test Layer**:
The system boundary and environment actually exercised by a test, classified from observed behavior rather than its filename or framework label.
_Avoid_: Test folder, test type

**Integration Surface**:
A technology or process boundary whose real semantics affect the behavior under audit, such as persistence, transport, messaging, containers, IPC, or an external service.
_Avoid_: Test layer, dependency

**Audit Obligation**:
A behavior for which the auditor expects test evidence, derived from a project contract, Risk Scenario, and any relevant technology contract.
_Avoid_: Test case, generated requirement

**Project Contract**:
The project's declared behavior from specifications, acceptance criteria, ADRs, public interfaces, and other project-owned normative documents.
_Avoid_: Implementation behavior

**Technology Contract**:
The behavior guaranteed or required by a framework, runtime, protocol, or external system at the version used by the project.
_Avoid_: Project requirement

**Contract Conflict**:
A contradiction between applicable Project Contracts, Technology Contracts, versions, or observed configuration that prevents one unambiguous Audit Obligation.
_Avoid_: Test failure

**Unclassified Finding**:
A supported test-audit finding that does not yet justify changing the stable finding taxonomy.
_Avoid_: New category

**Finding Category**:
The top-level classification of an audit finding, chosen by the action it requires: missing evidence, weak evidence, untrustworthy oracle, unfaithful environment, unexecuted test, or undetermined.
_Avoid_: Finding type, defect class

**Mechanism Label**:
A secondary descriptor that names the specific mechanism behind a finding without changing its Finding Category or aggregate counts.
_Avoid_: Subcategory

**Severity Score**:
A 1-5 rating of the consequence of the Risk Scenario affected by a finding, independent of how well that finding is evidenced.
_Avoid_: Priority, impact score

**Confidence Score**:
A 1-5 rating of the evidential support for a finding, independent of the consequence at stake.
_Avoid_: Certainty, likelihood

**Finding Identifier**:
The `AUD-` prefixed number that names a finding within one audit, unique and never reused.
_Avoid_: F1-style or M1-style shorthand

