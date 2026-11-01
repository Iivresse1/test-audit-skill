# test-auditor

Independently audit an existing test suite. The auditor asks whether the suite supplies real evidence for the project's requirements and risks, and whether each test can be trusted to discriminate a failure. It reports findings; it does not write or repair tests.

## Invocation

```
/test-auditor [target] [mode]
```

Examples:

- `/test-auditor` — Risk-First across the current repository.
- `/test-auditor tests/ scoped` — only the selected path.
- `/test-auditor src/payments risk-first` — prioritize the named risk area.
- `/test-auditor exhaustive` — semantic review of every parseable test.

The skill is user-invoked. It does not activate on its own.

## Modes

| Mode | What it reviews | Default |
|---|---|---|
| Scoped | Every test inside a declared feature, directory, requirement, or test set | |
| Risk-First | The full inventory, reviewed by consequence and likelihood, with disclosure of what received less scrutiny | ✓ |
| Exhaustive | Every parseable test in the repository boundary | |

A repository without a usable requirement and risk model enters **Degraded Audit**: trustworthiness is assessed, and no coverage claim is made.

## What you get

A report with six sections: boundary and mode, conclusions, test inventory, findings, gap disclosure, and metadata.

Findings are numbered `AUD-001`, `AUD-002`, and so on. Each carries:

- a category — missing evidence, weak evidence, untrustworthy oracle, unfaithful environment, unexecuted test, or undetermined;
- a mechanism label — the specific cause, with secondary causes listed in the evidence;
- a severity score from 1 to 5 and a confidence score from 1 to 5, shown as `S4/C3`;
- the evidence anchor, and a recommended next action.

Coverage adequacy and test trustworthiness are reported separately. Low confidence is shown, never used to lower severity. Findings at severity 4–5 with confidence 1–2 are marked **requires human confirmation** and lead the report.

## Limits

- Coverage conclusions are relative to the declared obligations. The audit does not claim absolute completeness.
- Static review is the baseline. Dynamic confirmation requires an isolated copy; when isolation is unavailable, findings remain statically inferred and the report says so.
- Gaps are part of the result. An empty gap list must be justified.