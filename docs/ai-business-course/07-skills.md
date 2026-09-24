# Module 07 — Skills

**Time:** 90 minutes
**Goal:** You can build a skill from a task you did once, test it, A/B test it, and let it improve itself. Ben calls skills "the most important feature to master". This module is the longest for that reason.

## 1. Why it matters

> "Skill engineering is where prompt engineering was in 2022." — Ben
> "Anyone can build skills now in three seconds by just telling Claude to build a skill. There are going to be very few people who actually build good skills." — Ben

A prompt is used once. A skill is used forever, by you, your team and your agents. A skill is your domain expertise made into software for agents.

## 2. The concepts

### 2.1 What a skill is

Anthropic's definition: "folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks."

A skill is a folder:

```
my-skill/
  SKILL.md            the process. Frontmatter: name, description.
  references/         text files: examples, style guides, ICP, tool instructions
  assets/             non-text examples: images, decks, templates
  scripts/            optional code Claude runs (Python, JS)
```

The `description` in the frontmatter is what Claude reads to decide whether to load the skill. The body loads only when the task matches. Reference files load only when a step says so. This is progressive disclosure. It is why one agent can have thousands of skills without filling its context window.

The Neo picture: in *The Matrix* Neo uploads kung fu into his brain. A skill is that for an agent. Anthropic's short version: **projects store knowledge; skills perform tasks.**

### 2.2 Where skills sit between automations and chats

Ben's framing:

| Approach | Strength | Weakness |
|----------|----------|----------|
| Custom GPT / old project | Easy | Isolated. Does not self-improve. Small context. |
| n8n / Make automation | Deterministic. No human needed. | Breaks when judgement is needed. Most daily work needs judgement. |
| **Skill** | Process + judgement + human checkpoints. Self-improving. Shareable. Thousands per agent. | Needs care to build well. |

### 2.3 Two ways to build a skill

**Way 1 — do it once, then save it.** Do the task in a chat with Claude. Correct it as you go. When the output is good, say: "Please save this as a skill." Claude has the full context, including your corrections. Ben recommends this way for most people and most tasks.

**Way 2 — describe it up front.** When the process is already proven (an old custom GPT, a written SOP), paste it and ask for the skill.

**Way 3 — import and adapt.** Download a skill from a marketplace or an Anthropic plugin. Then: "Adjust this skill. Add my outreach templates and my ICP." Anthropic's built-in skills have "Customize with Claude".

Claude Academy's default: Claude interviews you and writes the skill.

### 2.4 Prepare before you prompt

The step most people skip. Before you ask for a skill:

1. Think through the ideal step-by-step process. Where are the decision points?
2. List the knowledge sources that improve each step. What we do. ICP. Voice. Examples. Tool instructions.
3. List the tools or connectors the skill needs.

Ben spends 30–60 minutes here. He says it makes output ten times better.

### 2.5 The skill prompt framework

Ben's structure. Use it as a checklist when you ask Claude to build a skill.

1. **Name and trigger.** "The skill is called `weekly-briefing`. Trigger it whenever I ask for the weekly briefing, the point hebdo, or the staff update."
2. **Goal.** One sentence. "Produces the French weekly staff briefing from the live dashboard."
3. **Connectors, APIs, MCPs.** Name them. Name the specific sheet, tab, page, or folder.
4. **Step-by-step process.** For each step:
   - what it does;
   - is there a human-in-the-loop checkpoint? which widget: checkboxes, single select, free text;
   - which reference file to read at this step (make it an obligatory step, or "it tends to skip");
   - the expected output.
5. **Keep SKILL.md clean.** Process only. Everything else in reference files.
6. **Ask for variations at checkpoints.** Five angles. Three outlines. Ten subject lines.
7. **Rules section.** Predict what goes wrong. Write a rule for each. This section grows the most over time.
8. **Progressive update.** "Every time the user says not to do something anymore, update the rules section. When the user approves a final output, save it as a good example in references/examples/."

### 2.6 Reference files

Three kinds:

- **Text:** example outputs, style guides, ICP, background, and *tool instruction files* ("how to use the Apify LinkedIn scraper in this process"). Claude can write the tool files itself after using the tool once.
- **Assets:** images, decks, videos as examples of the target output.
- **Scripts:** small programs that call an API. Ben's infographic skill has a Python script that calls an image model.

The single most valuable reference file: **good examples of finished work**.

### 2.7 Thin skills and the shared brain

Once you have a brain (module 05), skills get thinner. SKILL.md points to `brain/context/icp.md` instead of holding a copy. Update the ICP once, and dozens of skills improve. Ben migrated his skills with: "Adapt my LinkedIn skill. Instead of reference files inside the skill, point to the files in the brain."

### 2.8 Testing skills: evals

Anthropic's updated **skill-creator** skill can test a skill. After creating one, Claude asks "want me to run some test cases?" It spins up parallel sub-agents, runs the skill, grades against criteria, and produces a report: prompt used, steps, output, pass/fail per criterion, and a feedback box you can copy back into chat.

Rules for useful evals:

- **Optimise one thing at a time.** "Don't try to optimize five or six different things at the same time."
- **State the criteria.** Ben's example: "how closely does it follow the example references; does it use em dashes; length; does it include a personal story from the background file."
- **State the test design.** Same input, five variations. Or three different inputs.
- A vague "run some tests" only smoke-tests. Claude invents the criteria.

Ben's first run: style match failed 2 of 5. Word count failed 1 of 5. Claude proposed two rule changes. He applied them and re-uploaded. Second run: better. That is the loop.

### 2.9 A/B testing skills

Only once a skill works. "Use the skill-creator skill to run an A/B test on the newsletter skill to optimise for speed. It cannot change the step-by-step process. Reference files must still be read." Claude writes version B itself. The report has a benchmark tab.

Ben's result: A = 93,000 tokens, 204 seconds. B = 77,000 tokens, 160 seconds. B failed one step because a tool behaved differently that run. He re-ran, confirmed, and adopted B. Single runs are noisy. Re-run before you decide.

Also test *context*: one variant with all eight reference files, one without the voice file. Read both. Keep what helps.

Anthropic's advice: when a new model ships, A/B test skill vs no skill. Some skills become unnecessary.

### 2.10 Skill chains and commands

Theo's **skill chain**: a macro skill that fires skill 1, then skill 2, then skill 3. His proposal chain: build microsite → copy pass → QA pass → deploy → Slack ping. His product chain: hypothesis → build prototype → usability test → synthesise feedback → plan V2.

In Cowork the same thing is a **command**: one text file that lists the skills to run in sequence. Ben's `repurpose` command: LinkedIn writer → newsletter writer → diagram → GIF → infographic, from one input. Invoke with `/repurpose`. Build commands only after the skills work. Commands can be scheduled.

### 2.11 Skills in Claude Code

Same idea, file locations:

- personal: `~/.claude/skills/<name>/SKILL.md`
- project: `.claude/skills/<name>/SKILL.md` (shared through git)
- invoke with `/<name> [arguments]`, or Claude invokes it when the description matches.

Kim already has project skills: `erp-audit`, `erp-handover`, `briefing-hebdo-tsara`, `learn-capture`. They follow exactly this pattern.

### 2.12 Marketplaces and sharing

Three layers exist: Anthropic's built-in skills and plugins; public marketplaces (skillsmp, Smithery and others) where people publish; your own company-level and person-level skills. To share: ask Claude for a zip → teammate uploads it; or host on GitHub for a versioned link. Only install skills from sources you trust. A skill can contain code and instructions. Treat it like software.

## 3. How to do it in Claude — build one now

Use the weekly briefing as the example. Replace with your own task.

**Step 1 — do it once (30 min).** In the tsara-erp project: "Read the dashboard export. Suggest five angles for this week's briefing." Pick one. "Give me three outlines. Read `resources/examples/briefing-good.md` first." Pick one. "Write it. Mimic the tone, sentence length and structure of the example. Base every warning on a row of the export. Then review it against the example." Correct what is wrong. Note each correction.

**Step 2 — save it (5 min).**

> Save this as a skill called `weekly-briefing`. Trigger: whenever I ask for the weekly briefing, point hebdo, or staff update. Follow the exact process we just did. Include every reference file we used. Make reading the example file an obligatory step before writing. Add my corrections as rules. Add a progressive-update rule: when I say "don't do X anymore", update the rules; when I approve the final, save it to references/examples/.

**Step 3 — test it (15 min).** "Run three test variations of the weekly-briefing skill on last week's export. Optimise for: every warning traceable to a CSV row. Criteria: traceability, length under 400 words, French, three sections."

**Step 4 — fix and re-upload (10 min).** Apply the proposed rule changes. "Copy to your skills" → "upload and replace".

## 4. Worked example — the newsletter skill

Ben's `YouTube to newsletter` skill, built by doing it once:

1. Get the transcript through a scraper tool, not by pasting, so the skill can do it alone later.
2. Read ICP and newsletter strategy. Suggest five angles. Human picks.
3. Read the example newsletters. Suggest three outlines. Human picks.
4. Write. "Follow the exact style and tone of the examples. Almost mimic sentence structure and length. Base claims on what I said in the video. Read the background doc for stories. Reread ICP and strategy. Read what-we-do for the call to action. Review against all of the above before output."
5. Ten subject lines, three to eight words, lower case.

Six to eight reference files. Corrections during the run became rules. Then evals. Then an A/B test for speed. Now one link in, one newsletter out, in his voice.

## 5. Exercise (90 minutes)

1. Pick one task you do every week. Do it once with Claude, following section 3. Save it as a skill.
2. Run three test variations with one optimisation goal. Apply the fixes.
3. Write down the token and time numbers from the eval report in `docs/exercises/m07-skill-eval.md`.
4. Add to the skill's rules: "Never finish without listing the sources used."
5. Run it once more by name from a fresh chat. Does it fire from the trigger words alone?

## 6. Check yourself

1. **What is in SKILL.md and what is not?** The process. Everything else goes in reference files.
2. **Why make reading a reference file an obligatory step?** Otherwise the agent tends to skip it.
3. **How many things do you optimise in one eval run?** One.
