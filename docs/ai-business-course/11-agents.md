# Module 11 — Agents

**Time:** 60 minutes
**Goal:** You can explain how an agent works, what it needs to be autonomous, the three levels of autonomy, what an eval is, and how sub-agents keep the main agent's context clean. You can build a sub-agent.

## 1. Why it matters

"Everyone is a manager now." — Theo Tabba. "You are a manager of agents now, no matter what you used to do." — Ryan Carson. To manage a worker you must know how the worker works. This module is the worker's anatomy.

## 2. The concepts

### 2.1 The loop

**An agent is a model using tools in a loop.** Concretely:

1. Read the goal and the context.
2. Decide the next step.
3. Call a tool (read a file, search, run a command, send a message).
4. Read the tool's result.
5. Decide: done, or go to step 2.

Everything you see — Cowork, Claude Code, Codex, Devin — is this loop plus an interface plus safety rails. Andy Grove's rule applies: the success of a manager is the output of the team. Your output is now the output of your loops.

### 2.2 The four needs

Theo's list. An agent is autonomous when it has all four:

| Need | What it is | Where it comes from |
|------|------------|---------------------|
| **A clear goal** | What done looks like. How to measure it. When it is due. | The ticket. Module 03. |
| **Skills** | How to do this kind of task, your way. | Skills. Module 07. |
| **Tools** | Access to the systems the task touches. | Connectors, MCP. Module 08. |
| **Context** | What the business is, who the customer is, what good looks like. | The brain. Modules 04–05. |

Missing one and the agent behaves like a new hire on day one asked to write the board deck: it guesses. People get impatient with models because none of the four is baked in. Bake them in.

### 2.3 Three levels of autonomy

1. **Chatting.** You type, it answers. You do all the work between turns.
2. **Supervised agent.** It runs. You sit there clicking approve, approve, approve. You are "managing on hard mode": the agent is brilliant and junior, and you are its bottleneck.
3. **Autonomous agent.** Like a trusted hire after a few months. It runs for hours or days. It comes to you with results and with the decisions only you can make.

You move from 2 to 3 by adding the four needs and by extending permissions as trust grows. Not by turning off safety.

### 2.4 Evals: knowing what good looks like

An eval is your visibility into what the agent did and how good it was, against a standard. Without evals you cannot delegate, because you cannot tell an 8/10 from a 6/10 without reading everything.

Where the standard comes from:

- the goal says what success is;
- a skill or `review.md` holds the quality bar and the SOP;
- `resources/examples/` holds the pinnacle you compare against.

Combine those, give the agent the right tools, and you get the quality you want "over and over again". Module 07 covers automated evals of skills. Ryan's daily grading loop (module 12) is an eval on production conversations.

### 2.5 Hallucination in agents

An agent that fakes a fact then acts on it. Guardrails: give the sources; require citations; add a QA skill at the end of any chain ("make sure we are not over-promising, not saying anything egregious, not making anything up that is not in the transcripts"); keep write actions behind permission.

### 2.6 Sub-agents

A sub-agent is a helper with its own fresh context window, its own instructions and its own tool list. The main agent hands it a slice of work. Only a **summary** comes back. The main window stays clean. Ben: "Context is one of the most precious resources for these agents."

Claude Code docs: "Use one when a side task would flood your main conversation with search results, logs, or file contents you won't reference again."

Two uses:

- **Parallel bulk work.** Fifteen sub-agents each research ten leads. Done in two minutes instead of an hour.
- **Specialists.** A reviewer with read-only tools. A researcher that only searches. A writer that only writes.

### 2.7 Sizing sub-agents

Ben's rules from running them daily:

- 5 to 15 items per sub-agent;
- sweet spot 100–200 records per run; beyond that use a deterministic automation tool;
- be explicit: "spin up 15 parallel sub-agents, each researching 10 leads". Otherwise Claude may work sequentially or not use sub-agents at all;
- expect heavy usage. Be on the right plan.

Claude Code defaults: up to 20 concurrent sub-agents, nesting depth 3.

### 2.8 Isolated sub-agents vs teams

Cowork's sub-agents are isolated: they do not talk to each other. Claude Code also has **agent teams** that share a task list and message each other. Ben's advice: isolated sub-agents are enough and cheaper for office work. Teams suit shared, interdependent to-do lists. Module 15.

### 2.9 Orchestrator and children

Ryan's pattern: a strong model as the manager ("a Fable thread as the manager"), cheaper models as children. The manager reads the goal, splits it, spawns five child sessions, reviews what comes back. This is the shape of every agent team. Module 15.

### 2.10 Built-in sub-agents in Claude Code

- **Explore** — read-only search across many files. Returns the conclusion, not the file dumps.
- **Plan** — research for plan mode.
- **General-purpose** — anything else.

You can define your own in `.claude/agents/<name>.md` with a description, allowed tools, a model, and a system prompt. Invoke by name, by `@mention`, or make one the session default.

### 2.11 Agent definitions in plugins

Ben's outbound plugin has an `agents/` folder with `lead-qualifier.md`. The skill says "spawn parallel batches of the lead-qualifier agent". The agent file holds the role, the criteria, and the output format. Skills describe processes; agent files describe workers.

### 2.12 Signals that you are managing well

- Each session has one clear job, the same project context, and a specific hand-off format.
- You receive small packets of work you can inspect, accept, revise or reject.
- You are not untangling a giant pile of AI work at the end of the day.

## 3. How to do it in Claude

**A parallel bulk task in Cowork:**

> I want to qualify these 150 leads against my ICP: marketing agencies that provide SEO services, based in the US. Spin up 15 parallel sub-agents that each research 10 leads. Each returns: qualified yes/no, one-line reason. From the summaries, deliver an updated CSV with two new columns: status, reason.

Ben's result: 82 of 150 qualified in about two minutes, with reasons.

**A specialist sub-agent in Claude Code:**

```
.claude/agents/reviewer.md
---
name: reviewer
description: Reviews a change against review.md. Read-only. Use before any merge.
tools: Read, Grep, Glob
model: <strongest available>
---
You review changes against review.md. You never edit files.
Output: must fix / should fix / OK to ship. One line per item, with file and line.
```

Then: "Use the reviewer agent on the current changes."

## 4. Worked example — the outbound pipeline

Ben's full flow, built in one session and saved as a plugin:

1. **Qualify.** 15 sub-agents × 10 leads. Output CSV with status.
2. **Enrich.** 18 sub-agents: 17 researchers plus one that runs the LinkedIn scraper. Output: last post, company size, description.
3. **Write.** 17 sub-agents write personalised icebreakers for the 37 best.
4. Saved as three skills, two agent files and one command `/outbound-pipeline` that runs them in sequence.

Total human time: an afternoon to build. Then minutes per run.

## 5. Exercise (60 minutes)

1. Write the four needs for one task you want to delegate. Goal, skills, tools, context. Mark what is missing.
2. Run one parallel sub-agent task on real data: 30–50 rows. Be explicit about the number of sub-agents and rows each.
3. Create one specialist sub-agent (a reviewer or a researcher) in the LEARN repo. Use it once.
4. Write `docs/exercises/m11-agent-anatomy.md`: the loop in your own words, and the four needs for your task.

## 6. Check yourself

1. **What are the four needs for autonomy?** Clear goal, skills, tools, context.
2. **What comes back from a sub-agent to the main agent?** Only a summary.
3. **How many items per sub-agent?** Five to fifteen.
