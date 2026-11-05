---
name: plan-from-report
description: Use when the user has a finished sniv report and wants to act on it, for example a weekly content plan, post ideas, a brief for a designer or an agency, or a check of progress against the report's targets. Opens the report with the sniv tools and builds the plan only from its findings, steps, targets, and unlocked sections.
---

# Turn a sniv report into a plan

A sniv report names one bottleneck and the steps to fix it. This skill turns those steps into work the user can do this week. It spends no credits unless the user asks for a re-read.

## Tools in this skill

| Tool | Use it to | Credits |
|------|-----------|---------|
| `list_findings` | Get the ranked findings and the steps | 0 |
| `get_report` | Open all unlocked sections | 0 |
| `read_brand` with `kind: "reread"` | Measure change after the plan | 9 |

## Steps

1. Get the `report_id`. Use the last report in this conversation, or ask the user for it. The user can find it in their reports on sniv.
2. Call `list_findings` for the findings and steps.
3. Call `get_report` for the unlocked sections. A full report can include:
   - `direction`: positioning, audience, content pillars, formats, cadence, and the role of each platform.
   - `kpis_plan`: KPIs with a baseline and a target, and a week-by-week plan.
   - `first_posts`: 5 post hooks with format, platform, and why.
   - `copy_account`: one account to learn from, what to copy, and what not to copy.
4. Build the output that the user asks for. Use the structures below.

## Outputs

- **This week's plan**: 3 to 5 tasks. Tie each task to one step or finding of the report.
- **Content calendar**: use `cadence`, `formats`, `pillars`, and `first_posts`. Do not add more posts a week than the report's cadence.
- **Brief for a designer or an agency**: the bottleneck, the target KPIs, the account to copy, and the first 5 posts.
- **Progress check**: compare the user's new numbers with the report's `baseline` and `target`. Offer a re-read for 9 credits to get new numbers from sniv. Ask for a yes before you call `read_brand` with `confirm: true`.

## Rules

- Each item in the plan names the finding or step it comes from.
- Use only the numbers in the report. Do not invent baselines, targets, or results.
- On a free report, the plan can use only the verdict and step 1. Say that a full report adds the direction, the 30-day plan, and the first 5 posts.
- Do not spend credits without a clear yes from the user.
