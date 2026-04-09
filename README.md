QA teams waste hours writing test cases, analyzing defect reports, and building test plans from scratch. This repository gives you Claude Code skills that do that work in minutes. Built by a QA practitioner with 26 years of enterprise testing experience, not by a vendor trying to sell you a platform.

What Is This Repository?
testmetry-skills is a growing collection of Claude Code skills purpose-built for software quality engineering. Each skill is a drop-in instruction set that tells Claude exactly how to handle a specific QA task, from generating traceable test cases to running full defect metric analysis.
These are not generic AI prompts. Every skill reflects real practitioner logic, uses defined formulas, handles missing data gracefully, and produces output a working QA team can actually use.

Available Skills
SkillWhat It DoesInputtest-case-writerGenerates complete, traceable test cases with step-by-step instructions and single-outcome expected resultsUser stories, BRDs, mockups, wireframesdefect-analyzerAnalyzes defect reports across 14 dimensions including Pareto root cause, leakage ratio, reopen rate, and rejection rateCSV or Excel defect export
More skills in progress. See the roadmap below.

Who Uses These Skills

QA engineers who need consistent, repeatable output without rewriting prompts every session
Test leads and architects who want traceable test cases mapped to requirements without doing it manually
QA managers who need defect metrics and recommendations they can take straight into a review meeting
Teams running Claude Code who want specialist QA capability built directly into their workflow


Quick Start
Step 1: Install Claude Code
If you do not have Claude Code set up, follow the official installation guide.
Step 2: Add a skill to your project
Copy the skill folder you want into your project's .claude/skills/ directory:
your-project/
  .claude/
    skills/
      test-case-writer/
        SKILL.md
        README.md
        examples/
Step 3: Trigger the skill
Natural language:
Generate test cases for the checkout feature from this user story: [paste story]
Analyze this defect report [attach CSV file]
Direct slash command:
/test-case-writer
/defect-analyzer
That is it. No configuration. No API keys. No setup beyond dropping the folder in.

Skill Design Principles

Every skill in this repository follows the same rules:
No placeholders in output. Test data uses real values. Formulas use real numbers. You get something you can act on, not a template to fill in later.
Graceful field handling. Skills work with whatever data you provide. Missing fields are skipped cleanly, not hallucinated.
Defined formulas, not estimates. Defect rejection rate, reopen rate, and leakage ratio all use the exact formulas documented in each skill's README.
Layman-executable steps. Test case steps are written so a new tester can follow them without interpretation. Every step names the screen, the button, and the exact value to enter.
Single-outcome expected results. No "or" conditions. No "may". One observable outcome per expected result.

Skill Roadmap
Skills planned for this repository, in build order:

test-estimation-calculator - Effort estimation for test activities based on scope, complexity, and team capacity
bug-report-writer - Converts rough tester notes into complete, reproducible bug reports
test-plan-writer - Generates structured test plans from project briefs or sprint goals
regression-suite-builder - Identifies regression scope from release notes or change descriptions
acceptance-criteria-reviewer - Reviews user stories for testability gaps before development starts
api-test-case-writer - Generates test cases from REST API specs and OpenAPI/Swagger docs
automation-candidate-picker - Recommends which test cases are worth automating and why

Watch the repo or check testmetry.com for updates when new skills drop.

Repository Structure
testmetry-skills/
  test-case-writer/
    SKILL.md           # The Claude Code skill file
    README.md          # Installation, usage, and output format
    examples/          # Sample outputs so you know what to expect
  defect-analyzer/
    SKILL.md
    README.md
    examples/
Each skill is self-contained. Install only what you need.

Contributing
Found a gap in coverage logic? A field type the skill handles poorly? A QA scenario that produces bad output?
Open an issue with:

The input you provided
The output you got
What you expected instead

Pull requests welcome. If you are building a skill that fits the QA practitioner scope of this repo, open an issue first to discuss before building.

Keywords
claude code skills, qa automation, test case generation, defect analysis, software testing ai, claude code qa, test case writer, defect metrics, quality engineering, test automation tools, ai testing, software quality, jira defect analysis, test plan generator, claude code plugins

License
MIT. Use it, fork it, build on it. If you publish work built on these skills, a link back to this repo or testmetry.com is appreciated but not required.

Built by Georgy Ukkuru -26 years in enterprise QA. Writing and speaking about AI in testing at conferences including Automation Guild, TestFlix, and BrowserStack summits.
