# test-case-writer

A Claude Code skill that generates complete, execution-ready test cases from user stories, BRDs, UI mockups, wireframes, and plain-language feature descriptions.

Built by a practitioner with 26 years of enterprise QA experience. This is not a generic AI prompt. It's an opinionated, structured workflow that produces test cases a real tester can actually execute.

---

## What It Produces

A single consolidated markdown table covering:

- Primary (happy path) workflows
- Alternate flows
- Error handling scenarios
- Edge and boundary conditions
- Role-based access variations

Plus a mandatory Summary Section with coverage confirmation, requirement traceability, and documented assumptions.

---

## Who This Is For

- QA engineers who want consistent, repeatable test case generation inside Claude Code
- Teams tired of half-baked AI test output that misses error paths and edge cases
- Leads who need traceable test cases mapped back to user stories or BRDs

---

## Installation

1. Copy the `test-case-writer/` folder into your project's `.claude/skills/` directory:

```
your-project/
  .claude/
    skills/
      test-case-writer/
        SKILL.md
```

2. Optionally add a reference in your project's `CLAUDE.md`:

```
## Available Skills

- `/test-case-writer` -- Generates test cases from user stories, BRDs, mockups, or feature descriptions
```

3. That's it. Claude Code will detect the skill automatically.

---

## How to Use

**Option 1: Natural language trigger**

```
Generate test cases for the login feature from this user story: [paste story]
```

```
Write test cases from this BRD section: [paste content]
```

```
Create a test case table from this wireframe description: [paste description]
```

**Option 2: Direct invocation**

```
/test-case-writer Login Feature - Sprint 4
```

---

## Input Options

You can provide any combination of:

| Input Type | Example |
|---|---|
| User story | "As a user, I want to reset my password so that..." |
| BRD section | Pasted functional requirements text |
| UI mockup description | Field names, labels, buttons, validation rules |
| Wireframe notes | Navigation flows, screen transitions, dynamic states |
| Plain feature description | "The checkout page has a promo code field that validates against active codes" |

The more detail you provide, the better the coverage. The skill will tell you what assumptions it made when input was incomplete.

---

## Output Format

```
| Test ID | Test Case Name | Creation Date | Designer | Equivalence | Priority | Purpose | Pre-Conditions | Test Data | Category | Step No. | Description | Expected Result |
```

Followed by a Summary Section with:
- Total test cases count
- Breakdown by category
- Requirement traceability
- Assumptions made

---

## Design Principles

**Steps are layman-executable.** Every step says exactly where you are, what to click, and what to enter. No interpretation required.

**Expected Results are single-outcome.** No "or" conditions. No "may". One thing, stated clearly, that a tester can verify without judgment.

**Test Data is always explicit.** No placeholders. Real values, real roles, real boundary numbers.

**Coverage is mandatory.** The skill will not stop at happy path. Every error path, edge case, and role variation gets covered.

---

## Contributing

Issues and PRs welcome. If you find a gap in coverage logic or a case type the skill handles poorly, open an issue with an example and expected behavior.

---

## License

MIT. Use it, fork it, build on it.

---

## Author

Built by [Georgy Ukkuru](https://testmetry.com) -- Practice Director, Quality Engineering at Speridian Technologies. 26 years in enterprise QA. Writing and speaking about AI in testing at [testmetry.com](https://testmetry.com).
