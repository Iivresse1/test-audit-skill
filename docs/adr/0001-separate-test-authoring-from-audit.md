---
status: accepted
---

# Separate Test Authoring From Independent Audit

The project will define a Test Author and a separate Test Auditor. Combining them would be convenient, but an auditor that immediately evaluates tests it just produced shares the author's assumptions and weakens the independence of the review; the auditor therefore evaluates existing tests and reports findings without generating replacement tests as part of the same responsibility.

## Considered Options

- One skill writes and audits tests: less coordination, but correlated reasoning and a broad responsibility.
- Separate author and auditor skills: more coordination, but clearer completion criteria and a genuinely adversarial review boundary.

## Consequences

The two skills may share terminology and evidence definitions, but their workflows and completion criteria remain separate.

