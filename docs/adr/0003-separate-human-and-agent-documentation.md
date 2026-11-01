---
status: accepted
---

# Separate Human and Agent Documentation

The installed skill will keep a human-facing README separate from the agent-facing SKILL.md and operational references. A single combined guide would be easier to author, but it would load installation, explanation, and report-reading material into the agent's context on every invocation; README therefore explains capabilities and findings to users, while SKILL.md routes the workflow and references disclose detailed decision rules only when needed.

## Consequences

README may summarize finding categories in plain language, but normative classification criteria have one authoritative home in the relevant agent reference. Documentation reviews must reject duplicated operational rules that could drift between audiences.
