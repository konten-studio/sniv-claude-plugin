---
name: read-brand
description: Use when the user wants an outside read, audit, score, or diagnosis of a brand's public social media on Instagram, TikTok, Facebook, Threads, YouTube, or LinkedIn. Also use when the user pastes a handle or a profile link and asks what holds the brand back. Runs the read with the sniv tools and presents the score, the one bottleneck, and the next steps.
---

# Read a brand with sniv

sniv reads a brand from the outside, like a stranger would. It uses public data only. It scores the account from 0 to 100 and names the one bottleneck: reach, engagement, or conversion. Every number in a report comes from a computed metric with a source and a date.

## Tools in this skill

| Tool | Use it to | Credits |
|------|-----------|---------|
| `read_brand` | Start a read | 0 for `free`, else see the table below |
| `get_report` | Follow a read and open the finished report | 0 |
| `list_findings` | Get the ranked findings and steps of a finished report | 0 |
| `get_wallet` | Show the balance and the free reads left today | 0 |

## Read kinds

| `kind` | Credits | What the user gets |
|--------|---------|--------------------|
| `free` | 0 | 1 a day per account. 1 platform. Score, one finding, step 1, and one hook from the brand's best post. About 60 seconds. |
| `extra` | 1 | The same as `free`, after the free read of the day is used. |
| `full` | 19 | Up to 6 platforms. Sections 00 to 10: verdict, presence and funnel, the one bottleneck, platform audit, visual and voice, the account to copy, rivals, direction, KPIs and a 30-day plan, the first 5 posts, method and limits. A few minutes. sniv also sends an email. |
| `noacct` | 19 | A brand with no social account. Give its `website`. |
| `reread` | 9 | A new read of an earlier report. Give `parent_report_id`. Use it to measure change. |

1 credit = $1. Credits never expire.

## Steps

1. Get the handle and the platform.
   - Accept `@handle`, a profile link, or a website.
   - A profile link tells the platform. For a bare handle with no platform, ask the user which platform.
   - If the brand has no social account, use `kind: "noacct"` with `website`.
2. Set `goal` only when the user names one: `sales`, `awareness`, `leads`, `community`, or `hiring`.
3. Pick the kind. Start with `free` unless the user asks for more.
4. For a paid kind, call `read_brand` without `confirm` first. The tool returns the price and the balance and spends nothing.
   - Show the user the price and the balance in one sentence.
   - Call `read_brand` again with `confirm: true` only after the user says yes in this conversation.
   - If `enough` is false, give the user the `topup_url` from the result.
5. Follow the read. Call `get_report` with the `report_id` and `wait_seconds: 25`.
   - Repeat while `status` is `queued` or `running`. Give the user one short line of progress between calls.
   - A full report can take a few minutes. After about 8 calls, offer to check again later.
6. Present the report when `status` is `done` or `partial`. Use the order below.

## Present the report

1. The score out of 100 and the headline.
2. The one bottleneck, when the report has it.
3. The findings. Keep each number, source, and date exactly as the report gives them.
4. The steps: the step, why, and the target.
5. On a `free` read, name the locked sections in one line. Say once that a full report opens them for 19 credits. Do not repeat the offer.
6. On a `partial` read, name the platforms that sniv could not read and the credits that came back (`refunded`).
7. The date of the data (`data_as_of`).

## Rules

- Use only the numbers in the tool results. Do not round, recompute, or add a number that the report does not have.
- Do not spend credits without a clear yes from the user for that read. Never set `confirm: true` on the first call of a paid kind.
- sniv reads public data only. Never ask the user for a social media password.
- If sniv refuses a handle because its owner opted out, tell the user. Do not try another way to read that account.
- A locked section stays locked. Do not guess what it says.

## Errors

| Result | Tell the user |
|--------|---------------|
| `insufficient_credits` | The read costs more than the balance. Give the `topup_url`. |
| `not_found` | sniv found no report with that id on this account. |
| `failed` status | The read did not finish. sniv returned the held credits. |
| Too many calls | Wait one minute, then try again. |
| Connection turned off | Connect sniv again in the AI app. |
