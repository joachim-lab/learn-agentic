# Module 12 — Loops and scheduled work

**Time:** 60 minutes
**Goal:** You can set up recurring agent work that runs without you, build the loops that make the business smarter every day, and know which loop to build first.

## 1. Why it matters

Greg: "This is when a lot of people start having that aha moment where it's an actual 24-7 employee." Until now every module needed you at the keyboard. Loops are where the agent works while you sleep, and where signal flows back into the brain.

## 2. The concepts

### 2.1 Three kinds of loop

| Loop | What repeats | Example |
|------|--------------|---------|
| **Scheduled task / routine** | The same prompt at a fixed time | Morning brief at 07:00 |
| **Trigger-driven** | A prompt when an event happens | A proposal request in an email fires the proposal chain |
| **Self-improvement loop** | Grade → fix → ship, daily | Grade yesterday's chatbot conversations; open a fix for anything under the bar |

### 2.2 Scheduled tasks in Cowork

Sidebar → **Scheduled** → New task → name, description, prompt, frequency (monthly, weekly, daily, hourly, down to minutes), model, folder to grant. It sends the prompt to a fresh session on schedule.

Three ways to create one:

1. the Scheduled UI;
2. in chat: `/schedule` then "every day at 06:00, run my email-categorisation skill";
3. inside a skill prompt: "you will run this on the first of each month at 09:00" — it saves itself to Scheduled.

Runs show progress. A blue dot means it needs input from you. Cloud scheduled tasks run even when your laptop is off. (Ben's recording said "only when the desktop is open". That was true for local tasks then. Cloud tasks changed it.)

No instant webhooks yet: poll instead. "Every hour, check for new payments; send a thank-you email for each."

### 2.3 Routines in Claude Code

Three flavours:

- **Desktop local tasks** — run on your machine. Need the app open. Minimum interval one minute. Skipped if the computer sleeps.
- **Cloud routines** — run on Anthropic's servers on a fresh clone of the repo. Minimum interval one hour. Can also fire on API calls or GitHub events (a pull request opened).
- **`/loop`** — polling inside an open session.

Create one: Code tab → Routines → New routine, or just say "set up a daily code review that runs every morning at 09:00". Each task has its own permission mode. Run it once with **Run now** and choose "always allow" for the permissions it needs, or it will stall waiting for you.

### 2.4 Which loop first

Greg: do not start by asking the agent to ship production code at night. Start with a **recurring operator task**: useful, controlled, touches nothing important.

**The morning brief** — his sample routine, every weekday 07:00:

> Read `/customers` and `/context`, and open GitHub issues if connected. Create or update `/context/morning-brief.md` with: the top customer pain point from the latest notes, one product risk, one recommended build task for today, and one question I should ask customers today. Do not edit production code. Do not open a pull request. Under 500 words.

**The weekly ops review** — every Friday 15:00:

> Review open issues and recent customer notes. Group related issues. Identify duplicates. Suggest the single highest-leverage fix for next week. Write the summary to `/context/weekly-ops.md`. Do not edit code.

**The PR reviewer** — on every pull request:

> Review it using review.md. Comment only on issues that could cause bugs, broken flows, security problems or confusing behaviour. Post a short summary: what looks good, what needs attention, whether it is ready for human review.

After those three: every morning the agent tells you what matters; every week it shows the patterns; every change gets checked against your standard. That is "the night shift".

### 2.5 Ryan's production watchdog

Every day at 09:00: read all events for paying customers from the database, summarise into a JSON, render in the admin. Each line links to the real screen the customer saw. Ryan: "You think you know what's going on, but you don't." The links matter: humans are very good at spotting "that's weird" when they can look.

### 2.6 Ryan's self-improvement loop

Untangle has an agent, Grace, that talks to lawyers and clients. Every day:

1. an automation reads yesterday's conversations;
2. grades each on a rubric Ryan wrote with the agent ("here is how you judge whether this is good or bad");
3. anything below the score spawns a child session that fixes it and opens a pull request;
4. Ryan reviews and ships. About three fixes a day. Many are paper cuts he would never have found or bothered with.

Cost: cheap tuned model for the loop, about five dollars a session. His line: "If you're not willing to pay 15 dollars a day to improve one of the core feature sets of your product, what are you doing?"

### 2.7 Ben's scheduled skills

- **Failed-payment follow-up**, daily: find yesterday's failed Stripe payments → read prior email threads → classify the failure → draft a type-specific email → save as Gmail draft → report. "Already making an impact on my revenue."
- **Meeting digest**, daily: read yesterday's meeting transcripts → create tasks → update processes → write overview and next-day agenda into Notion.
- **Monthly accounting**, first of the month: Gmail, Stripe, web and browser to update the spreadsheet. Pings when it needs input.
- **Newsletter ideation**, daily 08:00: scan five sources, qualify against ICP, write an HTML dashboard, keep a CSV of what was already seen.
- **Call prep**, daily 07:00 for every meeting: CRM, emails, transcripts, web → HTML brief.
- **Pipeline review**: hot and at-risk leads, DM'd to Slack.

### 2.8 Theo's capture routine

Every hour or two: pull from Slack, meeting recordings, email, task boards into a brain inbox. Then a curation step files, cleans and detects triggers. Then the proposal chain fires on its own. Theo: "It's magic when I don't even know what proposal was asked for... I get the Slack ping and go, oh, proposal is ready."

### 2.9 Triggers without webhooks

Until instant triggers exist for your tool, the pattern is: a frequent poll ("every 15 minutes check the inbox for X") that fires a skill chain when it finds a match, and records what it has handled in a CSV so it does not repeat.

### 2.10 Notifications

Add to any scheduled skill: "If there is a high-priority item, send me a notification through Slack." Ryan: Slack in the top-left corner of his screen is where agents report. Theo's proposal chain ends with a Slack ping. Put notifications in a channel you read on your phone.

### 2.11 Write-back and the daily log

Every loop should write to `daily/YYYY-MM-DD.md`: what it did, what it found, what it changed. That log is how the next session, and you, know what happened. It is also the raw material for lessons. This is the "business gets smarter over time" line made real.

### 2.12 Costs and limits

Loops cost usage every run. Start with three. Use the cheapest model that passes the eval. Set a run budget. Watch the usage page weekly. Cloud routines cannot see local files; they work on a fresh clone. Local tasks need the app open.

## 3. How to do it in Claude — first three loops

1. **Morning brief** (Cowork, cloud, daily 07:00). Adapt Greg's prompt to your brain: read `daily/` from the last two days, `tasks/`, and the dashboard export. Write `daily/YYYY-MM-DD-brief.md`. Under 400 words. Read-only. Notify in Slack or email.
2. **Weekly review** (Friday 15:00). Read the week's `daily/` files. Group issues. One highest-leverage action for next week. Write `intelligence/weekly/YYYY-WW.md`.
3. **A watchdog for your most important system** (daily). For Tsara: read the ENGINE warnings tab, summarise by pond, link each to the sheet row. Flag any threshold crossed twice in a row.

Run each once with **Run now**. Grant the permissions. Check the output the next morning from your phone.

## 4. Worked example — Tsara Tilapia morning brief

> Every day at 06:30 Réunion time. Use the `briefing-hebdo-tsara` skill's data sources. Read the dashboard, the warnings, and yesterday's `daily/` log. Write `daily/YYYY-MM-DD-brief.md` in French: pond status in one table, every open warning with pond, metric, threshold and proposed action, and the three actions for today. Under 400 words. Do not change any sheet. If a warning is critical, send it to the farm Slack channel.

Cost: one cheap-model session a day. Value: Kim and the team start every day with the same picture, and the log accumulates.

## 5. Exercise (60 minutes)

1. Set up the morning brief. Run it now. Read the output.
2. Set up the weekly review for Friday.
3. Add the write-back rule to both: append a line to `daily/YYYY-MM-DD.md`.
4. After three days, read the three briefs in a row. Note one thing you would not have noticed without them. Write it in `questions-log.md`.

## 6. Check yourself

1. **Which loop should you build first?** A recurring operator task that touches nothing important: the morning brief.
2. **What does a self-improvement loop do?** Grades yesterday's output on a rubric, spawns a fix for anything below the bar, leaves the ship decision to you.
3. **How do you handle a tool with no instant trigger?** Poll on a schedule, act on matches, record what was handled.
