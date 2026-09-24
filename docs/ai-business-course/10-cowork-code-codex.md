# Module 10 — Claude Cowork, Claude Code and OpenAI Codex

**Time:** 90 minutes
**Goal:** You can start each of the three tools, give it a folder and a ticket, and read the result. You know how they differ, how to use them with the Claude and ChatGPT desktop apps, and how to do simple coding without being an engineer.

## 1. Why it matters

These three are the agent tools you will use daily. They share one design: a folder, a standing-instruction file, a permission model, skills, MCP, and a plan-then-do loop. Learn one well and the other two take an hour.

## 2. Claude Cowork

### 2.1 Principle

Cowork is the "hand it off" mode. Support docs: "describe an outcome, step away, and come back to finished work." Sessions run in an isolated environment: a VM on your machine (on-device) or on Anthropic's servers (cloud). Cloud sessions keep running when your laptop is closed.

### 2.2 First steps

1. Desktop app → **Cowork** tab. Also on claude.ai and mobile on Pro/Max/Team.
2. Settings → Cowork → **global instructions**. These apply to every session.
3. "+" menu → **connectors**. Enable the ones the task needs.
4. **Connect a folder.** Start every task by choosing the folder. Ben: make it a habit so every asset lands somewhere findable.
5. Give the ticket. Watch the task list fill. Answer the questions Claude asks (checkboxes, single select, free text).
6. Read the result. Read the files it wrote. Check the folder listing.

### 2.3 Interface

- **Task list widget.** Shows steps and progress.
- **Questions.** Cowork stops and asks when a decision is yours. Answer from desktop or phone.
- **Permission modes:** Manual (asks before each action), Auto (a classifier reviews and blocks risky actions), Skip (no checks — highest risk).
- **Projects.** Bind a folder, instructions, memory and scheduled tasks together.
- **Scheduled.** Sidebar section. `/schedule` in chat. Module 12.
- **Plugins.** Bundles of skills and connectors per role. Anthropic ships sales, marketing, productivity, legal, finance, customer-support and operations plugins.
- **Dispatch.** Send a task from your phone to the desktop. Module 13.

### 2.4 Strengths and limits

Strong for: documents, research, files, connectors, scheduled work, bulk work with sub-agents, non-technical users. Uses more usage than chat. Sub-agents use a lot. Sessions cannot be shared; artifacts can.

## 3. Claude Code

### 3.1 Principle

Claude Code is an agent that works inside a folder: reads files, edits them, runs commands, uses git. Built for software. The loop works for any folder of text. Two doors: the **Code tab** in the desktop app ("no terminal required") and the **terminal** command `claude`.

### 3.2 First steps — desktop (recommended for non-engineers)

1. Desktop app → **Code** tab → **Local** → **Select folder**. Start "with a small project you know well". LEARN is ideal.
2. Pick a model.
3. Type a request: "What does this project do? Explain the folder structure."
4. Read the answer. Then a real ticket.
5. Review changes in the **diff view**: the before and after of every file. In Manual mode you accept or reject each change. You can comment and ask for revisions.

### 3.3 First steps — terminal

- macOS/Linux: `curl -fsSL https://claude.ai/install.sh | bash`
- Windows PowerShell: `irm https://claude.ai/install.ps1 | iex`
- Check: `claude --version`. Then `cd` into a folder and run `claude`.
- Essentials: `/init` (writes a first CLAUDE.md), `/help`, `/clear`, `claude -c` (continue last session), `Shift+Tab` (cycle permission modes: Auto, Manual, Accept edits, Plan).

You do not need the terminal to be a pro operator. Kim runs `git` and `clasp` there by choice, because those touch identity and production. Everything else goes through the desktop tab or Cowork.

### 3.4 The workflow: explore → plan → code → commit

Claude Code 101's core loop. Explore the repo. Plan (plan mode). Make the change. Commit with a message that says why. Then review. Module 03 gives the prompts.

### 3.5 What makes Claude Code Claude Code

- **CLAUDE.md** — standing instructions, hierarchical: managed policy → `~/.claude/CLAUDE.md` → project `./CLAUDE.md` → `CLAUDE.local.md`. Under 200 lines each. Module 05.
- **Subagents** — helpers with their own context window and tool list. `/agents`. Module 11.
- **Skills** — `.claude/skills/<name>/SKILL.md`. Module 07.
- **Hooks** — deterministic guardrails. Module 08 and 14.
- **MCP** — `claude mcp add ...`. Module 08.
- **Routines** — scheduled sessions, local or cloud. Module 12.
- **Worktree isolation** — parallel sessions without collisions. Module 06.
- **Review** — `/review`, and a heavier remote review for risky changes.
- **Web** — claude.ai/code runs sessions in the cloud on a GitHub repo.

### 3.6 Simple coding for a non-engineer

You will not write code by hand. You will manage code that an agent writes. What you need:

1. **Read a diff.** Green added. Red removed. Ask: does this match the ticket? Is there anything surprising? Surprising is where the risk is.
2. **Know four words.** *Function*: a named block that takes inputs and returns an output. *Variable*: a named value. *Loop*: repeat for each item. *Condition*: do this if that. The LEARN curriculum map covers these.
3. **Run the checks.** Ask the agent to run tests and show output. Read the last ten lines.
4. **Use the eyes.** Ask the agent to open the app in the preview, click the flow, and report what a user would experience.
5. **Keep tickets small.** One reviewable change. If the diff is longer than a page, the ticket was too big.
6. **Never deploy from the agent.** The agent writes the command. You run it. You read the output (`tee` it to `_parked/out/`).

Greg's seven-day plan (module 17) is a non-engineer's path through all of this.

## 4. OpenAI Codex

### 4.1 Principle

Codex is OpenAI's coding agent, the counterpart of Claude Code. Open source, written in Rust. It exists as a CLI, an IDE extension, a cloud agent, and a desktop app that OpenAI positions as "a command center for agents".

### 4.2 First steps — CLI

- Install: `curl -fsSL https://chatgpt.com/codex/install.sh | sh` (or npm, Homebrew).
- Run `codex`. Sign in with your ChatGPT account.
- `/init` writes an **AGENTS.md** — Codex's CLAUDE.md.
- `/permissions` sets how much Codex may do without asking.
- `codex exec` runs a scripted, non-interactive task. `codex resume` continues. `codex mcp` adds MCP servers.
- Configuration lives in `config.toml`: rules, hooks, environment variables, permissions.

### 4.3 First steps — the Codex / ChatGPT desktop app

1. Download the ChatGPT desktop app (macOS, Windows, Linux). Sign in.
2. Pick where to work: a chat, a project, or open a folder.
3. Work mode gives threads per project. Each thread gets its own git worktree, so several agents work on one repo without conflicts.
4. Automations: scheduled background tasks (issue triage, CI failure checks).
5. Browser and computer use from the app. A code-review mode. Skills and plugins.

Ryan Carson's view: the Mac app "is so beautiful", generous with usage on the 200-dollar plan, and excellent as a general helper that opens tabs, writes docs and checks email. His warning: do not build your whole company's engineering on one lab's tool.

### 4.4 Availability

Included with ChatGPT Plus, Pro, Business, Enterprise and Edu at launch (February–March 2026). Exact tiers and limits change. Check learn.chatgpt.com/docs.

## 5. Side by side

| | Claude Cowork | Claude Code | OpenAI Codex |
|---|---|---|---|
| Made for | Knowledge work | Software | Software |
| Standing file | CLAUDE.md (folder) + global instructions | CLAUDE.md | AGENTS.md |
| Permission modes | Manual / Auto / Skip | Auto / Manual / Accept edits / Plan | `/permissions`, sandbox, approval modes |
| Skills | Yes | Yes | Yes |
| MCP | Connectors | `claude mcp add` | `codex mcp` |
| Sub-agents | Isolated sub-agents | Subagents + teams | Threads / worktrees |
| Scheduled | `/schedule`, Scheduled tab | Routines (local and cloud) | Automations |
| Runs in cloud | Yes | Yes (web) | Yes |
| From phone | Yes + dispatch | Web | Web / app |
| Best entry for non-engineer | Yes | Desktop Code tab | Desktop app |

They share so much because they follow the same idea: **a folder, a brain file, tools, permissions, a loop.**

## 6. Using them together

- **Same brain, many agents.** Point Cowork, Claude Code and Codex at the same folder. Ben got the same answer from Claude Code and Codex because both read the same CLAUDE.md and files. Keep one CLAUDE.md and one AGENTS.md that says "read CLAUDE.md".
- **Chat to think, agent to do.** Think through a problem in Claude Chat or ChatGPT. When the outcome is clear, hand the ticket to Cowork, Code or Codex.
- **Second opinion.** Ask Codex to review a change Claude Code made, or the reverse. Different models catch different mistakes.
- **Cost routing.** Use the cheaper tool for bulk or low-stakes work. Use the strongest model to plan and review.
- **Do not split one task across two agents.** One ticket, one agent, one result. Then review.

## 7. Worked example — the same ticket in three tools

Ticket: "In the LEARN repo, add frontmatter (title, date, type) to every file in `lessons/`. Do not change body text. Show me the diff."

- **Cowork:** connects the folder, edits the files, shows the result in the task list. Good for a one-off.
- **Claude Code (desktop):** same edit, plus a diff view and a proposed commit message. Good because this is a repo and you want history.
- **Codex CLI:** `codex "add frontmatter..."` in the folder. Same result. Good to compare quality and cost.

Pick Claude Code for this one. It is a repo change. Then you run `git commit` and `git push` yourself.

## 8. Exercise (90 minutes)

1. Run the ticket in section 7 in Claude Code (desktop). Read the diff. Accept. Commit yourself.
2. Install Codex CLI if you have a ChatGPT plan. Run `/init` in a copy of LEARN. Compare AGENTS.md with your CLAUDE.md.
3. In Cowork, ask for a one-page comparison of the three tools *as you experienced them*. Save to `docs/exercises/m10-three-tools.md`.
4. Capture the lesson.

## 9. Check yourself

1. **Which tool for "describe an outcome and step away", non-technical?** Cowork.
2. **What is Codex's equivalent of CLAUDE.md?** AGENTS.md.
3. **What is the one thing a non-engineer must do on every code change?** Read the diff and ask whether anything is surprising.
