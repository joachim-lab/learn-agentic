# Module 09 — Artifacts and outputs

**Time:** 45 minutes
**Goal:** You ask for the deliverable, not the text. You know which output shape to request for each business need, and where it should live afterwards.

## 1. Why it matters

Claude Academy's tip: **"Ask for the deliverable, not just the content."** Text in a chat is not delivered. A file in the right folder, a shared page, a deck the investor can open — that is delivered. Kim's own rule says it: "A file that exists only in chat is not delivered."

## 2. The concepts

### 2.1 What an artifact is

"An artifact is anything Claude makes for you that you'd put in front of someone: a design, a deck, a document, a dashboard, or a small interactive tool." It opens in a panel beside the chat. On paid plans it lives in the Artifacts tab, survives the chat, can be edited, shared and published.

> "Think of the conversation as where you create, and the Artifacts tab as where your outputs live." — Claude Academy

### 2.2 Output shapes and when to use each

| Need | Shape | Why |
|------|-------|-----|
| Something people read and edit together | **Claude Docs** or a Markdown file | Living document. Comments. Versions. |
| Something to present | **Claude Slides** | Editable deck. Export to PowerPoint or PDF. |
| A visual, a mockup, a landing page | **Claude Design** | Judged by looking at it. |
| Numbers to sort, filter, calculate | **Sheet** (Sheets artifact or xlsx) | Formulas. Rows. |
| A thing people open again: dashboard, tracker, calculator, status page | **Published HTML artifact** | Own URL. Shareable. Updatable. |
| A diagram or board to work on together | **Whiteboard** | Shared canvas. |
| Code someone will run | **A file** in the repo | The file is the deliverable. |
| A one-off chart "just to see" | Inline image or HTML in chat | Do not clutter the gallery. |

Kim's standard is Markdown for everything meant to be read. That overrides the table for reading documents. Slides, sheets and dashboards keep their shapes.

### 2.3 Artifacts as micro-products

Theo's proposal microsite is an artifact: a branded page, deployed on a link, personalised from the meeting transcripts. His Labs page with a functional prototype and a usability test is an artifact. Ben's newsletter-ideation dashboard and YouTube analytics dashboard are HTML artifacts. Ryan's production watchdog writes a JSON that an admin page renders.

The pattern: **an artifact is the fastest way to put something real in front of a customer or a colleague and get signal.** A functional prototype in ten minutes beats a forty-page spec in ten days.

### 2.4 Artifacts that keep state

A published artifact can do more than display. It can remember what viewers do (a poll, a sign-up sheet, a checklist), keep shared data, know who is viewing, and ask Claude a question. Theo's usability test collected answers in the page and a "synthesise" button ran another skill on them. Ask for these capabilities when the page is a tool, not a report.

### 2.5 Files: where they go

For files, the rule is the one in Kim's preferences and in module 05:

- deliverables go into the project folder, in the right subfolder;
- Drive mirror: `Handover/` for handovers and chat transfers, `Claude/` for everything else Claude makes;
- never the Drive root; always pass the folder ID;
- a chat transfer summary is a Google Doc; everything else meant to be read is Markdown.

The agent should write the file, list the folder to confirm it exists, and then tell you the path. That is delivery.

### 2.6 Editing artifacts

Three ways: ask Claude in chat; edit directly inside template artifacts (Docs, Slides, Design); highlight text and "Edit with Claude". Leave comments on a shared artifact; Claude can read and answer them.

### 2.7 Quality bar for outputs

Greg's `review.md` for a landing page: clear in five seconds, CTA visible, copy in the customer's words, works on mobile, no unnecessary complexity. Write the equivalent for each output type you produce often. Put it in `resources/examples/` next to a good example. Skills read both before producing.

### 2.8 Images

Claude does not have a photo-realistic image model of its own. It can draw with code (SVG, charts, HTML) and it can call an image model through an MCP or a script. Ben's infographic skill calls Google's Gemini image model through an API key and a brand-guideline reference file. If you need branded visuals at volume, that is the pattern: brand guide in a file, image model behind a tool, skill in front.

## 3. How to do it in Claude

- "Turn these notes into a one-page doc" → Docs artifact.
- "Make this a deck for the bank, eight slides, French" → Slides.
- "Build a tracker for pond stocking dates I can update from my phone" → published HTML artifact with stored state.
- "Save the report as `docs/reports/2026-09-feed-analysis.md`" → file in the repo.
- Always add: "Then list the folder and give me the path."

## 4. Worked example — from report to tool

Kim asks for "a summary of warnings by pond". Version one is a Markdown report. Useful once.

Version two: "Build a dashboard page that reads the warnings CSV, groups by pond, colours by severity, and lets me tick a warning as handled. Publish it. I will open it every morning." Now it is a tool the whole team opens. Republish when the CSV changes. Same data, different shape, ten times the use.

## 5. Exercise (30 minutes)

1. Take one report you produce regularly. Ask Claude for it as three shapes: Markdown, Slides, and a published dashboard.
2. Open each on your phone. Which one would the reader actually use?
3. Write a `review.md` for that output: five yes/no questions a good version passes.
4. Save the best version in the right folder and confirm the path.

## 6. Check yourself

1. **What is the Claude Academy rule about outputs?** Ask for the deliverable, not just the content.
2. **When does an HTML artifact deserve to be published rather than sent once?** When people will open it again: dashboard, tracker, tool, status page.
3. **When is a file "delivered", in Kim's rules?** When it exists in the project folder and the agent has listed the folder to confirm.
