# AI Development Log - Flight Booking System (Group 17)

This log records how the team used Agentic AI in each increment: the task given to the agent, the files it changed, the corrections the team required, and who reviewed the output. The full instructions for each task are stored in [`prompts/`](../prompts/).

## 1. Agents Used

| Agent | Used for |
|---|---|
| Claude (Anthropic) | Assistant used by the team to review the documentation against the project instructions and to apply approved documentation changes |
| Claude Code | Planned for implementation and tests from v0.1.0 onwards |

## 2. How the Team Works with the Agent

A team member gives the agent a task and records it in `prompts/`. For each change, the agent explains what it will change and why. The team member approves or rejects the change before it is applied, then reviews the result in the pull request.

## 3. Log

| Version | Agent task / prompt ref. | Changed modules | Issues / corrections | Student review |
|---|---|---|---|---|
| v0.1.0-design | [prompts/v0.1.0-design-docs-review.md](../prompts/v0.1.0-design-docs-review.md) - Claude | `README.md`, folder READMEs, `docs/testing.md`, `docs/ai_development_log.md`, `prompts/` ([PR #28](https://github.com/AbdalslamBondoq/Software-project-Flight-Booking-System/pull/28)) | The agent first reviewed an outdated local copy; it re-checked the current `main` branch before editing. Applied at Abdullah's request from his account. | Abdullah Jaber - pending |

## 4. How to Add an Entry

1. Create a prompt record in `prompts/` named `vX.Y.Z-<task>.md` before giving the task to the agent.
2. After the agent finishes, list the files it changed and link the pull request.
3. Record anything the agent got wrong and how the team corrected it.
4. Record which team member reviewed the output and what they checked.
