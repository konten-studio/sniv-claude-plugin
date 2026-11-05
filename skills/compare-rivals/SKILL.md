---
name: compare-rivals
description: Use when the user wants to compare a brand's social media with up to 4 competitors or rivals on one platform, asks which rival does better, or asks which account to learn from. Runs the sniv compare_rivals tool after the user accepts the price, then presents the comparison from the report.
---

# Compare a brand with its rivals

sniv compares one brand with 1 to 4 rival accounts on one platform. It uses public data only. A comparison costs 3 credits. 1 credit = $1.

## Tools in this skill

| Tool | Use it to | Credits |
|------|-----------|---------|
| `compare_rivals` | Start a comparison | 3 |
| `get_report` | Follow the comparison and open it | 0 |
| `get_wallet` | Show the balance | 0 |

## Steps

1. Get the brand handle, the platform, and 1 to 4 rival handles.
   - All accounts must be on the same platform: `instagram`, `tiktok`, `facebook`, `threads`, `youtube`, or `linkedin`.
   - If the user has no rivals in mind, ask for them. A full read with the `read-brand` skill also finds rivals.
2. Call `compare_rivals` without `confirm`. The tool returns the price and the balance and spends nothing.
3. Show the price and the balance in one sentence. Call `compare_rivals` again with `confirm: true` only after the user says yes in this conversation.
4. Call `get_report` with the `report_id` and `wait_seconds: 25`. Repeat while `status` is `queued` or `running`.
5. Present the result when `status` is `done` or `partial`.

## Present the comparison

1. The brand's score and headline from the verdict section.
2. A table of the rivals from the `rivals` section: handle, followers, engagement rate (`er`), and why sniv picked the account. Copy the values as the report gives them.
3. The rival that leads, and the one thing the brand can learn from it. Use only what the report says.
4. The date of the data and any accounts that sniv could not read.

## Rules

- Use only the numbers in the tool results. Do not estimate a rival's numbers.
- Do not spend credits without a clear yes from the user.
- sniv reads public accounts only. If a rival is private or opted out, say so and continue with the others.
- If the balance is too low, give the user the `topup_url` from the result.
