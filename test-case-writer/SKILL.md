---
name: test-case-writer
description: Use when someone asks to generate test cases, write test cases from a user story, create test cases from a BRD, design test cases from a mockup or wireframe, or produce a test case table from requirements.
argument-hint: [feature name or requirement ID]
disable-model-invocation: true
---

# Test Case Writer

Generates complete, execution-ready, traceable test cases from any combination of:
- User stories
- Business Requirements Documents (BRDs)
- UI mockups or wireframes
- Forms and templates
- Workflows
- Plain-language feature descriptions

---

## Before You Start

Read every input document the user provides. Do NOT generate test cases until you have reviewed all available inputs. Look for:

- Field names, labels, buttons, dropdowns, and validation rules
- Navigation paths and screen transitions
- Role-based access rules
- Error messages and system feedback
- Business rules, decision points, and dependencies

If a piece of behavior is defined anywhere in the inputs, use it. Do not raise questions about documented behavior.

If critical information is genuinely missing (e.g., no validation rules, no role info), list your assumptions in the Summary Section at the end.

---

## Step-by-Step Workflow

**Step 1: Inventory the inputs**

List what the user has provided:
- User story? Note the story ID and acceptance criteria.
- BRD? Note the section headings and functional rules.
- Mockup/wireframe? Extract all fields, labels, buttons, and navigation flows.
- Form/template? Extract field names, types, mandatory rules, and validation logic.

**Step 2: Map all test paths**

Before writing a single test case, map out every path you need to cover:

- Primary (happy path): the normal, successful flow
- Alternate flows: valid but non-default paths
- Error handling: invalid inputs, missing required fields, system failures
- Edge and boundary conditions: min/max values, empty states, character limits
- Role-based access: what each role can see, do, or be blocked from

Do not skip any branch. Every decision point in the requirements must appear in at least one test case.

**Step 3: Generate the test case table**

Output all test cases in a single consolidated markdown table with these exact columns:

| Test ID | Test Case Name | Creation Date | Designer | Equivalence | Priority | Purpose | Pre-Conditions | Test Data | Category | Step No. | Description | Expected Result |

Column rules:

- **Test ID**: Sequential. Format: TC-001, TC-002, etc.
- **Test Case Name**: Short, descriptive. Follows pattern: [Action] + [Object] + [Condition]. Example: "Submit Login Form with Valid Credentials"
- **Creation Date**: Use today's date in DD-MMM-YYYY format
- **Designer**: Leave as `[Your Name]` so the user can replace it
- **Equivalence**: The equivalence partition this case belongs to. Example: Valid Input, Invalid Input, Boundary Value
- **Priority**: High / Medium / Low
- **Purpose**: One sentence. What business rule or requirement does this test validate?
- **Pre-Conditions**: What must be true before this test runs? List each condition on a separate line within the cell.
- **Test Data**: Exact values. No placeholders. Include: user role, field values, boundary values, reference data. Populate only in the first row of each multi-step test case.
- **Category**: One of: Primary Workflow / Alternate Flow / Error Handling / Edge & Boundary / Role-Based Access
- **Step No.**: Sequential within each test case. Restart at 1 for each new test case.
- **Description**: See Step Detail Rules below.
- **Expected Result**: See Expected Result Rules below.

---

## Step Detail Rules

Every step must be executable by a new tester with zero context. For each step:

- Say exactly where the user is: the page or screen name
- Say exactly what to click: put the button or link name in "double quotes"
- Say exactly what to type or select: put values in 'single quotes'
- For dropdowns: say how to open it, then what value to select
- For navigation: write it as Home > Module > Screen
- For keyboard actions: write in ALL CAPS (ENTER, TAB, ESCAPE)
- Include wait instructions only when needed: "Wait until the page finishes loading and the spinner disappears."

Never write vague steps like:
- "Verify it works"
- "Check the page"
- "Perform the required actions"

---

## Expected Result Rules

Every Expected Result must be:

- Single-outcome: one thing happens, stated clearly
- Observable: something visible, measurable, or verifiable
- Free of "or", "and/or", "may", "might", "should be able to"

Each Expected Result must state at least one of:
- What is displayed (exact message text, field value, status label)
- What changed (record created, status updated, email sent)
- What did not happen (save blocked, button disabled, field hidden)

If multiple outcomes are possible, write them as separate test cases.

Good examples:
- "A success toast appears with the message: 'Record saved successfully.'"
- "The 'Status' field updates to 'Approved'."
- "The system blocks submission and displays: 'Email address is required.'"

Bad examples:
- "User is redirected or sees a confirmation."
- "System saves or shows a validation message."

---

## Test Case Categories (Required Coverage)

Your output must include test cases across all applicable categories:

| Category | What to Cover |
|---|---|
| Primary Workflow | The successful, end-to-end happy path |
| Alternate Flow | Valid but non-default paths (e.g., optional fields skipped) |
| Error Handling | Invalid inputs, missing required fields, system-level errors |
| Edge & Boundary | Min/max values, empty states, character limits, zero-state screens |
| Role-Based Access | What each role can see, edit, submit, or is blocked from |

---

## Test Data Rules

- Never use placeholders like `<email>` or `[name]`. Use actual values: 'john.doe@example.com', 'John Doe'
- Always specify the user role in the test data
- For boundary tests: specify the exact boundary value (e.g., '255 characters', '0', '-1', 'null')
- For dropdown/reference fields: specify the exact option to select (e.g., 'Active', 'Pending Review')
- For multi-step test cases: populate Test Data only in the first row of the test case

---

## Summary Section (Mandatory)

After the test case table, output this summary block:

```
## Test Case Summary

**Total Test Cases Generated:** [N]

**Breakdown by Category:**
- Primary Workflow: [N]
- Alternate Flow: [N]
- Error Handling: [N]
- Edge & Boundary: [N]
- Role-Based Access: [N]

**Requirements / User Stories Covered:**
- [Story ID or Requirement ID]: Covered by TC-XXX, TC-XXX

**Coverage Confirmation:**
All primary, alternate, error, edge, and role-based paths have been tested.

**Assumptions Made:**
- [List any assumption where documentation was missing or ambiguous in mumbered format]
- [If no assumptions, write: "None. All behavior derived from provided inputs."]
```

---

## What This Skill Does NOT Do

- Does not generate test cases from memory or guesswork when inputs are missing
- Does not combine multiple outcomes into a single Expected Result
- Does not use vague step language
- Does not skip the Summary Section
- Does not use placeholders in Test Data

---

## Supporting Files

This skill works standalone. For projects using this skill repeatedly, consider adding to the same directory:

- `examples/` -- Sample outputs for common feature types (login, CRUD forms, role-based dashboards)
- `templates/field-validation.md` -- Pre-mapped boundary conditions for common field types
- `templates/role-matrix.md` -- Role access mapping template to fill before running the skill
