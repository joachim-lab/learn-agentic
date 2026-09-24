# Module 13 — Working online and from your phone

**Time:** 45 minutes
**Goal:** You can run, steer and review agent work from your phone, away from your desk. You have a cadence that keeps you sane when ten agents are working.

## 1. Why it matters

Ryan Carson does about half his work from an iPhone. His agents run in the cloud. They are blocked only by his decisions. "Why wait until you're in front of your Mac to give feedback? It makes no sense. You've got to be available." "The office is your phone."

For a farm operator who is often on site, at a pond, or driving, this is not a nice-to-have. It is the difference between agents that wait and agents that work.

## 2. The concepts

### 2.1 "Offline" means away from the desk

You asked how to work offline using your phone. The precise answer: **you are away from your computer, not off the network.** Agents run in the cloud. Your phone is the remote control. A few things also work with no signal — reading briefs you downloaded, dictating a ticket to send later — but the agent itself needs the cloud.

### 2.2 What runs where

| Work | Where it runs | Phone role |
|------|---------------|-----------|
| Cloud Cowork session | Anthropic's servers | Start, answer questions, read result |
| Cloud routine / scheduled task | Anthropic's servers | Read the output, get the notification |
| Claude Code on the web | Anthropic's servers on a GitHub repo | Start, review, approve |
| Desktop Cowork session | Your Mac (must be on) | Dispatch a task to it; read result |
| Desktop-linked cloud session | Cloud, with a bridge to your Mac's folders | Steer; files reach your folders when the Mac is on |
| Codex cloud task / Devin session | Vendor's servers | Browser on phone |

Rule: **anything you want to touch from your phone must run in the cloud or on a machine that stays on.**

### 2.3 Dispatch

Install the Claude mobile app. Same account. Allow dispatch. Now you can trigger Cowork on your desktop from your phone: "Check today's emails. Anything important?" The desktop does the work, the summary comes back to your phone. Needs the desktop running. Most useful once you have skills and scheduled tasks to trigger.

### 2.4 The cloud-first setup

1. Keep the brain in a git repo pushed to GitHub. Cloud sessions clone it.
2. Prefer cloud Cowork and cloud routines for anything you may check from the phone.
3. Use Slack (or email) as the agents' reporting channel. Notifications reach the phone.
4. Publish dashboards as artifacts. Open them on the phone.
5. Keep the desktop on and plugged in when you rely on local tasks or dispatch.

### 2.5 The decision cadence

Ryan's most important lesson is not technical. With many agents, your job becomes **making high-stakes decisions all day**. Before, two or three a day. Now ten to twenty by lunch. It is tiring. It is a new muscle.

His system:

- **Two buckets.** Big important threads: pin them. Small fixes and fires: let them rip, come back later.
- **A 25-minute cadence.** Check the pinned threads every 25 minutes. Not constantly. Clicking through threads all day wipes you out. "Slow is smooth and smooth is fast."
- **An analog list.** A paper card with the three things that must ship today. Because ten fires will try to distract you.
- **Rest is part of the system.** The cadence exists so you can mentally rest between decision bursts.

### 2.6 Small packets of work

Greg's rule for parallel sessions applies double on a phone screen: each session should return a **small packet** you can inspect, accept, revise or reject in two minutes. Root cause, files changed, checks run, what to look at, what is uncertain. If a session returns a wall of text, the ticket was too big.

### 2.7 Answering questions on the go

Cowork stops and asks when a decision is yours. The question arrives with options (checkboxes, single select, free text). Answer from the phone. This is human-in-the-loop at the right grain: the agent did the work, you made the call.

### 2.8 Dictation

Both Ryan and Ben dictate most prompts. Wispr Flow, or the native mic. On a phone, dictation is faster than typing a brief. Speak the four parts of the ticket: job, scope, result, boundary.

### 2.9 What not to do from a phone

- Do not approve a deploy you have not read. Read the diff summary. If you cannot read it on the phone, it waits.
- Do not paste production keys into a mobile chat.
- Do not run a "Skip all permissions" session from the phone. You are not there to catch it.

### 2.10 Ryan's numbers

22 to 25 pull requests a day on average, sometimes 40. The day he climbed Mount Washington with his son and had no signal, he shipped eight before leaving, from his phone, while the boy slept. The agents worked all day. The decisions waited for him.

## 3. How to do it in Claude

- **Mobile app:** Cowork tab → new task → choose the project → dictate the ticket. It runs in the cloud.
- **Check a running task:** the task list shows steps. The blue dot means a question is waiting.
- **Dispatch to desktop:** in the mobile app, choose your desktop as the target. Requires the desktop app open and signed in.
- **Notifications:** turn on push for Claude and for Slack. Route agent reports to one Slack channel.
- **Artifacts:** open the Artifacts tab on mobile. Dashboards render there.
- **Scheduled tasks:** create them on desktop with a cloud target. Read outputs on mobile.

## 4. Worked example — a morning at the ponds

06:30 — The morning brief arrives in Slack. Kim reads it while walking to pond 3. One warning: oxygen dipped twice overnight in pond 5.

06:40 — Kim dictates a Cowork task from the phone: "Pull the last 48 hours of oxygen readings for pond 5 from the ENGINE sheet. Plot them. Compare with the aeration schedule. Tell me if the dips match the pump off-times. Read-only."

06:55 — The result arrives: a chart, and yes, the dips line up with the pump pause. Kim answers a Cowork question: "Draft a note to Charles about the pump timer? Yes / No." Yes.

07:10 — The draft is in Slack. Kim edits one line on the phone and sends it. Total desk time: zero.

## 5. Exercise (45 minutes)

1. Install the mobile app. Enable dispatch. Run one dispatched task to your desktop.
2. Start one cloud Cowork task from the phone with a dictated ticket. Answer at least one question it asks.
3. Set your phone: Claude and Slack notifications on. One Slack channel for agent reports.
4. For one week, try the 25-minute cadence and the paper card. Note in `questions-log.md` how many high-stakes decisions you made before lunch on day three.

## 6. Check yourself

1. **What must be true for a task to be steerable from your phone?** It runs in the cloud or on a machine that stays on.
2. **What is the 25-minute rule?** Check pinned high-stakes threads every 25 minutes, not constantly.
3. **What is dispatch?** Triggering Cowork on your desktop from your phone.
