# Module 05 — Metadata and data architecture

**Time:** 60 minutes
**Goal:** You can design a folder and file structure that agents navigate without help. You know what metadata is and why it makes agents reliable.

## 1. Why it matters

An agent finds information the way a new employee does: by reading folder names, file names, and the notes at the top of files. Bad structure means the agent reads everything or reads nothing. Good structure means it reads the right three files in ten seconds. Structure is cheap. Re-explaining is expensive.

## 2. The concepts

### 2.1 Data, metadata, instructions

- **Data:** the content. A transcript. A feed log. A price list.
- **Metadata:** data about the data. Title, date, owner, status, tags, source, which project it belongs to. Metadata is what lets an agent decide *whether* to read a file before reading it.
- **Instructions:** how to behave. CLAUDE.md, SKILL.md, README.md.

Agents work best when all three are separate and each has a predictable place.

### 2.2 Markdown is the source of truth

Every source in this course lands on the same choice: **plain Markdown files in folders.** Reasons:

- any model reads it, any vendor, any tool;
- git versions it;
- humans read it without software;
- it is cheap in tokens;
- it survives when a product dies.

Sheets, Docs, Notion and CRMs stay where they are. They are systems of record for their own data. The brain holds the narrative: strategy, SOPs, decisions, examples, and pointers to the systems of record.

### 2.3 Frontmatter: the metadata block

At the top of a Markdown file you can put a small block between `---` lines. Skills use it. Memory files use it. Use it for your own files too.

```markdown
---
title: Weekly briefing W39
date: 2026-09-21
project: tsara-erp
type: briefing
status: sent
source: dashboard export 2026-09-21
---
# Briefing semaine 39
...
```

An agent can now filter: "all briefings with status draft", "everything about project X since August". A skill's frontmatter (`name`, `description`) is what lets Claude decide to load it without reading the body. That is progressive disclosure. It only works because the metadata is there.

### 2.4 Naming rules

- **Dates first, ISO format:** `2026-09-21-briefing.md`. Sorts correctly. No ambiguity.
- **Numbered sequences:** `001-your-first-repo.md`. The highest number is the newest.
- **Kebab case, lowercase, no spaces:** `feed-conversion-analysis.md`.
- **One noun that says what it is:** `proposal`, `transcript`, `sop`, `decision`.
- **Never** `final`, `final2`, `new`, `copy of`.

Kim's LEARN repo already follows this: `lessons/001-your-first-repo.md`.

### 2.5 The CLAUDE.md router

Ben calls it "the brain file". It sits at the root of the folder. It is not an encyclopaedia. It is a **map plus rules**:

```markdown
# <Project> — how to work here

## What this folder is
One paragraph.

## Where things are (read)
- Strategy and ICP: context/
- SOPs by department: departments/<name>/sops/
- Meeting transcripts: intelligence/transcripts/YYYY-MM/
- Good examples of finished work: resources/examples/

## Where things go (write)
- Daily agent log: daily/YYYY-MM-DD.md (append, never overwrite)
- Decisions: intelligence/decisions/YYYY-MM-DD-<topic>.md
- Deliverables: docs/
- Never write to the root.

## Rules
- Read context/what-we-do.md before any customer-facing text.
- Numbers come from the systems of record, never from memory.
- Ask before deleting anything.
```

The official Claude Code guidance: keep CLAUDE.md under about 200 lines. Longer files use more context and get followed less. Split rules into `.claude/rules/*.md` if needed. Add a line when the agent makes the same mistake twice or when you type the same correction twice.

### 2.6 A business folder structure

Ben's Obsidian "AI operating system" structure. It is a good default. Rename to your language.

```
brain/
  CLAUDE.md               router + rules
  context/                team, strategy, ICP, brand, operator profile, pain points
  daily/                  one file per day: what the agents did, decisions, open questions
  departments/
    operations/sops/
    sales/sops/
    finance/sops/
  intelligence/
    transcripts/YYYY-MM/
    decisions/
    competitors/
    market/
  onboarding/             SOPs for new people and new clients
  projects/<name>/        one folder per live project
  resources/
    prompts/
    templates/
    examples/             approved outputs = the quality bar
  skills/                 reference material that skills point to
  tasks/                  to-do lists
```

Ben's note: `daily/` is "probably the most important one". It is the log. It is where the business gets smarter.

For a solo operator drop `departments/`, `onboarding/`, `teams/`.

### 2.7 Greg's product-repo structure

For a product or app, Greg's "AI employee workspace":

```
repo/
  CLAUDE.md      how Claude works here (working style, business context, quality bar)
  roadmap.md     what matters this week, and what is out of scope
  review.md      how to judge work before it ships
  app/           the product
  context/       the business brain
  customers/     sales calls, support notes, objections, customer language
  specs/         feature specs
  demos/         demo flows, scripts, screenshots
  routines/      recurring prompts
```

Three root files, six folders. The takeaway: **Claude gets far more useful when the project explains itself.**

### 2.8 Kim's structure, mapped

Your preferences already define a data architecture. It maps cleanly:

| Kim's rule | Architecture principle |
|------------|------------------------|
| One folder per project under `~/Claude/projects/` | One brain per domain |
| `CLAUDE.md` per project, wins over preferences | Router + rules, scoped |
| `patches/YYYY-MM/`, `apps/<clone>/`, `docs/`, `_parked/pull/`, `_parked/out/` | Predictable write locations |
| No loose file in the project root | Root is for the router only |
| Drive mirror: `Handover/`, `Claude/` | Metadata by audience and author |
| Every command output teed to `_parked/out/<step>.txt` | Traces are captured, not lost |

What is missing, and what this course will add: a `context/` folder with the reusable documents, a `daily/` log, and `resources/examples/`.

### 2.9 CSV as a small database

Not everything needs a real database. Ben's ideation skill keeps a CSV of every source it has already checked: source, URL, date, run time, qualified or not. The skill reads it first and skips what it has seen. A CSV with clear column names is a database an agent can read and write with no setup. Use it for dedup lists, run logs, small registries. Move to Sheets or SQLite when several people or agents write at once.

### 2.10 Systems of record and pointers

The brain does not copy the ERP. It points to it. A file `context/systems.md` says: "Fish stock is in Sheet <id>, tab Stock. Feed log is in Sheet <id>, tab Nourrissage. Read them through the Google Drive connector. Never copy their numbers into this folder." The agent then knows where truth lives and does not duplicate it.

### 2.11 Wiki links and graphs

Obsidian shows Markdown files as a graph. `[[ICP]]` inside a file links to `ICP.md`. Agents follow those links the way they follow folder names. It is optional. It helps when the brain passes a few hundred files.

## 3. How to do it in Claude

1. Create the folder tree with one prompt in Cowork: "Set up this folder as a business brain. Create the structure in section 2.6, a CLAUDE.md router, and a README in each folder that says what goes there. Ask me for missing context first. Keep version one small."
2. Point Cowork, Claude Code and any other agent at the same folder. No sync, no API.
3. Add frontmatter to every new document. Ask Claude to add it to old ones in bulk.
4. When the agent cannot find something, do not answer in chat. Fix the router.

## 4. Worked example — from scattered to navigable

Before: Tsara's SOPs are in three Google Docs, two WhatsApp threads and Kim's head. A new Cowork task asks "what is the feeding protocol for pond 3 at 26 °C?" The agent searches Drive, finds two conflicting docs, and guesses.

After: `tsara-erp/context/sops/feeding.md` holds the protocol with frontmatter `status: current, reviewed: 2026-09-01`. The old Docs are marked `status: superseded`. CLAUDE.md says "feeding rules: context/sops/feeding.md; the thresholds table in it is authoritative." The agent reads one file and answers correctly. Time to build: one hour. Payback: every session after.

## 5. Exercise (60 minutes)

1. Draw your target structure for **one** project on paper. Ten folders maximum.
2. Create it with the prompt in section 3.
3. Move or copy three real documents into it. Add frontmatter to each.
4. Write the CLAUDE.md router. Under 60 lines.
5. Test with three questions in fresh Cowork tasks. Fix the router after each miss.
6. Commit. Message: "brain v1: structure, router, three docs".

## 6. Check yourself

1. **What is metadata for?** It lets an agent decide whether to read a file before reading it.
2. **What is CLAUDE.md, in three words?** Map plus rules.
3. **Where do the ERP's numbers live?** In the system of record. The brain points to them. It does not copy them.
