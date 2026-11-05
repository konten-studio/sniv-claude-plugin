# sniv for Claude

sniv reads a brand from the outside, like a stranger would. It looks at the public side of Instagram, TikTok, Facebook, Threads, YouTube, and LinkedIn. It scores the account from 0 to 100 and names the one bottleneck and the one fix. Every number in a report comes from a computed metric with a source and a date.

This plugin connects Claude to the sniv MCP server and adds three skills that teach Claude how to use it well.

## Install

In the Claude apps, find sniv in the plugin directory and add it.

In Claude Code, you can also install it from this repository:

```
/plugin marketplace add konten-studio/sniv-claude-plugin
/plugin install sniv@sniv
```

## What the plugin contains

| Part | What it does |
|------|--------------|
| MCP server `sniv` | Connects to `https://mcp.sniv.social/mcp`. You sign in with your sniv account. |
| Skill `read-brand` | Runs a read of a brand, asks before it spends credits, and presents the score, the bottleneck, and the steps. |
| Skill `compare-rivals` | Compares a brand with up to 4 rivals on one platform. |
| Skill `plan-from-report` | Turns a finished report into a weekly plan, a content calendar, or a brief. |

The plugin has no scripts, no hooks, and no local code. It runs nothing on your computer.

## MCP tools

| Tool | What it does | Credits |
|------|--------------|---------|
| `read_brand` | The daily free read, or a paid read (extra, full, no account, re-read) | 0 for the free read. Paid reads show the price first. |
| `compare_rivals` | A brand against up to 4 rivals on one platform | 3 |
| `get_report` | Status and content of a report | 0 |
| `list_findings` | Ranked findings and next steps of a finished report | 0 |
| `get_wallet` | Balance, held credits, daily limit, free reads left today | 0 |

A paid tool returns the price first and spends nothing until you say yes.

## Before you start

1. Install the plugin.
2. When Claude asks, sign in with your sniv account. Google or an email link both work. The account is free.
3. Approve the connection. It can spend up to 40 credits a day. You can change that limit at [app.sniv.social/mcp](https://app.sniv.social/mcp).

Every account gets 1 free read a day. Your first connection adds 10 welcome credits, once per account. 1 credit = $1, and credits never expire. Top up at [app.sniv.social/wallet](https://app.sniv.social/wallet).

## Example prompts

- "Read @yourbrand on Instagram. What holds it back?"
- "Compare @yourbrand with @rival1 and @rival2 on TikTok."
- "How many credits do I have?"
- "Show the findings of my last sniv report."
- "Turn my sniv report into a plan for this week."

## What the plugin sends and fetches

- The plugin talks only to `https://mcp.sniv.social/mcp`. It sends nothing to any other address.
- Claude sends sniv only the inputs of each tool call: a handle or a profile link, the platform, the goal, rival handles, a website, and report ids.
- sniv does not read your chat, your files, or your memory in Claude.
- sniv reads only public data on the social platforms. It never asks for a social media password.
- sniv keeps your reports, your credit history, and the name, daily limit, and last use of each connection. See the [privacy policy](https://sniv.social/privacy).

## Turn it off

Open [app.sniv.social/mcp](https://app.sniv.social/mcp) and turn off the connection. You can also remove the plugin in Claude.

## Links

- Docs: [sniv.social/docs/mcp](https://sniv.social/docs/mcp)
- Privacy: [sniv.social/privacy](https://sniv.social/privacy)
- Terms: [sniv.social/terms](https://sniv.social/terms)
- Support: [read@sniv.social](mailto:read@sniv.social)

## License

MIT. See [LICENSE](LICENSE).
