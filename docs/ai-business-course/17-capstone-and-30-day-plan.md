# Module 17 — Capstone and 30-day plan

**Time:** 30 days
**Goal:** You operate an AI-native business. Agents read and write to it. It gets smarter every day. You make the decisions.

## 1. The seven-day core (Greg's plan, adapted)

Greg: "You can do this in seven hours, seven days or 31 days." The order matters more than the pace.

| Day | Do | Output |
|-----|----|--------|
| 1 | **Repo brain.** CLAUDE.md, roadmap.md, review.md, /context, /customers. Write the customer, the problem, the current goal, the definition of done. | A folder that explains itself |
| 2 | **Plan mode.** One small task. Make the agent inspect the repo before editing. | A plan: files, risks, verification steps |
| 3 | **One visible improvement.** Small enough to review. Real enough to show a customer. | One reviewable change |
| 4 | **The eyes.** Agent opens the result, clicks through, checks mobile, improves clarity. | One focused fix |
| 5 | **Review.** Diff view. Agent reviews against review.md. Deep review for anything serious. | must / should / OK list |
| 6 | **Ship to ten people.** Send the thing. Put their replies into /customers. | Ten pieces of signal |
| 7 | **First routine.** Morning brief: read notes and issues, recommend one build task. | A loop that is alive |

The final loop: customer feedback → `/customers`; direction → `roadmap.md`; working style → `CLAUDE.md`; quality → `review.md`; small tasks → plan mode; changes → preview and review; recurring work → routines.

## 2. The 30-day plan

### Week 1 — Foundations (modules 01–06)

- Day 1–2: modules 01–03. Setup checklist. Three tickets rewritten.
- Day 3–4: modules 04–05. Interview-build two context docs. Brain v1 with router. Commit.
- Day 5: module 06. `context/systems.md`. One cloud task from the phone.
- Day 6–7: Greg's day 1–3.

**Measured:** brain has ≥ 5 context docs; CLAUDE.md under 60 lines; three tickets done through plan mode.

### Week 2 — Skills and tools (modules 07–09)

- Day 8–9: module 07. Two skills built by doing. Evals with one goal each.
- Day 10: module 08. Tool map. Two new connectors. One tool instruction file.
- Day 11: module 09. One report in three shapes. `review.md` for it.
- Day 12–14: Greg's day 4–7. Morning brief live.

**Measured:** two skills pass their evals ≥ 80 %; morning brief has run three mornings; you read it on your phone.

### Week 3 — Agents and loops (modules 10–13)

- Day 15–16: module 10. Same ticket in Cowork, Claude Code, Codex. Comparison note.
- Day 17: module 11. Four needs for one task. One parallel sub-agent job on real data. Reviewer agent.
- Day 18–19: module 12. Weekly review and watchdog routines. Write-back to `daily/`.
- Day 20–21: module 13. Dispatch. 25-minute cadence for a week. Paper card.

**Measured:** three routines running; one bulk job of ≥ 50 records; ≥ 30 % of your agent interactions from the phone.

### Week 4 — Control and team (modules 14–16)

- Day 22: module 14. Three tiers in CLAUDE.md. Two hooks. Keys moved.
- Day 23–28: module 15. The seven-day team build. Plugin v1.
- Day 29: module 16. Score the catalogue. Top five on roadmap.md.
- Day 30: capstone review below. Capture the lesson.

**Measured:** plugin with ≥ 2 skills, 1 command, 1 agent file; one production hook tested; one week of `daily/` logs.

## 3. Capstone: one end-to-end system

Pick one process that today costs you two or more hours a week. Build the whole chain.

**Requirements:**

1. A trigger or schedule starts it without you.
2. It reads from the brain and from at least one connected tool.
3. At least one step uses sub-agents in parallel.
4. At least one human-in-the-loop checkpoint with options, answerable from your phone.
5. A QA step against `review.md` before anything leaves.
6. Output is a deliverable in a named folder or a published artifact, and a Slack or email notification.
7. It writes to `daily/`.
8. Every rule you added during the build is in a skill's rules section or in CLAUDE.md.
9. You can name the permission tier of every action it takes.
10. It has run three times. You have the eval report.

**For Tsara Tilapia, a candidate:** the weekly staff briefing chain. Monday 06:00: watchdog summary → `weekly-briefing` skill drafts in French → reviewer checks against the best example → Kim approves on the phone → published as a Markdown file in `docs/briefings/` and posted to the farm channel → `daily/` updated. Month 2: a grader compares each briefing to the best and proposes rule updates.

## 4. Self-assessment: are you a pro?

Answer honestly. Yes/no.

**Manage agents**
- [ ] I write tickets with job, scope, result and boundary.
- [ ] I use plan mode before meaningful work.
- [ ] I read diffs and look for the surprising change.
- [ ] I ask for variations at decision points.
- [ ] I turn corrections into rules.

**Agents read and write to the business**
- [ ] My brain is folders of Markdown with a CLAUDE.md router.
- [ ] My skills point to the brain instead of copying it.
- [ ] My tools follow the five-level hierarchy; browser and computer use are last resorts.
- [ ] Every deliverable lands in a named place and I confirm it exists.
- [ ] Agents write to `daily/`.

**The business gets smarter over time**
- [ ] Three routines run without me.
- [ ] Approved outputs are saved as examples.
- [ ] Skills have evals with one goal per run.
- [ ] A grader or review loop proposes improvements.
- [ ] Lessons are captured in LEARN.

**Control**
- [ ] Three permission tiers written down.
- [ ] Keys in a password manager, never in files or chats.
- [ ] Hooks block the human-owned commands.
- [ ] Fetched content is treated as data.
- [ ] I own every deploy.

**Team**
- [ ] I run parallel sessions with small packets.
- [ ] I use an orchestrator with cheaper children for bulk.
- [ ] I have at least one plugin.
- [ ] I check pinned threads every 25 minutes, not constantly.
- [ ] I do a meaningful share of this from my phone.

Twenty or more yes: you are operating as a pro. Below fifteen: go back to the module with the most no's.

## 5. What changes every three to six months

Ryan: "This is going to change every three to six months." What will change: interfaces, model names, plan limits, which features are desktop-only, what is beta. What will not change: the loop, the four needs, the brain in Markdown, tickets, plan then do, review layers, permission tiers, small packets, the decision cadence. When a product changes, re-read the principle and re-map the button.

Re-run this course's exercises with a new model. A/B test each skill against no skill. Delete what the model now does alone.

## 6. Closing

Theo's last line: "It feels like you have to be a technical guru to get started. Really, to become an AI-native org, think through the lens of managing agents and what those agents need to succeed, and you will be ahead of most companies in the world. Just get started. Scrape your knee and get stuff done."

Ryan's: "The best way to learn is to do."

Claude Academy's: "The most important thing you can do now is just get started."

Capture the lesson.
