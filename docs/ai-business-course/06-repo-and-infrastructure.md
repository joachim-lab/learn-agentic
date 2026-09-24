# Module 06 — Repo and infrastructure

**Time:** 60 minutes
**Goal:** You can explain where an agent runs, what a repo is, why cloud beats local for many agents, and how to keep production safe.

## 1. Why it matters

Ryan Carson: "The more you become a better agent manager, the more technical you become." You do not need to code. You do need to know the shape of the machine your agents work in. Otherwise you cannot judge risk, cost or speed.

## 2. The concepts

### 2.1 The repo is the workspace

A repo is a folder whose history git records. Lesson 001 in LEARN covers the four commands. For agents, the repo is:

- **the workspace** — where files live and where the agent does the work;
- **the memory** — CLAUDE.md, context files, logs;
- **the audit trail** — every change is a commit with a message;
- **the undo button** — any commit can be restored.

Claude Academy: "git tracks every version so you can always roll back." That is why agents should work in repos even for non-code work. A folder of Markdown under git is a repo. Your LEARN folder is one.

### 2.2 Where the agent runs

| Place | What it means | Good for | Limits |
|-------|---------------|----------|--------|
| **Your machine (local)** | The agent edits files on your laptop | Small tasks. Front-end work you want to see. Files that must not leave the machine. | One thing at a time. Laptop must be on. Changes can collide. |
| **A sandbox on your machine** | A small virtual machine the desktop app runs. Your folders are mounted inside it. | Cowork on-device sessions. Safe experiments. | It is not your Mac. Paths outside the mount are invisible to you. |
| **A cloud sandbox** | A fresh virtual machine on the vendor's servers | Long tasks. Many tasks in parallel. Work from your phone. Scheduled work when your laptop is off. | Needs the files pushed to it (git) or connected (folder link). |
| **A server / production** | Where the real product runs for real users | Nothing agent-driven without human approval | Mistakes hit customers. |

Kim's preferences say it exactly: "Your device shell is a sandbox, not my Mac. My folders are mounted at `~/mnt/<folder>` inside that shell. A path like `~/Claude/projects/...` inside it creates a decoy I never see." That is the sandbox row of this table, lived.

### 2.3 Cloud agents: why Ryan says "local is caveman"

Ryan Carson runs five to ten cloud agents at once. His reasoning:

- Local work means one copy of the code, one thing at a time. Two things at once means git worktrees or a second copy. Five things is not possible.
- A cloud agent gets its own virtual machine. Click "new session", a VM spins up, the agent works. No collisions. No "did I pull the latest".
- He ships 22 to 25 pull requests a day. On a day he climbed a mountain with his son, he shipped eight before breakfast from his phone.

His nuance: for heavy new UI, start local so you can see it. Then move it to the cloud fast.

Claude offers this as **Cowork in the cloud** (web and mobile), **Claude Code on the web** (claude.ai/code), and **cloud routines**. Codex has cloud tasks. Devin, Factory and others are cloud-first products.

### 2.4 Worktrees and isolation

When several agents edit the same repo, each needs its own copy of the working files. Git worktrees do that: one repo, several working folders, each on its own branch. Claude Code's desktop Code tab offers "worktree isolation" per session. Codex's app does the same per thread. You do not need to run the commands. You need to know: **one agent, one worktree, one branch, one pull request.**

### 2.5 Dev, exec and prod

- **Dev:** where you try things. Breaking it costs nothing.
- **Prod (production):** what users use. Breaking it costs money and trust.
- In Apps Script, Kim's rule is "always work on exec, never dev": the `exec` deployment is what users open. A redeploy is `clasp deploy -i <deploymentId>`. Without `-i` clasp creates a new deployment with a new URL. That rule exists because the agent once cannot tell the two apart. Write such rules in CLAUDE.md.

### 2.6 Secrets and keys

Ryan's practice, worth copying word for word:

- All production write keys live in a password manager (1Password). Never in the repo. Never in a prompt. Never in CLAUDE.md.
- Agents do not hold prod write keys. When an agent needs one, it asks. You paste it into that one session. Both of you know what is happening.
- Read keys for dev are fine in an environment file that git ignores (`.gitignore`).

Kim's version: "I run every command that touches production or my identity: git, clasp, deploys, logins. You never run them." Same principle, stricter. Good.

### 2.7 Environments, dependencies, migrations

Three words that show up in agent permission lists:

- **Environment:** the set of installed tools and settings a program needs. A cloud VM has a fresh one each time.
- **Dependency:** a library the program uses. Installing one changes the environment. Ask first.
- **Migration:** a change to a database's structure. Hard to undo. Ask first, always.

### 2.8 Local files and the desktop bridge

The Claude desktop app can link a cloud session to your computer. The session reaches your connected folders through a bridge. Files move up (stage) or down (commit). Each move is slow and leaves two copies. The rule from Kim's own preferences and from the Claude docs is the same: **work on files where they live. Move a file only when the step needs a tool that exists only on the other side.**

### 2.9 Cost

Ryan's numbers, September 2026, for a one-person software company at product-market fit: about 5,000 dollars a month per "engineer-equivalent" of agent work is where it "shakes out". His 20,000-dollar month was a mistake he fixed with model routing: cheap tuned models for loops, the strongest model to plan and review. A 200-dollar-a-month plan is plenty for a solo operator doing office work. Watch usage. Scale the model to the stakes.

### 2.10 Vendor lock-in

Ryan argues: do not build your whole engineering motion inside one frontier lab's tool. Independent agent products (Devin, Factory, Amp, Cursor) route between models and optimise for cost. Greg's counter: you still use the same models inside them. Take both points: keep your brain in plain Markdown and git so it moves anywhere. Then use whichever tool is best today.

## 3. How to do it in Claude

- **Turn a folder into a repo:** ask Claude Code: "Initialise git here. Write a .gitignore that excludes secrets and _parked/out. Make the first commit." Then you run the push.
- **Cloud session:** open claude.ai/code or Cowork on the web. Pick the repo (GitHub) or a connected folder. Give the ticket.
- **Isolation:** in the desktop Code tab, start a new session per ticket. Enable worktree isolation for parallel sessions.
- **Secrets:** never paste a key into a chat that will be saved. Use the credential features of the desktop app or paste into a single session and rotate after.

## 4. Worked example — three tickets, three places

| Ticket | Where | Why |
|--------|-------|-----|
| "Rewrite the feeding SOP in Simplified Technical English." | Local Cowork with the tsara-erp folder | Text only. You want to read the diff on your screen. |
| "Audit all six Apps Script clones for duplicated constants. Report only." | Cloud Cowork, read-only | Long. Many files. You will read the report on your phone. |
| "Redeploy ENGINE to exec with the new threshold." | **You**, in your terminal, with the command Claude wrote | Touches production and your identity. |

## 5. Exercise (45 minutes)

1. Ask Claude Code, in the LEARN folder: "Explain what git status, git log and git diff show me. Then run them and explain the output." Read it.
2. Start one Cowork task in the cloud on the LEARN repo. Ticket: "List every Markdown file, its frontmatter, and the ones missing frontmatter. Write the result to docs/exercises/m06-inventory.md." Check the result from your phone.
3. Write `context/systems.md` for one project: which system holds which data, and which keys the agent never sees.
4. Capture the lesson: "capture the lesson" in LEARN.

## 6. Check yourself

1. **Why work in a repo even for non-code work?** History, rollback, audit trail, and a shared workspace for agents.
2. **What does one cloud agent get that a local one does not?** Its own fresh machine, so it cannot collide with other work.
3. **Where do production keys live?** In a password manager. Never in the repo, the prompt or CLAUDE.md.
