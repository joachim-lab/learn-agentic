# Module 16 — Business use cases

**Time:** 45 minutes
**Goal:** You have a catalogue of proven use cases, each with the problem, the AI approach, the result, and the modules it needs. You pick the five with the best return for your business.

## 1. Why it matters

Theo, quoting Demis Hassabis: "Running 100 miles an hour in the wrong direction is worse than standing still." Speed only pays in service of the customer. This module is about direction: which loops, skills and agents to build first.

## 2. Catalogue

Each entry: **Problem → Approach → Result → Needs (modules).** Sources in brackets.

### 2.1 Sales and revenue

1. **Proposal in five minutes** [Theo]. Problem: proposals take three days; prospects cool off. Approach: trigger on "send me a proposal" in email or transcript → skill chain: microsite → copy in your voice → QA against transcripts → deploy → Slack ping. Personal moments pulled from past calls. Result: minutes instead of days; LCA credits it with large deals closed. Needs: 04, 07, 08, 12.
2. **Outbound pipeline on 150 leads** [Ben]. Problem: qualification and enrichment do not fit one context. Approach: 15 sub-agents qualify, 18 enrich, 17 write icebreakers; saved as a plugin with one command. Result: 82 qualified in two minutes, 37 personalised messages. Needs: 07, 08, 11, 15.
3. **Warm leads from post engagers** [Ben]. Approach: scrape who engaged with a target's LinkedIn post → dedupe → qualify against ICP → enrich → CSV. Result: 127 engagers, 17 qualified. Needs: 08, 11.
4. **CRM prospect miner** [Ben]. Problem: lost leads never revisited. Approach: skill scans the lost column, sub-agents read LinkedIn and email history, prioritise. Result: 160 records ranked with a comms summary. Needs: 08, 11.
5. **Call prep every morning** [Ben, Anthropic plugin]. Approach: daily 07:00 for each meeting: CRM, emails, transcripts, web → HTML brief with agenda and discovery questions. Needs: 08, 09, 12.
6. **Win/loss analysis** [Ben]. Approach: read won and lost deals, transcripts, emails → win rate, best and worst profiles, objections, red flags. Finding: "we have to get far better at follow-ups". Needs: 04, 08.
7. **Rep performance coaching** [Ben]. Approach: per rep: grade, three strengths, three improvements, per-stage scorecard. Needs: 04, 08.
8. **Pipeline review to Slack** [Ben]. Daily: hot and at-risk leads DM'd. Needs: 08, 12.
9. **Failed-payment recovery** [Ben]. Daily: yesterday's failed payments → email history → classify → type-specific draft → Gmail draft. "Already making an impact on revenue." Needs: 07, 08, 12.

### 2.2 Product and customers

10. **Functional prototype in ten minutes** [Theo]. Problem: PRDs take weeks; nobody can feel them. Approach: a goal command → skill chain with design-system skill and a UI library MCP → deployed on a Labs page. Result: a working feature in the brand's design system, tested live. Needs: 07, 08, 09.
11. **Usability test + synthesis + V2** [Theo]. Approach: the prototype ships with a test flow; answers collected in the page; "synthesise" skill produces lessons; "plan V2" skill executes. Result: feedback and a second version in the same session. Needs: 09, 11, 12.
12. **Production watchdog** [Ryan]. Daily 09:00: every event for paying customers → JSON → admin page with links to the real screens. "You think you know what's going on, but you don't." Needs: 08, 09, 12.
13. **Self-improvement grader** [Ryan]. Daily: grade the product agent's conversations on a rubric; below the bar → child session opens a fix. About three shipped fixes a day on a cheap model. Needs: 11, 12, 14.
14. **End-to-end sign-up test** [Ryan]. Three times a week: a cloud agent clicks through sign-up, onboarding and the core flow in a browser, records video, fixes what it finds, triggers a triage session on failure. About 60 dollars in tokens per run. Needs: 08, 12, 14.
15. **Customer-language mining** [Greg]. Skill: read latest calls and support notes → exact customer words, repeated objections, buying triggers. Feeds landing pages, ads and demos. Needs: 04, 07.
16. **Landing-page teardown** [Greg]. Skill: look at the page as the buyer; five-second clarity; vague copy; missing trust; CTA; one focused fix. Needs: 03, 07.
17. **Demo script from notes** [Greg]. Skill: latest product state + customer notes → pain, product moment, payoff. Needs: 04, 07.

### 2.3 Operations and knowledge

18. **Morning brief** [Greg]. Weekday 07:00: top customer pain, one risk, one build task, one question to ask customers. Read-only. Needs: 12.
19. **Weekly ops review** [Greg]. Friday: group issues, find duplicates, one highest-leverage fix. Needs: 12.
20. **Meeting digest** [Ben]. Daily: transcripts → tasks, process updates, overview, next-day agenda in Notion. Needs: 08, 12.
21. **Monthly accounting pre-work** [Ben]. First of month: Gmail, Stripe, web, browser → update the spreadsheet; pings for input. Needs: 08, 12.
22. **Capture → curate → brain** [Theo]. Hourly capture from all tools; librarian curates; triggers detected. Needs: 04, 05, 12.
23. **Second brain in Obsidian** [Ben]. One folder, one CLAUDE.md router, every agent points at it. "What should I focus on today?" answered from the vault. Needs: 04, 05.
24. **SOP and process documentation** [Anthropic operations plugin]. Formalise a process from someone's head: flow, RACI, SOP. Needs: 04, 09.
25. **Vendor review / risk register / status report** [Anthropic operations plugin]. Ready-made skills; customise with your context. Needs: 07.

### 2.4 Marketing and content

26. **YouTube → newsletter in your voice** [Ben]. Skill with transcript tool, 6–8 reference files, five angles, three outlines, ten subject lines; evals and A/B tests. Needs: 07.
27. **Content repurposing chain** [Ben]. `/repurpose`: LinkedIn → newsletter → diagram → GIF → infographic from one input. Needs: 07, 15.
28. **Brand-aligned infographics** [Ben]. Brand guide file + image model behind a tool + HITL choices. Needs: 07, 08, 09.
29. **Newsletter ideation dashboard** [Ben]. Daily scan of five sources, CSV dedup database, HTML report. Needs: 05, 09, 12.
30. **Analytics dashboard** [Ben]. Channel CSV → HTML dashboard → cross-referenced with transcripts for best hooks and formats. Needs: 09.
31. **SEO audit and optimiser** [Ben]. Audit skill (compliance, performance, E-E-A-T, GEO) + optimiser + website MCP → "almost autonomous" upkeep. Needs: 07, 08.

### 2.5 Tsara Tilapia — the local list

32. **Morning pond brief** (module 12 example). Warnings by pond with evidence rows. Needs: 08, 12.
33. **Weekly staff briefing in French** (`briefing-hebdo-tsara`). Already a skill. Add evals against the best example. Needs: 07.
34. **Feed-conversion analysis on demand from the phone** (module 13 example). Needs: 08, 13.
35. **ERP static audit** (`erp-audit`). Weekly, read-only, reports duplicated constants, wasted runtime, clones that drift from live. Needs: 07, 12.
36. **Handover generator** (`erp-handover`). End of session → Google Doc in Handover/. Needs: 09.
37. **Patch pipeline**: plan mode → heredoc patch with anchor asserts → Kim deploys → Claude reads `_parked/out/`. Needs: 03, 06, 14.
38. **Supplier price watch**: weekly browser task on feed and fingerling suppliers → CSV → alert on change. Needs: 08, 12.
39. **Cold-chain and delivery planning**: from orders and the seasonal calendar, draft the week's harvest and packing plan; human approves. Needs: 04, 07.
40. **Investor monthly report**: from the four weekly briefings and the dashboard → French docx or Slides. Needs: 09.

### 2.6 Service businesses built on this

Theo's startup thesis: package this system as a service for one niche. Pick industry × function × company size (restaurants, dentists, real estate...). Start with **niche, high-frequency** workflows you can demo on a sales call. Then general high-frequency. Then niche high-value low-frequency. Ryan's sector: family law, as an "AI divorce agent for divorce firms". Greg: "If Late Checkout spun up five new companies, it would be this times five with different industries."

## 3. Speed impact (Theo's table)

| Task | Before | After |
|------|--------|-------|
| Proposal | up to 3 days | minutes |
| Functional prototype | 1–2 weeks | minutes |
| Collect and synthesise user feedback | days | same session |

## 4. How to pick your five

Score each candidate 1–5 on four axes: **frequency**, **time it costs you today**, **risk if wrong**, **how much context you already have written down**. Multiply frequency × time. Divide by risk. Prefer high context. Build the top five. Start with read-only ones.

## 5. Exercise (45 minutes)

1. Copy the catalogue into `docs/exercises/m16-use-cases.md`. Delete what does not apply. Add five of your own.
2. Score them with the formula in section 4.
3. Write the top five as tickets with the four parts (module 03).
4. Put the first one on this week's roadmap.md.

## 6. Check yourself

1. **Which use case should you build first?** A high-frequency, read-only one with context already written: the morning brief.
2. **What made Theo's proposal personal?** Meeting transcripts filed in the brain, and a skill told to pull personal moments from them.
3. **What is the niche formula for a service business?** Industry × function × company size; start with high-frequency niche workflows.
