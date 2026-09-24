# Module 15 — Building a team of agents

**Time:** 90 minutes
**Goal:** You can design, build, operate and control a team of agents for your business. You know the nine parts of an AI employee, the patterns for running many in parallel, how to bundle them into plugins, and how to keep costs sane.

## 1. Why it matters

One agent is a helper. A team of agents is an operating layer for the company. Greg: "Once you set it up this way, Claude Code starts to feel less like a one-off chat thing and more like an operating layer for your company." Ryan runs ten at once. Theo's proposals write themselves. This module puts every previous module together.

## 2. The concepts

### 2.1 The nine parts of an AI employee

Greg's map. Each part maps to a module.

| # | Part | What it means | Module |
|---|------|---------------|--------|
| 1 | **Workspace** | A repo where the work lives | 06 |
| 2 | **Memory** | CLAUDE.md, roadmap.md, review.md, /context, /customers | 04, 05 |
| 3 | **Brief** | Plan mode before touching anything | 03 |
| 4 | **Ticket** | One clear assignment with a finish line | 03 |
| 5 | **Eyes** | The agent inspects what it built: preview, tests, logs | 03, 10 |
| 6 | **Review** | Layers: your read, agent vs review.md, deep review | 14 |
| 7 | **Schedule** | Routines: morning brief, weekly review, PR review | 12 |
| 8 | **Permissions** | Safe / ask first / human-owned | 14 |
| 9 | **Skills, connectors, hooks** | Repeatable, connected, guarded | 07, 08 |

"Give Claude a place to work, context to understand the business, a clear way to plan, a way to execute, a way to check, a way to review, a few recurring responsibilities, and boundaries."

### 2.2 The three root files

For any product or project repo:

- **CLAUDE.md** — how to work here. Working style ("small reviewable changes; explain the plan before editing when the task affects behaviour; run checks after; summarise what changed, what you tested, what needs human review"). Business context (what, for whom, the promise). Quality bar.
- **roadmap.md** — what matters this week. And explicitly **what is out of scope** ("payments, CRM integration, admin dashboards, multi-user permissions are out of scope"). Scope is what keeps the agent from wandering.
- **review.md** — how to judge work before it ships. Yes/no questions.

The setup prompt:

> Help me set up this repo as an AI employee workspace. Create or update CLAUDE.md, roadmap.md, review.md, /context, /customers, /specs, /demos, /routines. Business context: product <X>, buyer <Y>, pain <Z>, promise <P>, current goal <G>. Before writing, ask me for any missing context that would materially change the setup. Keep the first version simple.

### 2.3 Team shapes

**Shape A — parallel specialists (Greg).** One session per work stream, same project context, different job and hand-off. Morning example: a bug session, a landing-page session, a sales-script session. Each returns a small packet. Use worktree isolation so changes do not mix.

**Shape B — orchestrator and children (Ryan, Ben).** A strong model as manager. It splits the goal, spawns children on cheaper models, reviews the returns. Ben's outbound pipeline: 15 qualifiers, 18 enrichers, 17 writers, one command in front. Cowork sub-agents are isolated; only summaries return.

**Shape C — skill chain / command (Theo, Ben).** A fixed sequence of skills, each possibly using sub-agents, fired by one trigger. Theo's proposal chain: microsite → copy → QA → deploy → Slack. His product chain: hypothesis → prototype → usability test → synthesis → V2 plan. Ben's `/repurpose`: LinkedIn → newsletter → diagram → GIF → infographic.

**Shape D — the night shift (Greg).** Scheduled routines that run alone: morning brief, weekly ops review, PR reviewer, production watchdog, self-improvement grader.

**Shape E — communicating team (Claude Code agent teams).** Agents share a task list and message each other. For interdependent engineering work. Ben: for office work, isolated sub-agents are enough and cheaper.

Most businesses need A + B + C + D. E is for software teams.

### 2.4 Roles in a business agent team

A starter roster. Each is a skill, an agent file, or a routine. Name them. Ben and Theo both name theirs.

| Role | Type | Does |
|------|------|------|
| **Librarian** | Routine + skill | Captures inbound (email, transcripts, Slack) into the brain inbox; curates; files; detects triggers |
| **Chief of staff** | Routine | Morning brief; weekly review; task prioritisation |
| **Watchdog** | Routine | Reads the system of record; summarises what customers/ponds/accounts did; links to evidence |
| **Researcher** | Sub-agent | Read-only; searches web and tools; returns a summary |
| **Qualifier / Enricher** | Sub-agents in batches | Bulk classification and data enrichment |
| **Writer** | Skill | Produces in your voice from the brain's examples |
| **Reviewer / QA** | Sub-agent, read-only | Checks against review.md; must/should/OK |
| **Grader** | Routine | Scores yesterday's output on a rubric; opens fixes |
| **Builder** | Claude Code session | Executes tickets in plan → do → verify |
| **Deployer** | **You** | Runs the human-owned commands |

### 2.5 Plugins: how a team is packaged

A **plugin** = skills + commands + agents + connectors, bundled. Three effects: more complexity is possible (commands chain skills; agent teams are specialised; connectors are preset); sharing per department is easy (sales plugin, ops plugin); it is versionable, so an update reaches every account that uses it.

Build order: **skills first → bundle into a plugin → add commands that chain them → add agent files → add routines.** Ben's prompt to package a team:

> Create a plugin called `<name>`. Inside: a skill for the exact way we did qualification, with its own agent.md the skill refers to; a skill for the exact way we did enrichment, with its own agent.md; both instructed to spawn parallel batches of sub-agents as above; a command.md `/outbound-pipeline` that asks for a CSV, runs both skills in sequence, and delivers the enriched CSV. Store everything in the plugin.

Share: zip → teammate uploads; or host on GitHub for a versioned link; or a private marketplace.

Anthropic's open-source department plugins (sales, marketing, product, legal, finance, customer support, operations) are good starting points. Customise, do not start blank.

### 2.6 The workday of an agent manager

- **06:30** Read the morning brief on the phone.
- **08:00** Pick three work streams. Write three tickets. Start three sessions (Shape A). Pin them.
- **08:00–12:00** Every 25 minutes: check pinned threads. Answer questions. Accept or reject packets. Between checks: your own work — customers, ponds, judgement.
- **All day** Small fires go to un-pinned sessions. Come back to them when you can.
- **15:00 Friday** Read the weekly review. Update roadmap.md.
- **Night** Routines run: watchdog, grader, PR reviews, librarian.

Ryan: expect ten to twenty high-stakes decisions by lunch. It is a new muscle. Pace yourself.

### 2.7 Evals for a team

A team without evals is a team you cannot trust. For each role: what is the standard, where is the example, how is it scored, who sees the score. Automated evals for skills (module 07). Daily grading for production output (module 12). Your own read for anything that ships.

### 2.8 Cost and model routing

Ryan's rule: the strongest model as manager and reviewer; tuned cheap models for loops and bulk. Cowork lets you pick the model per scheduled task. Claude Code lets you set a model per sub-agent. Budget per role. Watch weekly. A one-person office operation runs on a standard plan. A software factory runs on thousands a month and needs routing.

### 2.9 Ownership and lock-in

Keep the brain, the skills, the agent files and the plugins in plain files in git. Then the team survives a change of vendor or tool. Ben's second brain gave the same answers from Claude Code and Codex because both read the same files.

### 2.10 Growth path

1. One agent, one folder, three root files. (Week 1)
2. Three routines. (Week 2)
3. Five skills built by doing. (Weeks 2–3)
4. First parallel sub-agent job on real data. (Week 3)
5. First command chaining three skills. (Week 4)
6. First plugin. Share it with one colleague. (Month 2)
7. Daily grader on your most important output. (Month 2)
8. Orchestrator sessions as the default for big goals. (Month 3)

## 3. How to do it in Claude — build your first team this week

**Day 1 — Workspace and memory.** Run the setup prompt from 2.2 on your main project folder. Write the three tiers of permissions into CLAUDE.md.

**Day 2 — Routines.** Morning brief and weekly review (module 12).

**Day 3 — Two skills by doing.** Your most frequent document and your most frequent analysis (module 07).

**Day 4 — Reviewer and researcher.** Two agent files in `.claude/agents/`. Read-only tools.

**Day 5 — Parallel job.** One bulk task with explicit sub-agent counts on real data.

**Day 6 — Command.** Chain the two skills plus the reviewer into one `/command`.

**Day 7 — Package and log.** Bundle into a plugin. Write `daily/` entries. Capture the lesson in LEARN.

## 4. Worked example — Tsara Tilapia agent team v1

| Role | Implementation |
|------|----------------|
| Librarian | Daily routine: WhatsApp exports and staff notes from the connected folder → `intelligence/notes/YYYY-MM/`, tagged by pond and topic |
| Chief of staff | Morning brief 06:30; Friday review 15:00 |
| Watchdog | Daily: read ENGINE warnings and stock tabs; summary by pond; link to sheet rows |
| Writer | `weekly-briefing` skill (French, STE, three sections) |
| Analyst | `feed-conversion-analysis` skill; read-only on the sheets |
| Reviewer | `.claude/agents/reviewer.md` against `review.md` |
| Auditor | `erp-audit` skill, weekly, read-only |
| Builder | Claude Code session per patch, plan mode, `patches/YYYY-MM/` |
| Deployer | Kim: `clasp deploy -i ...` with `tee` to `_parked/out/` |
| Grader (month 2) | Grade each week's briefing against the best example; propose rule updates to the skill |

Everything lives in `tsara-erp/`. Every file is Markdown or CSV. Every output goes to a named folder. Kim owns deploys.

## 5. Exercise (this week)

Do the seven days in section 3. At the end, write `docs/exercises/m15-team-v1.md`: the roster table, what each role produced this week, and the three decisions you made that the team could not.

## 6. Check yourself

1. **What are the nine parts of an AI employee?** Workspace, memory, brief, ticket, eyes, review, schedule, permissions, skills/connectors/hooks.
2. **What is the build order for a plugin?** Skills, then bundle, then commands, then agents, then routines.
3. **Which model does the orchestrator use, and which do the children use?** The strongest for the manager and reviewer; cheaper models for children and loops.
