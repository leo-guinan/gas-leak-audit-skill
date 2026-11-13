---
name: gas-leak-audit
description: Audit an AI agent, workflow, repository, or organization for Generation, Accounting, and Search (GAS) leaks: wasted production, unmeasured costs, lost knowledge, and broken learning loops. Produce an evidence-backed leak register, prioritized repairs, and a recurring inspection schedule. Use when asked to diagnose AI inefficiency, self-audit an agent, map business workflows, detect repeated work or lost knowledge, or measure system learning.
---

# GAS Leak Audit

**GAS = Generation, Accounting, Search.** Every intelligent system generates outputs, accounts for resources and outcomes, and searches for information. A *GAS leak* is a loss of energy, money, time, information, or learning capability caused by a broken, missing, or inefficient connection among these activities.

Your mission: **discover where the system's effort goes, what it produces, what survives, and what is learned.** Do not confuse more activity with more learning.

## Operating rules

1. **Read-only by default.** Inspect only resources and logs actually available and authorized. Never modify code, accounts, billing, schedules, retention settings, permissions, or production systems without specific approval. Avoid secrets and personal data; aggregate or redact. Do not send sensitive content to external services.
2. **Observe before judging.** Never manufacture telemetry, usage totals, historical baselines, counterfactual savings, or proof of learning. Mark unavailable data `unknown` and suggest the smallest useful measurement.
3. **Separate facts, estimates, and hypotheses.** Give every finding an evidence link or reproducible observation, confidence, and a way to falsify it. Avoid saying a process is wasteful merely because it looks redundant: redundancy can provide resilience or quality control.
4. **Bound the audit.** Select one system, one objective, a representative timeframe, and 1–3 key workflows. When scope is missing, start with the current agent and its accessible execution trail, then explicitly describe the limits.
5. **Optimize for user outcomes, not raw token reduction.** Check correctness, quality, reliability, security, accessibility, and human effort before recommending cuts.
6. **No automatic scheduling without authorization.** Recommend a cadence and provide the schedule specification. Create an actual recurring task only after the user explicitly opts in and a scheduling capability is available.

## Audit procedure

### 0. Establish the inspection boundary

Capture: `system`, `owner`, `objective`, `critical workflows`, `time window`, `authorized evidence sources`, `success metrics`, and `constraints` (privacy, quality, reliability, budget). Record what is *not* visible. For self-audits, distinguish present conversation context from externally stored logs: do not assume you can inspect hidden internal reasoning or prior requests.

### 1. Map the GAS lines

For each selected workflow, trace the sequence:

`trigger → search/retrieval → generation/decision → accounting/verification → outcome/feedback → reusable memory → next invocation`

Many workflows branch or loop; draw those edges as needed. Assign each step to one or more categories:

- **G / Generation:** ideas, drafts, inference, code, decisions, artifacts, customer outputs, rework.
- **A / Accounting:** tokens and compute, wall-clock time, human review, dollars, energy (only if measured), quality and failure counts, revenue or other outcomes.
- **S / Search:** retrieval, discovery, prior decisions, context assembly, source validation, memory lookups and updates.

Note systems of record, handoffs, owners, data freshness, and whether the next iteration receives a useful update.

### 2. Inspect for leaks

Check the following failure patterns. Do not assert a leak without evidence.

| ID | Leak | Observable signature | First diagnostic |
|---|---|---|---|
| G1 | Repeated generation | Near-identical outputs are recreated with no useful reuse | Compare task fingerprints or artifact histories |
| G2 | Unused generation | Output produced but never reviewed, deployed, or used | Trace artifact to a downstream decision or outcome |
| G3 | Regeneration due to poor inputs | Frequent correction loops, contradictory instructions | Count retries and classify root causes |
| A1 | Unmeasured cost | No reliable cost/time/quality measure per workflow | Inventory telemetry and missing fields |
| A2 | Expensive routing | High-cost model/tool chosen for low-complexity task without measured benefit | Compare equivalent tasks on quality, latency, total cost |
| A3 | Unclosed outcome loop | Spend is observed, but customer/business outcome is not | Follow an output to a decision and later result |
| S1 | Repeated search | Same question researched again despite prior reliable answer | Sample recurring queries and retrieval hits |
| S2 | Knowledge evaporation | Useful findings remain in chats, private heads, or ephemeral context | Test ability to retrieve a past resolved case |
| S3 | Stale/unsafe retrieval | Old or unverified knowledge is reused as current truth | Check source timestamp, provenance and validation |
| X1 | Broken GAS handoff | Generated knowledge never reaches shared memory or measurement | Trace a single item end-to-end |
| X2 | Measurement without adaptation | Reports recur, but decisions and procedures do not change | Check closed-loop actions across periods |

For each suspected leak: collect a representative example, estimate frequency only when supported, identify likely cause, and propose one minimal intervention. Check whether the intervention would move cost elsewhere (e.g., faster AI output increasing human verification time).

### 3. Test whether learning occurred

**Learning requires demonstrated improvement on comparable tasks, not activity or stored text.** Choose 1–3 benchmark tasks or recurring workflow cases. If a baseline exists, compare before and after on quality-adjusted completion time, human interventions, errors, reuse, and cost. If no baseline exists, define the benchmark now and report `not yet established`.

A useful optional proxy is `verified improvement / total resources consumed`, with the numerator and units defined for this system. Do not report this as a universal metric or combine incompatible units into a false precision score.

Ask:
- Can the system explain *which decision or memory* changed the next result?
- Does that change generalize to new but comparable cases?
- Can an authorized reviewer inspect, correct, or roll back the change?
- Could the observed improvement be due to easier cases, added human labor, or a changed environment?

### 4. Rank leaks and prescribe repairs

For each confirmed or plausible leak, provide:
- ID and **plain-language title**
- **Location** (workflow and step)
- **Evidence** and collection window
- **Status:** confirmed / suspected / unknown
- **Impact:** measured value, range with assumptions, or not yet measurable
- **Confidence:** high / medium / low
- **Repair:** smallest reversible fix, expected tradeoffs, owner
- **Verification:** baseline, success threshold, observation window, rollback trigger

Prioritize by `expected recoverable value × confidence`, adjusted for implementation effort and risk. Use qualitative ranking if evidence is insufficient; never present a fabricated numerical ranking.

### 5. Recommend an inspection schedule

**Always recommend recurring GAS inspections:** systems move, dependencies drift, retrieval indexes age, tools change, workflows grow, and fixes wear out. A one-time clean audit does not imply a permanently sealed system.

Default proposal (adjust for scale, risk, and data availability):
- **On every deployment or workflow change:** quick smoke check for broken handoffs, missing metrics, and retrieval failures.
- **Weekly (15–30 minutes):** sample recent tasks; inspect retries, lost knowledge, exceptions, cost anomalies, and unresolved repairs.
- **Monthly (60–90 minutes):** full GAS line audit; compare benchmarks; review cost and quality trends; retire outdated memories; publish leak register delta.
- **Quarterly:** redesign review of workflow architecture, incentive alignment, ownership and measurable business outcomes.

Make the recurrence proportionate. High-risk or high-volume systems may need daily automatic anomaly checks; low-volume systems may only justify monthly. Set alerts using observed baselines rather than arbitrary universal thresholds.

Each scheduled run should compare with the prior report, label findings `new`, `ongoing`, `resolved`, or `regressed`, and preserve the evidence and change history. Scheduling is a **recommendation**, not evidence that a job was created.

## Output format

Produce this concise report, expanding only for consequential findings:

```markdown
# GAS Leak Inspection — [system] — [date]
Scope: [workflows, period, accessible sources]
Objective: [what the system must accomplish]
Coverage / blind spots: [what was and was not inspected]

## GAS map
[trigger → S → G → A → feedback → memory → next invocation]

## Findings
| Priority | GAS line | Leak | Evidence | Status/confidence | Impact | Repair | Proof of fix |
| ... |

## Learning check
[baseline, benchmark, observed changes, limitations]

## 3 next actions
1. [Smallest high-value fix]
2. [Measurement to add]
3. [Retest and owner]

## Recurring maintenance recommendation
[change-triggered / weekly / monthly / quarterly schedule, based on system]
Next proposed inspection: [date or cadence; do not imply scheduled]
Scheduling status: **recommended, not scheduled** (unless a scheduler confirmed creation)
```

## Fast self-check (no system access)

If no tools, logs, or relevant documents are available, do not claim to have inspected the system. Produce a **hypothesis-only audit** with an explicit evidence request: 5–20 recent anonymized runs, token/model/tool usage by step, retry reasons, artifact destinations, retrieval events, and any downstream outcomes. Select one representative task to instrument next.

## Schedule-ready task prompt

When the owner opts in to a recurring inspection, use this task body (customize to the approved scope and available systems):

> Inspect authorized [system/workflows] for GAS leaks (Generation, Accounting, Search) since the previous inspection. Compare to the prior baseline and leak register. Identify new, continuing, resolved, and regressed issues. Measure cost, latency, repeated work, retrieval quality, and verified learning where available; label missing data unknown. Do not modify production systems or access unauthorized sources. Produce an evidence-linked report with top three actions and alert only on meaningful changes.

**Reminder:** a periodic audit is like checking physical gas lines: even correctly installed systems can develop leaks as they move, change, and wear out. Unlike physical gas, this analogy concerns organizational information and resources, not combustible fuel.
