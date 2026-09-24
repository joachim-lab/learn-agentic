# Module 03 — Prompts and instructions

**Time:** 60 minutes
**Goal:** You write prompts that an agent can finish without guessing. You know the difference between a prompt, a ticket, a brief and a standing instruction.

## 1. Why it matters

Greg Isenberg's rule: **once the model starts guessing, you are no longer managing the work. You are cleaning up the work.** Good prompts remove guessing. They are the cheapest lever you have.

## 2. The concepts

### 2.1 Four kinds of instruction

| Kind | Lives | Lifetime | Example |
|------|-------|----------|---------|
| **Prompt** | One message | One turn | "Give me five subject lines." |
| **Ticket** | One message | One task | "Add a waitlist form with name, email, company and a success state." |
| **Brief / plan** | Start of a task | One task | "Use plan mode. Inspect the app and the three MD files. Propose the smallest change. Wait for approval." |
| **Standing instruction** | Preferences, project instructions, CLAUDE.md, skills | Forever | "Never save to the Drive root." |

Beginners put everything in prompts. Pros push everything durable into standing instructions and keep prompts short.

### 2.2 The three-part prompt (Claude Academy)

1. **Set the stage.** Role, objective, context. "You are the operations assistant of a tilapia farm in Réunion. We prepare the weekly staff briefing."
2. **Define the task.** One clear outcome. "Write the briefing for week 39 from the attached dashboard export."
3. **Specify rules.** Style, tone, format, length. "French. Short sentences. Three sections: status, warnings, actions. Under 400 words."

Talk to Claude like a capable colleague. Natural, concise, conversational. Do not write in keywords.

### 2.3 The ticket

A ticket is a small, clear assignment with a visible finish line. It has four parts:

- **the job** — what to do;
- **the scope** — what it includes;
- **the expected result** — how you will know it is done;
- **the boundary** — what not to touch.

Good tickets from the "99%" video:

- "Create a pricing page using the existing design system. Keep it consistent with the home page."
- "Fix the onboarding redirect bug after email verification."
- "Turn these five customer objections into a sharper landing-page section."

Bad tickets: "Make the app better." "Make this pop." "Add AI." "Build the whole thing."

Rule: **one ticket, one finish line, one reviewable change.**

### 2.4 The brief and plan mode

For meaningful work, talk it through before the agent touches anything. In Claude Code and Cowork this is **plan mode**. The agent reads the context, thinks, and shows the approach. You react. Then it executes.

The brief template:

```
Use plan mode.
I want to <outcome>.
First inspect <files, folders, CLAUDE.md>.
Then give me: the files that need to change, the smallest clean
implementation, the user experience, the risks, how we verify it,
and what you leave out of version one.
Wait for my approval before editing.
```

Measure twice, cut once. Plan mode is the measuring.

### 2.5 The execution prompt

After the plan is approved:

```
Implement the approved plan as one focused change.
Keep it small enough to review in the diff view.
After editing, run the relevant checks.
Summarise: what changed, what you tested, what still needs human review.
```

### 2.6 The inspection prompt ("eyes")

Do not stop at "done". Ask the agent to use what it built.

```
Start the app and inspect the flow.
Check it from the point of view of <the user> seeing it for the first time.
Tell me what they understand in five seconds, what feels confusing,
whether the form works, what happens after submission.
Then make one focused pass on the highest-impact issue.
```

### 2.7 The review prompt

```
Use review.md as the standard.
Review the current changes for production issues, broken edge cases
and confusing flows.
Separate into: must fix / should fix / OK to ship.
Flag files changed outside the ticket's scope.
```

### 2.8 Ask for variations, not one answer

Ben's habit: at every decision point ask for several options. "Five angles." "Three outlines." "Ten subject lines." You pick. This uses your judgement where it counts and saves rounds of correction.

### 2.9 Ask the model to ask you

Add this line to any setup prompt: **"Before you start, ask me for any missing context that would materially change the result."** The model then interviews you. This is how Ben builds strategy docs in 30–60 minutes. It is also how Claude Academy suggests building a skill: Claude interviews you and writes it.

### 2.10 Corrections become rules

Every time you correct the model, decide: is this a one-off, or a rule? If it is a rule, it goes into a standing instruction. Ben's skills have a rule "every time the user says not to do something anymore, update the rule section." That is how the system gets smarter over time.

### 2.11 Troubleshooting table (Claude Academy)

| Symptom | Fix |
|---------|-----|
| Generic answer | Add context. Attach the file. Name the audience. |
| Wrong length | State the length. "Under 300 words." |
| Wrong format | Show an example of the format you want. |
| Made-up facts | Give the source. Ask it to mark unsupported claims. |
| Wrong tone | Describe the style. Give two examples of your voice. |

## 3. How to do it in Claude

- **Plan mode:** in Claude Code, press Shift+Tab to cycle modes, or write "use plan mode". In Cowork, ask for a plan first.
- **Dictation:** the desktop app and mobile app take voice. Long briefs are faster spoken. Ben and Ryan both dictate most prompts (Wispr Flow or the native mic).
- **Slash commands:** `/schedule`, `/review`, `/init` and your own skills. Type `/` to see them.
- **Attach, do not paste.** Attach a file, or grant a folder. Pasting fills the context window with noise.

## 4. Worked example — from vague ask to ticket

**Vague:** "Improve the weekly briefing."

**Ticket:**

> Read `docs/briefings/2026-W38.md` and the dashboard export in `data/dashboard-W39.csv`. Write `docs/briefings/2026-W39.md`. Same three sections as W38. French. Each warning names the pond, the metric, the threshold and the action. Under 400 words. Do not change any file in `data/`. When done, list every warning you included and the row of the CSV it came from.

The second version has a job, a scope, a result, a boundary and a verification step. An agent can finish it. You can check it in two minutes.

## 5. Exercise (45 minutes)

1. Take three tasks from your real to-do list. Write each one first as you would say it. Then rewrite it as a ticket with the four parts.
2. Run one ticket in Cowork with plan mode. Read the plan. Change one thing. Approve. Read the result.
3. Note every correction you made. For each one decide: one-off, or rule? Put the rules in the project instructions of your AI course project.
4. Save the three tickets in `docs/exercises/m03-tickets.md`.

## 6. Check yourself

1. **What are the four parts of a ticket?** Job, scope, expected result, boundary.
2. **When do you use plan mode?** For any meaningful task before the agent touches anything.
3. **What happens to a correction that is really a rule?** It moves into a standing instruction: preferences, project instructions, CLAUDE.md or a skill.
