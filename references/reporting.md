# Evidence records and bug bounty reports

Use these formats during all six phases. Adapt the final submission to supplied program requirements without weakening the evidence or independence requirements.

## Output layout

Use a new audit directory outside the target, or the output location selected by the user:

```text
index.md
coverage.md
records/C-001.md
evidence/C-001/
reports/C-001.md
```

Create report files only for findings that pass the readiness gate. Store provisional report material in records. Keep rejected candidates and duplicate aliases in the index/ledger; they do not need submission files. Capture relevant command output and reproduction assets, rather than dumping entire logs or unrelated repository content. Record the actual chosen output path in the handoff.

## Candidate record

Use explicit `unknown` or `not run` values where necessary. Never fill an evidence field with a predicted outcome.

| Field | Required content |
| --- | --- |
| Identity | Stable ID, concise title, discoverer agent identity, date, canonical ID if duplicate |
| Target | Repository/revision, relevant local changes, component, file and line references; distinguish source from deployed assets |
| Eligibility | Program/asset scope, applicable rules and their source/version, exclusions; `eligible`, `ineligible`, or `unknown` with reasons |
| Claim | Expected behavior and its basis, actual behavior, reachable trigger, root-cause trace, relevant guards/counterevidence |
| Preconditions | Required access/role, configuration, attacker control, victim interaction, deployment assumptions |
| Reproduction | Minimal steps, synthetic fixtures/accounts, exact commands/requests, observed outputs, environment, cleanup if needed |
| Evidence | Relative paths to sanitized evidence, capture provenance, commands actually executed, failures and limits |
| Impact | Demonstrated security consequence, affected boundary/data, realistic scale; distinguish observations from inference |
| Severity | Proposed severity and reasoning; program rating scheme when supplied; unknown where impact is unproven |
| Recommendation | Root-cause fix guidance and a meaningful regression scenario; no target edits |
| Phase 3 | Actual verifier identity, verdict, independent checks/results, counterevidence and unresolved questions |
| Phase 5 | Actual second verifier identity, disposition, assertion checks, rerun results/limits and required revisions |
| Disposition | Submission-ready, confirmed/internal, unresolved, rejected, or duplicate; reasons and remaining work |

Keep technical verdict, record verification, and eligibility separate. Examples:

- A confirmed IDOR with unknown program scope is a verified technical finding pending eligibility, not submission-ready.
- A false alarm with a sound rejection rationale may have a verified record and still remain rejected.
- A functional calculation error without a qualifying security consequence stays an internal observation.
- A duplicate may have a valid reproduction; link it to the canonical finding rather than inflating the report count.

An independent check must identify what the agent actually inspected or ran and the resulting evidence. Record tool-provided agent IDs or task identities; do not invent external reviewers, tool runs, timestamps, or results.

## Coverage entry

For each area or cross-component flow record:

```text
Area | Paths/entrypoints | Risk/checks | Inspection and test evidence |
Candidate IDs | Status | Exclusion, blocker, or remaining work
```

Include untouched areas and inaccessible components. A successful test run covers its assertions only. Broad coverage does not prove the absence of vulnerabilities.

## Submission-readiness gate

All of the following must hold before creating a final submission file:

1. **Technical validity:** phase 3 is `confirmed`; the reachable path, preconditions, actual behavior, and security impact have evidence.
2. **Record validity:** phase 5 is `verified` by an agent distinct from the discoverer and phase-3 verifier, with no unresolved material contradiction or unverified revision.
3. **Reproduction:** another reviewer has sufficient steps/assets to reproduce. An independently reproduced local PoC can establish a source-code issue, but not production exposure. If execution was unavailable, require conclusive traced evidence and program acceptance of source-only reports; otherwise keep the report provisional and name the missing check.
4. **Eligibility:** available program rules establish the asset, vulnerability class, and performed validation are in scope. Required deployment evidence must exist if claiming a live asset is affected. Missing rules mean eligibility is unknown.
5. **Impact and severity:** the demonstrated consequence qualifies under the program rules. Severity does not depend on invented credentials, unsupported chaining, or unverified configuration. Use supplied rating guidance; include a CVSS vector or platform taxonomy only when supported and checked against its authoritative definition.
6. **Canonical finding:** internal duplicates are merged by root cause and boundary. Do not assert uniqueness against private reports you cannot access.
7. **Evidence hygiene:** report text, attachments, requests, responses, filenames, and URLs are sanitized. Preserve reproducibility with labeled placeholders and instructions for obtaining the reviewer's own credentials. Share only authorized synthetic or appropriately redacted data.

If a gate fails, keep the record and state exactly what is missing. Do not turn an incomplete runtime check into a successful check by lowering the claim after the fact; revise the claim explicitly and re-verify it.

## Default submission template

Use this only when no program template is provided. Replace bracketed fields with supported claims and omit inapplicable optional fields. Use portable relative evidence links and include the referenced sanitized assets in the handoff.

```markdown
# [Affected component]: [vulnerability] allows [demonstrated consequence]

## Summary

[Who can trigger what behavior, the broken security boundary, and the consequence.]

## Affected asset and version

[In-scope asset or source repository/revision. File/line references and deployment
evidence where applicable. Do not equate a local checkout with production.]

## Preconditions

[Roles, configuration, attacker-controlled inputs, and required interaction.]

## Steps to reproduce

1. [Prepare synthetic data/accounts and the stated environment.]
2. [Run the exact command or request; explain credential placeholders.]
3. [Observe the specific unauthorized or incorrect outcome.]

## Proof of concept and evidence

[Minimal runnable PoC or request, sanitized actual output, relative evidence links,
and cleanup when applicable. Identify any unexecuted steps explicitly.]

## Expected and actual behavior

[Expected behavior and its basis, followed by the demonstrated deviation.]

## Impact and severity

[Concrete security consequence, realistic preconditions and limits, severity
rationale, and any clearly labeled inference.]

## Root cause and recommendation

[Code path and missing/incorrect control, a focused fix recommendation, and a
regression scenario that would catch the issue.]

## Validation and limitations

[What was independently reproduced or traced, tested revision/environment,
and material limitations. Avoid claiming broader deployment coverage.]
```

Keep internal agent transcripts, rejected leads, duplicate aliases, and coverage administration in the audit index and records rather than the submission narrative. Agent agreement is provenance, not proof of impact.

## Final handoff

In `index.md`, link reports and records by disposition, link the coverage matrix, and record the audit revision, rules source, executed checks, blockers, and remaining queue. State whether the audit is complete or partial and whether reports are ready for manual submission. Preserve pending scope or verification requirements even when no final reports qualify. The skill never submits reports or promises payment.
