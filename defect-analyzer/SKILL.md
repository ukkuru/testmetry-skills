---
name: defect-analyzer
description: Use when someone asks to analyze a defect report, analyze bug data, perform defect metrics analysis, review a defect log, or upload a defect file for quality insights.
argument-hint: [defect report file path or feature name]
disable-model-invocation: true
context: fork
---

# Defect Analyzer

Analyzes defect reports to produce actionable quality insights, metrics, and recommendations. Works with any defect data file (CSV, Excel, or pasted table) regardless of which fields are present.

---

## Step 1: File Check

If no file has been provided, respond with exactly this:

> "Please upload your defect report file to get started. Accepted formats: CSV, Excel (.xlsx), or a pasted data table. I'll analyze whatever fields are available."

Do not proceed until a file or data is provided.

---

## Step 2: Record Count Check

Before analysis, count the total number of defect records in the file.

If the record count exceeds 1,500:

> "This file contains [N] records. A thorough analysis of this size will take approximately [X] minutes. I'll work through it systematically and surface the most impactful insights."

Estimate time at roughly 1 minute per 300 records. Round up to the nearest minute.

Then proceed with the full analysis. Do not wait for user confirmation.

---

## Step 3: Field Inventory

Silently scan the file and identify which fields are present. Do not list or explain this to the user.

Common fields to look for (exact names will vary):

- Defect ID / Bug ID
- Title / Summary / Description
- Status (Open, Closed, Fixed, Rejected, Reopened, etc.)
- Severity (Critical, High, Medium, Low)
- Priority (P1, P2, P3, P4 or similar)
- Component / Module / Feature / Area
- Phase Found / Discovery Stage (Unit, Integration, System, UAT, Production)
- Root Cause / Root Cause Category
- Date Reported / Created Date / Opened Date
- Date Closed / Fixed Date / Resolved Date
- Defect Type (Functional, Performance, Usability, Security, etc.)
- Reported By / Found By (to identify UAT vs internal)
- Assigned To / Owner
- Reopened flag or Reopen Count
- Rejection reason / Resolution

Skip any analysis section that depends entirely on fields not present in the file. Do not mention skipped sections to the user.

---

## Step 4: Run the Analysis

Execute all applicable sections below. Output only insights and numbers. No methodology explanations. No "I calculated this by..." commentary.

---

### 4.1 High-Defect Areas

Identify the top 5 components, features, or modules by defect count. Present as a ranked table with count and percentage of total.

If component/module field is absent, skip this section.

---

### 4.2 Defect Introduction Phases

Show defect volume by discovery phase (Unit, Integration, System, UAT, Production). Identify which phase is producing the most defects. Flag if UAT or Production defects are disproportionately high relative to earlier phases.

If phase/discovery stage field is absent, skip this section.

---

### 4.3 Pareto Analysis: Root Causes

Identify the top root cause categories. Calculate cumulative percentage. Identify which root causes account for 80% of defects. Present as a table: Root Cause | Count | % | Cumulative %.

If root cause field is absent, skip this section.

---

### 4.4 Open vs. Closed Trend Analysis

Calculate:
- Total defects reported by time period (week or month, whichever the data supports)
- Total defects closed in the same period
- Net open defect movement (are open defects growing or shrinking?)
- Average gap in days between reported date and closed date

Flag if open defects are trending upward or if closure rate is falling behind the reporting rate.

If date fields are absent, skip this section.

---

### 4.5 Severity and Priority Assessment

Break down defects by Severity and by Priority. Calculate counts and percentages for each level. Flag any Critical or P1 defects that are still open. Identify mismatches where high severity defects carry low priority.

If severity or priority fields are absent, work with whichever one is present.

---

### 4.6 Pattern and Trend Identification

Look for:
- Recurring defects in the same component across releases or sprints
- Spikes in defect volume at specific time periods
- Clusters of the same defect type or root cause

Report patterns that are statistically significant, not noise.

---

### 4.7 Defect Resolution Time Analysis

Calculate:
- Average resolution time in days (Date Closed minus Date Reported)
- Resolution time by severity: are Critical defects being fixed faster than Low ones?
- Oldest open defects: list the top 5 by age in days

If date fields are absent, skip this section.

---

### 4.8 Reopened Defect Tracking

Calculate:
- Total defects reopened
- Reopen rate: (Total Reopened / Total Closed) x 100
- Components or assignees with the highest reopen rates

Flag reopen rates above 10% as a process risk.

If reopen data is absent, skip this section.

---

### 4.9 Documentation Quality Assessment

Sample up to 20 defect descriptions. Assess:
- Are steps to reproduce present?
- Are expected vs. actual results documented?
- Are environment details included?

Report the percentage of defects with adequate documentation. Flag if below 70%.

If description/summary field is too sparse to assess, skip this section.

---

### 4.10 Test Coverage Effectiveness

Show the distribution of defects found at each test phase. Calculate what percentage escaped to later phases (especially UAT and Production). A high percentage found in UAT or Production signals gaps in earlier test phases.

If phase data is absent, skip this section.

---

### 4.11 Defect Rejection Rate

Calculate using Status field only:

Rejection Rate = (Total Defects with Status = 'Rejected' / Total Defects Reported) x 100

Report the rate and flag if above 15% as a reporting accuracy concern.

Use only the Status field for this calculation. Do not infer rejection from other fields.

---

### 4.12 End-User Defect Leakage

Identify defects reported during UAT or post-release (Production). Calculate:

Leakage Ratio = (UAT + Production Defects / Total Defects) x 100

Flag leakage above 20% as a pre-release testing gap.

If phase or source field is absent, skip this section.

---

### 4.13 Business Impact Summary

For all open defects, assess combined business risk by:
- Counting open Critical and High severity defects
- Identifying which components they affect
- Estimating user-facing vs. internal impact where data allows

Provide a plain-language summary of the risk exposure, not a list of individual defects.

---

### 4.14 Defect Type Distribution

Break down defects by type (Functional, Performance, Usability, Security, etc.). Calculate count and percentage per type. Identify which type dominates and what it signals about testing focus gaps.

If defect type field is absent, skip this section.

---

## Step 5: Top 7 Recommendations

After completing all applicable analysis sections, output exactly 7 recommendations.

Rules:
- Every recommendation must be grounded in the data from the analysis above
- No generic QA advice. Every recommendation must reference specific numbers, components, or patterns found in this file
- Each recommendation must be actionable: state what to do, not just what the problem is
- Order by expected business impact, highest first

Format:

**Recommendation 1:** [Title]
[2-3 sentences: what the data shows, what action to take, what outcome to expect]

Repeat for all 7.

---

## Output Structure

Present the analysis in this order:

1. File Summary (record count, date range if available, fields detected that are relevant)
2. High-Defect Areas
3. Defect Introduction Phases
4. Pareto: Root Causes
5. Open vs. Closed Trend
6. Severity and Priority Assessment
7. Pattern and Trend Identification
8. Resolution Time Analysis
9. Reopened Defect Tracking
10. Documentation Quality
11. Test Coverage Effectiveness
12. Defect Rejection Rate
13. End-User Leakage
14. Business Impact Summary
15. Defect Type Distribution
16. Top 7 Recommendations

Skip any section where required fields are absent. Do not mention skipped sections.

---

## Hard Rules

- Do not ask for additional data mid-analysis. Work with what is provided.
- Do not explain analysis methodology or logic. Output insights and numbers only.
- Do not combine sections. Each section stands alone.
- All percentages must be calculated, not estimated.
- Reopen rate, rejection rate, and leakage ratio must use the exact formulas specified above.
- Accuracy of calculations is non-negotiable. Show the numbers used if a metric could be contested.
