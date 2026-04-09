# defect-analyzer

A Claude Code skill that analyzes defect reports and produces actionable quality insights, metrics, and recommendations.

Drop in a CSV or Excel defect export. Get a full analysis covering defect concentration, root cause Pareto, resolution time, reopen rates, leakage ratios, rejection rates, business impact, and 7 data-grounded recommendations.

Built by a QA practitioner with 30 years of defect analysis experience. Every metric uses a defined formula. No generic advice.

---

## What It Analyzes

| Analysis | What You Get |
|---|---|
| High-Defect Areas | Top 5 components by defect count and % |
| Defect Introduction Phases | Where in the lifecycle defects are being created |
| Pareto: Root Causes | Which root causes drive 80% of defects |
| Open vs. Closed Trend | Closure rate vs. reporting rate over time |
| Severity and Priority | Distribution, mismatches, open criticals |
| Pattern and Trend | Recurring defects, release spikes, clusters |
| Resolution Time | Average fix time by severity, oldest open defects |
| Reopened Defects | Reopen rate, high-risk components and assignees |
| Documentation Quality | % of defects with adequate reproduction steps |
| Test Coverage Effectiveness | Phase distribution, escape rates to UAT/Production |
| Rejection Rate | Rejection Rate = Rejected / Total Reported x 100 |
| End-User Leakage | Leakage Ratio = (UAT + Prod) / Total x 100 |
| Business Impact | Plain-language risk summary for open criticals |
| Defect Type Distribution | Functional vs. Performance vs. Usability breakdown |
| Top 7 Recommendations | Data-grounded, actionable, ordered by impact |

---

## Installation

Copy the `defect-analyzer/` folder into your project's `.claude/skills/` directory:

```
your-project/
  .claude/
    skills/
      defect-analyzer/
        SKILL.md
```

Optionally add to your `CLAUDE.md`:

```
## Available Skills

- `/defect-analyzer` -- Analyzes defect reports and produces quality insights and recommendations
```

---

## How to Use

**Upload a file and trigger naturally:**

```
Analyze this defect report [attach file]
```

```
Run a defect analysis on the attached CSV
```

```
Here's our bug data from last sprint. What does it tell us? [attach file]
```

**Direct invocation:**

```
/defect-analyzer
```

The skill will prompt you to upload a file if none is provided.

---

## Accepted Input Formats

- CSV exports from Jira, Azure DevOps, TestRail, Zephyr, or any defect tracker
- Excel (.xlsx) defect logs
- Pasted tabular data

The skill works with whatever fields are present. Missing fields are handled gracefully. No field mapping required.

---

## Key Formulas Used

**Rejection Rate:**
```
Rejected Defects / Total Defects Reported x 100
```
Calculated from the Status field only.

**Reopen Rate:**
```
Total Reopened / Total Closed x 100
```
Flagged as a process risk above 10%.

**Leakage Ratio:**
```
(UAT Defects + Production Defects) / Total Defects x 100
```
Flagged as a pre-release testing gap above 20%.

---

## What Makes This Different

Most AI defect analysis prompts are generic. This skill:

- Uses defined formulas, not estimates
- Skips sections gracefully when fields are missing instead of hallucinating
- Flags specific thresholds (10% reopen rate, 15% rejection rate, 20% leakage)
- Produces recommendations tied to the actual data in your file, not boilerplate QA advice
- Handles files over 1,500 records with an upfront time estimate

---

## Part of testmetry-skills

This skill is part of the [testmetry-skills](https://github.com/testmetry/testmetry-skills) collection, a growing library of Claude Code skills for QA engineers. Built by practitioners, not vendors.

More QA frameworks, tools, and thinking at [testmetry.com](https://testmetry.com).

---

## License

MIT. Use it, fork it, build on it.
