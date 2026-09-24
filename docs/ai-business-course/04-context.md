# Module 04 — Context

**Time:** 60 minutes
**Goal:** You understand that context is the moat. You can build the context layer that gives your agents 20/20 vision of your business.

## 1. Why it matters

> "Context is really the key to get good outputs with AI." — Ben
> "The context I think will be your actual moat in the upcoming months and years." — Ben
> "You have to make your company readable to agents." — Theo Tabba

Models are a commodity. Everyone has the same Claude. What you alone have is your business knowledge, written down where agents can read it. That is context. The company that writes it down wins.

## 2. The concepts

### 2.1 Two meanings of "context"

1. **The context window.** The fixed space the model reads at once. A technical limit. Module 01.
2. **The context layer.** Everything about your business that agents can read: strategy, customers, processes, decisions, examples, history. A business asset.

The skill is to put the right slice of the context layer into the context window at the right moment. That is called **context engineering**.

### 2.2 Why chat history is not context

A chat is gone when it ends. Memory keeps a few facts. Neither holds your SOPs, your pricing history, your customer language or last week's decisions. Those must live in files. Files persist. Files are shared. Files are versioned. Files can be read by any agent from any vendor.

### 2.3 The first-day test

Theo's test: imagine a smart new hire on day one, asked to write the board deck for next week. She has a fuzzy goal, some skills, no tools and no context. She will fail. Not because she is stupid. Because nothing is in front of her.

Every agent starts every session on day one. **Your context layer is the onboarding pack it reads in the first minute.**

### 2.4 The loop: capture → curate → store → execute → experience

Theo's model of how context flows in an AI-native business:

1. **Capture.** Information arrives from many tools: email, meeting transcripts, Slack, sheets, forms. A routine collects it into an inbox folder every hour or two.
2. **Curate.** A "librarian" step reads the inbox, cleans, files, discards, and detects triggers ("they asked for a proposal").
3. **Store.** The brain: folders of Markdown files, organised so agents can search, retrieve and write back.
4. **Execute.** People direct agents. Agents read the brain, do the work, produce artifacts.
5. **Experience.** Customers use the output. Their reaction is signal. Signal flows back to capture.

Plus the **traces**: the decisions, drafts and dead ends made along the way. Most businesses lose them. An AI-native business files them, because "why did we decide that" is a question agents get asked a lot.

### 2.5 The brain is just folders and Markdown

Theo showed his on GitHub. Ben showed his in Obsidian. Greg's is a repo with `/context`, `/customers`, `/specs`. All three are the same thing: **a folder tree of Markdown files with README or CLAUDE.md files that guide the agent through the tree.**

No database. No vector store. No vendor lock-in. Any agent — Cowork, Claude Code, Codex, anything — can read it. Module 05 gives the structure.

### 2.6 The reusable context documents

Ben's set for marketing and sales. Adapt the names to your business.

| Document | What it holds |
|----------|---------------|
| **What we do** | The business in one page. Products. Prices. Promise. |
| **ICP** (ideal customer profile) | Who buys. Their words. Their pain. |
| **Voice / personality** | Tone attributes. Signature phrases. What we never say. |
| **Channel strategy** | Newsletter, LinkedIn, WhatsApp — what each is for. |
| **Writing framework** | How a piece is structured. |
| **Good examples** | Finished work you are proud of. "The thing that impacts performance the most." |
| **Background / operator profile** | Who you are. Your story. Your failures. |
| **Pain points** | Repeated customer complaints and objections, in their words. |

For a farm the list changes shape but not nature: what we produce, who buys, price list, SOPs, thresholds, seasonal calendar, past incidents, good examples of briefings and reports.

### 2.7 Build the documents with the model

Do not write them alone. Ben's method:

> "I want to create a <strategy document> that I can later give when I'm building skills for research, ideation, scripting. Interview me. Ask me questions one by one. Then write the document."

Budget 30 to 60 minutes per document. Ben says outputs become "ten times better" after this step. It is the step most people skip.

If you have a template from someone else: "This document is from someone else. I want the same format adapted to my business. Analyse it and ask me questions so you can build me a similar doc."

### 2.8 Bootstrapping context when you have none

Greg asked Theo: "I don't have 55 experts' worth of context. How do I start?" Theo's answer:

- The world is large. Other people have produced good work. Find libraries of it (Mobbin for app design, public SOPs, industry reports). Wrap them in a skill.
- Use an MCP that exposes a library of examples.
- Give the agent a clear goal and the right tools. Load context slowly over time.
- Start with five files. Do not over-optimise. The structure evolves.

### 2.9 Progressive disclosure

Do not dump the whole brain into every prompt. Skills load only when triggered. Reference files load only when a step needs them. CLAUDE.md points; it does not contain. Ben's rule: "Keep the SKILL.md very clean and focused on the process. Any additional information should be in the reference files." The agent reads what it needs when it needs it. The window stays clean.

### 2.10 Write-back

Context is not read-only. Agents write back: a log of what they did today, a decision record, a new rule, an approved output saved as a good example. Ben says "remember this in my second brain" and names the target file. Theo's brain "improves over time" because agents write to it. Module 12 covers the loops that do this.

## 3. How to do it in Claude

- **Attach the folder, not the file.** In Cowork, grant the context folder once. Every task can read it.
- **Project knowledge.** Upload the reusable docs to the project. When knowledge grows large, Claude switches to a retrieval mode automatically (up to about 10× capacity on paid plans).
- **CLAUDE.md as router.** Put one at the root of the folder. It says: "Strategy is in `context/strategy.md`. Customer language is in `customers/`. Save daily logs to `daily/YYYY-MM-DD.md`." Module 05.
- **Memory for the essentials only.** Name, role, language, format rules. Everything else in files.
- **When it gets lost:** tell Claude to update CLAUDE.md with a navigation rule. Or edit it yourself.

## 4. Worked example — the proposal that wrote itself

Theo's LCA demo. A prospect asks for a proposal in an email. A routine picks up the trigger. It fires a skill chain: build a proposal microsite → tune the copy to Theo's voice → QA for over-promises and invented facts. Five minutes later Theo gets a Slack ping with a live link.

The proposal quotes a line the prospect said months ago in the first intro call: "the person behind the counter hands you something and says, trust me." Theo had forgotten it. The brain had not. The meeting transcript was filed under `spotify/meetings/`. The skill was told to pull personal moments from transcripts.

Result: proposals that took three days now take minutes. LCA says this is a big reason they close large deals. The model did nothing magic. **The context did the work.**

## 5. Exercise (60 minutes)

1. List the five documents your agents would need most. Use the table in 2.6 as a start.
2. For the first one, run the interview prompt from 2.7 in your AI course project. Let Claude ask you questions. Answer by dictation if you can. Save the result to `learn/docs/context/<name>.md`.
3. Add a line to the LEARN CLAUDE.md (or create it): where the context docs live and when to read them.
4. Test: in a fresh Cowork task, ask something only that document can answer. Do not attach it. Check that the agent finds it through CLAUDE.md.

## 6. Check yourself

1. **What is the difference between the context window and the context layer?** The window is the technical space the model reads at once. The layer is your written business knowledge that agents can read.
2. **What is the brain made of?** Folders of Markdown files, with README or CLAUDE.md files that route the agent.
3. **What document improves output quality the most, according to Ben?** Good examples of finished work.
