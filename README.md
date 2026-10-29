# aicoo for your agent

[aicoo](https://www.aicoo.io) is where a small team keeps its docs, to-dos and
meetings, with an AI teammate. This repo lets your own agent (Claude Code,
Codex, Cursor, OpenClaw, OpenHands, …) work in your aicoo as you.

## Start: paste one line into your agent

```
Read https://www.aicoo.io/skill.md and connect me to aicoo.
```

Your agent reads the skill, runs `npx -y @aicoo/cli@latest login`, and gives
you a link. Open it, press **Allow**, and you're connected. Then it runs
`npx -y @aicoo/cli@latest setup`, so new sessions already know aicoo.

Try: "What's on my plate today?", "Turn yesterday's meeting into to-dos",
"Save what we did in this session as a doc."

## Or install it yourself

**Claude Code plugin** (skill + MCP server):

```
/plugin marketplace add systemind-team/aicoo-skills-v2
/plugin install aicoo@aicoo
```

Then ask Claude to connect you to aicoo; the first time, it runs the login.

**Skills only** (any agent that reads `SKILL.md`): `npx skills add systemind-team/aicoo-skills-v2`

**MCP server** for any MCP client: command `npx`, args `-y @aicoo/cli@latest mcp`.
Log in once with `npx -y @aicoo/cli@latest login`; the token stays in
`~/.aicoo/credentials.json` and is never written into client configs.

## What your agent can do

- See what's due, open and new: `today`, `news`
- Find and read docs, list to-dos and meetings
- Work with full tables through the Aicoo web UI when the connected API does not support structured-table edits; preserve field types, formulas and linked form settings
- Add, change and finish to-dos; write new docs
- Read your team chats, and send a message as you: it shows you the exact text and the chat first, sends only after your yes, and the message shows "via" the agent
- **Edit an existing doc**: it shows you the change in chat first and applies
  it only after you say yes. Every edit can be undone, in chat or in aicoo.

It acts as you and sees only what you can see. Everything it writes shows in
aicoo as yours, "via" the agent. Disconnect it any time in aicoo under
**Agents → Connected agents**, or with `npx -y @aicoo/cli@latest logout`.

## What's here

| Path | What |
|---|---|
| `skills/aicoo/SKILL.md` | The skill. Same text as https://www.aicoo.io/skill.md |
| `skills/aicoo/references/full-table.md` | Full-table capability checks and web UI editing workflow |
| `.claude-plugin/` | Claude Code plugin and marketplace manifests |
| `.mcp.json` | Registers the aicoo MCP server (`@aicoo/cli mcp`) |

The CLI is on npm as [`@aicoo/cli`](https://www.npmjs.com/package/@aicoo/cli).
Issues and ideas: [open an issue](https://github.com/systemind-team/aicoo-skills-v2/issues).

MIT © Systemind
