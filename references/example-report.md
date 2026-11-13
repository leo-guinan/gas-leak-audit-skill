# GAS Leak Inspection — Customer quoting workflow — example (fictional)

> Illustrative only. Numbers and incidents below are not observations about a real business.

Scope: Sample of 20 anonymized quotes over a month. Objective: accurate quotes with reduced staff time.
Coverage / blind spots: Quote log and approved knowledge base visible; no access to payroll or customer revenue outcomes.

## GAS map
Customer request → search customer history and supplier catalog → draft quote → manager checks price and scope → sent quote → follow-up → approved examples stored in knowledge base.

## Findings
| Priority | GAS line | Leak | Evidence | Status/confidence | Impact | Repair | Proof of fix |
|---|---|---|---|---|---|---|---|
| High | S/X | Prior solutions not indexed | 6 of 20 sampled quotes repeated manual lookup of a resolved case | Confirmed / high | Time impact unknown until timed | Link approved examples by product/task, preserving version and reviewer | Next 20 comparable quotes show fewer repeated lookups without more corrections |
| Medium | A | Missing review duration | Review start/end missing for 18 of 20 samples | Confirmed / high | Unknown | Add two timestamps, no content capture | At least 95% of sampled quotes include timings |
| Low | G | Potential template regeneration | Similar quote drafts seen, but requirements differ | Suspected / low | Unknown | Compare quote templates to customer requirements before automating | Review identifies safe reuse cases without quality loss |

## Learning check
Baseline not established for quality-adjusted completion time. Begin a comparable-task benchmark; do not infer savings yet.

## 3 next actions
1. Index approved historical quote examples with provenance.
2. Instrument review time and corrections.
3. Recheck 20 comparable quotes after the change.

## Recurring maintenance recommendation
Weekly 15-minute sample and monthly full review; re-run after catalog/schema changes.
Next proposed inspection: next week.
Scheduling status: **recommended, not scheduled**.
