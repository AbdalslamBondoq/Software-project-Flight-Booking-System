# Prompt Records

This folder stores one Markdown file for each meaningful task given to the coding agent, as required by Section 3.3 of the project instructions. Each record is linked from [`docs/ai_development_log.md`](../docs/ai_development_log.md).

## File Naming

`vX.Y.Z-<short-task-name>.md`, for example `v0.1.0-auth-implementation.md` or `v0.4.0-design-seat-hold.md`.

## Template

```markdown
# vX.Y.Z - <Task title>

| Field | Value |
|---|---|
| Version / increment | vX.Y.Z |
| Agent | Claude Code |
| Requested by | <team member> |
| Date | YYYY-MM-DD |
| Pull request | #NN |

## Goal
<What the agent must build or change.>

## Relevant Requirements and Design
- Requirements: FR-xx, NFR-xx
- Diagrams: uml/<file>.md

## Key Instructions Given to the Agent
1. ...

## Intended Outputs
- Source files: src/...
- Tests: tests/...

## Acceptance Criteria
- ...

## Review Notes
- Reviewer: <team member>
- What was checked, what was wrong, and how it was corrected.
```

## Records

| File | Version | Task |
|---|---|---|
| [v0.1.0-design-docs-review.md](v0.1.0-design-docs-review.md) | v0.1.0-design | Documentation review against the project instructions |
