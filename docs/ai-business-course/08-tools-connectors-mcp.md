# Module 08 — Tools, connectors and MCP

**Time:** 60 minutes
**Goal:** You can connect Claude to any piece of software you use, in the cheapest and safest way that works. You know the five-level hierarchy and when to use each level.

## 1. Why it matters

A model with no tools can only talk. A model with tools can read your inbox, update your CRM, query your sheet, and post to Slack. Tools are how agents "read and write to the company". Without them, there is no AI-native business.

## 2. The concepts

### 2.1 What a tool is

A tool is a function the model can call. "Search the web." "Read this file." "Send this email." The model decides when to call it, calls it, sees the result, and continues. The agent loop (module 11) is model + tools + repeat.

### 2.2 MCP: the plug standard

The Model Context Protocol is an open standard created by Anthropic for AI applications to connect to tools and data. Claude Academy calls it "USB-C for AI". An **MCP server** bundles all the actions of one tool into one package: for Airtable, that is dozens of actions (list bases, create record, update field...). Any MCP-compatible agent can use any MCP server. Claude, Codex, Cursor and others all speak it.

Every **connector** in Claude is an MCP server under the hood.

### 2.3 The five-level hierarchy

Ben's rule for how to give Claude access to a tool. Always start at the top. Go down only when the level above does not exist.

| Level | What | Cost | Reliability | When |
|-------|------|------|-------------|------|
| 1. **Native connector** | Built into Claude. Log in and go. | Low | High | Always first. Gmail, Drive, Calendar, Slack, Notion, GitHub, Linear, Asana, Attio, Fireflies, Apify, Clay... |
| 2. **Existing MCP server** | The vendor or community publishes one. | Low | High | Google "<tool> MCP server". Paste the URL as a custom connector. |
| 3. **Build your own MCP** | Ask Claude to write one. | Medium once | High after | The tool has an API but no MCP. Use for anything you touch often. |
| 4. **Browser use** | Claude drives Chrome. | High | Medium | One-off access. Tools with no API. |
| 5. **Computer use** | Claude sees the screen and clicks. | Very high | Low | Local software with no other way in. |

Ben: "Browser use is actually an extremely inefficient way to access softwares or tools. It's token heavy, error prone, and pretty expensive." Computer use is worse. Claude uses the browser automatically when no connector exists. That is a sign you should add one.

### 2.4 Native connectors

Settings → Connectors → Browse connectors → log in. Claude Academy: "Claude can only access data you have access to." Permissions are scoped and revocable. On Team and Enterprise, an owner adds connectors and each member authenticates.

Set trusted read-only connectors to "always allow" so the agent does not stop for permission every step. Keep write actions on "ask".

### 2.5 Custom connectors (remote MCP)

Settings → Connectors → Add custom connector → paste the server URL → Add. Optional OAuth details under Advanced. Available on paid plans. Only connect servers you trust. The support docs warn: "Malicious MCP servers may include hidden instructions that try to make Claude perform unintended actions." That is prompt injection. Module 14.

Desktop alternative: Settings → Developer → Edit config opens a JSON file. Paste the vendor's snippet. Save. Restart Claude. If the JSON scares you, paste it into a chat and say "update this JSON with the new server, here are the vendor's instructions", then paste back.

### 2.6 Build your own

"Use the MCP builder skill. Build me an MCP server for <tool>. Here is the API documentation." Claude writes the server and the install steps. Ben did this for Circle.so in one session. Worth it for any tool you use weekly that has an API and no MCP.

### 2.7 Internet access and scrapers

Claude reads most URLs. It cannot read social networks directly (LinkedIn, Instagram, Facebook). Options:

- **Apify** — a marketplace of thousands of scrapers ("actors"): LinkedIn profiles and posts, X, Instagram, YouTube transcripts, Apollo. Free tier, then a paid plan (about 29–39 dollars a month at the time of Ben's recording; check). Native Cowork connector exists. You choose which actors to enable.
- **Research mode** — Claude runs many searches at once, across the web and your connectors, and synthesises with citations. Minutes, not seconds. For deep questions, not quick facts.

### 2.8 Claude in Chrome

A Chrome extension. Claude reads pages, clicks, fills forms, works across tabs, records reusable shortcuts, and can run scheduled browser tasks. It is also the browser Cowork and Claude Code use. All paid plans. Some categories (financial, adult) are restricted. Admins can allow-list sites. Use it when there is no connector, or when a human would use a browser anyway.

### 2.9 Computer use

Desktop Settings → General → Computer use. Invoke explicitly: "Update this in <app> using computer control." Slow, vision-based, expensive. Reserve for local desktop software with a specific click path.

### 2.10 Hooks: the guardrails around tools

Hooks are shell commands that run at fixed points in an agent's work: before a tool call, after a file edit, when the agent stops. They are deterministic. The model cannot skip them. Uses:

- after every edit, run the formatter;
- before any deploy command, run the tests and block if they fail;
- notify you on the desktop when the agent waits for input;
- block any command that contains `rm -rf` or a production URL.

Claude Code docs: "Hooks are user-defined shell commands... which gives you deterministic control: certain actions always happen rather than relying on the LLM to choose to run them." CLAUDE.md is advice. A hook is a rule. Module 14.

### 2.11 Tool instruction files

After Claude uses a tool once, ask it to write `references/tool-<name>.md`: which actions worked, which fields matter, what to avoid. Skills read that file at the step that uses the tool. Ben does this for every MCP in a skill.

### 2.12 Codex and the same ideas

Codex uses MCP too (`codex mcp add`). Its equivalent of CLAUDE.md is `AGENTS.md`. Its permissions live in `config.toml`. The hierarchy in 2.3 applies unchanged. Module 10.

## 3. How to do it in Claude — a connection checklist

1. Name the tool. Name the three actions you need (read X, list Y, create Z).
2. Check level 1: is it in Settings → Connectors → Browse?
3. If not, search "<tool> MCP server". Check the source is the vendor or a well-known community repo.
4. Add it. Test with one read action: "List my last five <things> in <tool>."
5. Ask Claude to write the tool instruction file.
6. Set permissions: read = always allow; write = ask.
7. Only then use it in a skill.

## 4. Worked example — Tsara Tilapia data

| Need | Level | How |
|------|-------|-----|
| Read the ENGINE sheets | 1 | Google Drive connector, or Sheets access from Apps Script |
| Weekly briefing to staff on WhatsApp | 4 → 2 | Start with Claude in Chrome on WhatsApp Web for one-offs. Move to an MCP for a messaging API when the volume justifies it. |
| Feed supplier price check on their website | 4 | Browser use, scheduled weekly. No API exists. |
| Fish price index from a market site | 2 or 4 | If they publish a feed or API, MCP. Otherwise browser. |
| Pull live Apps Script code | 0 | **You** run `clasp pull`. It touches your identity. Claude reads the output from `_parked/pull/`. |

## 5. Exercise (45 minutes)

1. List every piece of software you use in a week. Twenty lines maximum.
2. For each: which level from 2.3? Mark the ones with no connector and no MCP.
3. Connect two level-1 tools you have not connected yet. Test one read action each.
4. Pick one level-4 tool you touch often. Ask Claude: "Is there an MCP server for <tool>? If not, what API does it have?" Decide: build, or stay on browser.
5. Write the results to `docs/exercises/m08-tool-map.md`.

## 6. Check yourself

1. **What is an MCP server, in one line?** All the actions of one tool bundled into one package any agent can use.
2. **What is the last resort in the access hierarchy?** Computer use.
3. **What is the difference between CLAUDE.md and a hook?** CLAUDE.md is advice the model usually follows. A hook always runs.
