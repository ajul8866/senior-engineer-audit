# Senior Engineer Audit

A six-phase code audit skill for coding agents. Maps your codebase, investigates functional and security bugs, and verifies findings with independent agents before preparing bug bounty reports for manual submission.

## Install

Run from the project you want to audit. Requires Node.js 22.20 or later, as specified by the [skills CLI](https://github.com/vercel-labs/skills#install-a-skill).

```bash
npx skills add ajul8866/senior-engineer-audit
```

Choose your coding agent when prompted. To install directly for Codex:

```bash
npx skills add ajul8866/senior-engineer-audit --agent codex --yes
```

Add `-g` to make the skill available across projects.

## Usage

Open your project in Codex and enter:

```text
Use $senior-engineer-audit to audit this repository and prepare independently
verified bug bounty reports for manual submission.
```

Provide the program scope and rules with your request when preparing reports for a specific bounty program. Report language and format follow your request or the program requirements.

## How it works

| Phase | What happens |
| --- | --- |
| 1. Map | Identify components, entrypoints, data flow, trust boundaries, and review coverage. |
| 2. Investigate | Review each area and reproduce suspected functional or security bugs. |
| 3. Confirm | A fresh agent independently tries to prove or disprove each candidate. |
| 4. Record | Document evidence, preconditions, impact, severity, verdicts, and duplicate relationships. |
| 5. Verify again | Another fresh agent, distinct from the discoverer and first verifier, checks each record against the evidence. |
| 6. Report | Prepare eligible findings for manual submission and retain the audit history and coverage gaps. |

Full verification requires an agent with fresh subagent support. Unavailable verification or blocked runtime checks remain explicitly incomplete.

## Output

The agent writes results outside the target repository by default:

```text
index.md         # Findings, dispositions, limitations, and remaining work
coverage.md      # Areas reviewed, evidence, exclusions, and blockers
records/         # All candidates, including rejected and unresolved leads
evidence/        # Reproductions and sanitized supporting evidence
reports/         # Findings that meet the submission-readiness criteria
```

Submission readiness requires technical evidence, both independent checks, adequate reproduction, program eligibility, demonstrated impact, duplicate handling, and sanitized evidence. Functional bugs without qualifying bounty impact remain internal observations. Local review can proceed without program rules, with bounty eligibility marked unknown.

Live testing follows the supplied authorization and program rules. Coverage is recorded explicitly; complete bug discovery and bounty acceptance are not guaranteed.

See [SKILL.md](SKILL.md) for the complete workflow and [references/reporting.md](references/reporting.md) for record formats, report templates, and readiness criteria.
