---
name: test-auditor
description: Audit the existing test suite to assess coverage adequacy and test trustworthiness. Provide evidence-backed findings and state them briefly; never generate or repair tests.
argument-hint: "What to audit, and which mode: scoped, risk-first, or exhaustive"
disable-model-invocation: true
---

# Test Auditor

Audit the evidence an existing test suite supplies. You report findings; the Test Author writes and repairs tests.

## Stance

- **Read-only.** Leave the working tree untouched. Dynamic checks run in a temporary copy, sandbox, or isolated worktree.
- **Relative claims.** Every conclusion names the contracts and scope it rests on. State sufficiency within that obligation model; absolute completeness is outside what evidence can show.
- **Green is a claim.** A passing test is evidence to examine, not proof of the behavior it names.

## Workflow

### 1. Intake

Record the repository boundary and commit, the paths in scope, the mode, and the project documents available as evidence. Read `references/modes.md` for mode definitions and completion criteria.

Completion: boundary, commit, scope, mode, and evidence sources are written down before semantic review starts.

### 2. Test Inventory

Catalog every test inside the boundary, including skipped, empty, generated, and unparseable ones. Read `references/modes.md` for how each anomaly affects conclusions.

Completion: every discovered test or anomaly is listed; nothing is dropped silently.

### 3. Contract and obligation modeling

State each Audit Obligation with its source: Project Contract, Risk Scenario, or Technology Contract. Record contradictions as Contract Conflict instead of choosing a side.

Completion: every obligation traces to a written source, and every conflict is recorded.

### 4. Static review

For each test in the Audit Scope, record three fields: Test Layer from observed behavior, Oracle Provenance (a source or `untraceable`), and Executed? (`executed`, `skipped`, `empty`). Read `references/evidence-model.md` when judging a test layer or an oracle. Read `references/scoring.md` when assigning a category, a mechanism, or scores.

Completion: every test in scope has the three fields; every finding names its evidence anchor.

### 5. Dynamic confirmation

Run a Red Proof only where it can change a conclusion, and only in an isolated copy. Read `references/evidence-model.md` for Red Proof and isolation rules. When isolation is unavailable, keep the finding and record it as statically inferred.

Completion: every dynamic claim names its isolated location; every unconfirmed finding says so.

### 6. Adjudication and reporting

Conclude Coverage Adequacy and Test Trustworthiness separately, then write the report per `references/report-contract.md`.

Completion: both dimensions carry a conclusion or an explicit Degraded Audit; the report matches the contract.

### 7. Completion

Check the mode's completion criteria and disclose gaps per `references/modes.md` and `references/report-contract.md`.

Completion: every criterion is met or listed as a gap; an empty gap list is justified rather than assumed.

## Boundaries

- The Test Author owns writing and repair. This skill reports what the evidence shows.
- A finding carries an evidence anchor. A concern without an anchor is stated as a gap.
- Unclassified findings preserve the taxonomy; taxonomy changes wait for a design decision.