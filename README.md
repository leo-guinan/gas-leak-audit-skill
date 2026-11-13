# GAS Leak Audit

A reusable Hermes skill for finding measurable losses across Generation, Accounting, and Search (GAS): repeated or unused work, unmeasured costs and outcomes, knowledge that cannot be retrieved, and feedback loops that do not produce demonstrated improvement.

## What it does

The skill guides an evidence-bounded, read-only audit of an AI agent, workflow, repository, or organization. It maps how work moves from a trigger through search, generation, accounting, feedback, and reusable memory; checks for specific leak patterns; distinguishes observations from estimates and hypotheses; and produces a prioritized leak register with repairs and verification criteria.

It also checks whether the system actually learned. Stored notes or more activity do not count as learning by themselves: improvement must be demonstrated on comparable tasks, with quality, cost, time, human effort, and limitations considered.

## Repository contents

- `SKILL.md` — the complete skill instructions, audit procedure, report template, and schedule-ready prompt.
- `references/example-report.md` — an illustrative example report. Its scenario and numbers are fictional, not measured evidence.

## Use with Hermes Agent

Install the skill by placing the `gas-leak-audit` directory in a Hermes skills directory, for example:

```text
~/.hermes/skills/gas-leak-audit/SKILL.md
~/.hermes/skills/gas-leak-audit/references/example-report.md
```

For a named Hermes profile, use that profile's skills directory instead. Then start a new session or reset the current session, and load the skill by name (for example, `/skill gas-leak-audit`). Hermes documentation: <https://hermes-agent.nousresearch.com/docs/>

You can also use the skill as a standalone audit checklist: read `SKILL.md`, define a bounded inspection scope, and follow its report format.

## Safety and evidence boundaries

The audit is read-only by default. It does not authorize production changes, access to private data, external disclosure, or creation of recurring jobs. Missing telemetry must be labeled `unknown`; no cost, savings, baseline, or learning claim should be invented. The skill prioritizes user outcomes and quality—not token reduction for its own sake—and requires evidence, confidence, tradeoffs, and a falsifier for findings.

The example report is explicitly fictional and must not be cited as evidence about a real organization.

## Scope and limitations

An audit can only assess sources the operator is authorized to inspect and that are actually accessible. It is not a security certification, financial audit, or proof that a system is safe or efficient. Recommendations are hypotheses until verified against an agreed baseline and observation window.

## License

No license is currently included. Unless a license is added, the contents remain under their applicable copyright; public availability does not grant permission to reuse, modify, or redistribute them.
