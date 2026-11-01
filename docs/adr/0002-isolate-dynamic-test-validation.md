---
status: accepted
---

# Isolate Dynamic Test Validation

Red Proof and other fault-injection checks will run only in a temporary copy, sandbox, or isolated worktree. Mutating and restoring the user's active working tree would be simpler, but it cannot reliably distinguish the auditor's temporary edits from existing user changes; when isolation is unavailable, the auditor retains the static finding and reports that dynamic confirmation was not performed.

## Consequences

Dynamic validation is optional evidence rather than a prerequisite for every finding. The audit report must identify which conclusions were statically inferred and which were dynamically confirmed.
