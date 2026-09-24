# Module 02 — The Claude interface

**Time:** 60 minutes
**Goal:** You know every surface where Claude runs. You can pick the right one for a task in five seconds.

## 1. Why it matters

Claude is not one app. It is one model behind many doors. Each door fits a shape of work. Pick the wrong door and you fight the tool. Pick the right door and the work flows.

## 2. The concepts

### 2.1 Three shapes of work

Claude Academy says it in one line:

> "Chat is for thinking with Claude. Cowork is for delegating to Claude. Code is for building software with Claude."

| Shape | What you do | What Claude does | Where |
|-------|-------------|------------------|-------|
| **Chat** | Talk turn by turn | Answers, drafts, thinks with you | Web, desktop, mobile |
| **Cowork** | Describe an outcome and step away | Plans, does multi-step work, returns a result | Desktop, web, mobile, Chrome side panel |
| **Code** | Point at a folder and give a ticket | Reads, edits, runs commands, uses git | Desktop tab, terminal, web, VS Code |

Ben's course calls Cowork "the Claude Code for non-technical knowledge workers". Under the hood Cowork is an agent. It can act on files and tools. Claude Code is the same agent with more features for engineering. Learn Cowork well and Claude Code feels familiar.

### 2.2 The desktop app

The desktop app (macOS, Windows) has three tabs: Chat, Cowork, Code. It adds things the browser cannot do:

- **Folder access.** Grant one folder. Claude reads and writes files there.
- **Screenshots and dictation.** Quick capture. Voice input.
- **Computer use.** Claude sees your screen and clicks. Slow and token-heavy. Last resort.
- **Local scheduled tasks.** Run when the app is open.
- **Quick entry.** Option key on Mac opens a small prompt window.

### 2.3 Projects

A project is a workspace with its own chats, its own knowledge files, its own instructions and its own memory. One project per type of work. Every chat in the project starts with that context.

In Cowork a project can also be bound to a folder on your computer. Then you do not reselect the folder every chat.

Kim's setup already follows this pattern: **tsara-erp**, **learn**, **screen-companion**. Each has a folder, a Drive mirror and a CLAUDE.md. Module 05 explains why that is the right shape.

### 2.4 Project instructions and global preferences

There are three layers of standing instruction:

1. **Global preferences** (Settings). Apply to every chat. Kim's preferences say: Simplified Technical English, Markdown for reading documents, French when asked in French, where files live.
2. **Project instructions**. Apply to every chat in one project. Example from Ben: "You're my YouTube assistant... you have access to my YouTube folder... save every asset into the folder."
3. **CLAUDE.md** in a folder. Read by Cowork and Claude Code when they work in that folder. This is the file that tells the agent how the folder is organised and how to behave inside it.

Rule from Kim's own preferences: CLAUDE.md wins over global preferences, except on where files live and what Claude can see. Write the rule down once. Then every session obeys it.

### 2.5 Memory

Claude remembers facts about you across chats. It saves topics as you go, not a summary after the chat ends. Project memory is separate per project. You can:

- say "remember this" or "forget this";
- view and edit the memory summary in Settings;
- open an incognito chat (ghost icon) that saves nothing;
- pause or reset memory.

Memory carries into Cowork tasks in the cloud. It does not replace your context files. Memory is a handful of essential facts. Your context layer is thousands of files. Module 04.

### 2.6 Artifacts

An artifact is anything Claude makes that you would put in front of someone: a document, a deck, a dashboard, a small tool. It opens in a side panel. On paid plans it lives in the Artifacts tab and survives the chat. Module 09.

### 2.7 Skills, connectors, plugins

Three words you will hear in every module.

- **Skill:** a folder of instructions Claude loads when a task matches. Teaches Claude *how you do* a task. Module 07.
- **Connector:** a link to another tool (Gmail, Drive, Slack, Notion, GitHub). Gives Claude *access*. Module 08.
- **Plugin:** a bundle of skills, commands, agents and connectors for one role or department. Module 15.

### 2.8 Mobile

The mobile app does chat, Cowork in the cloud, and **dispatch**: send a task from your phone to Cowork on your desktop. Module 13 covers how to run half your work from a phone.

### 2.9 Claude in Chrome

A browser extension. Claude reads pages, clicks, fills forms. It also serves as the browser for Cowork and Claude Code. Available on all paid plans. Some site categories are blocked for safety. Module 08.

### 2.10 Plans

Cowork, custom skills, custom connectors and Claude Code need a paid plan (Pro, Max, Team, Enterprise). Sub-agent work and long Cowork tasks use a lot of usage. Ben's advice: if you run parallel sub-agents daily, be on Max. Check current limits at support.claude.com. They change.

## 3. How to do it in Claude — first setup checklist

Do this once. Thirty minutes.

1. Install the desktop app from claude.com/download. Sign in.
2. Settings → Capabilities → turn on **Code execution and file creation**. This enables skills and artifacts.
3. Settings → write your **global preferences**. Language, format, where files go. Keep it under 40 lines.
4. Sidebar → Projects → create one project per domain. Bind each to a folder on your computer.
5. Settings → Connectors → connect Gmail, Google Drive, Calendar. Set "always allow" only for read actions you trust.
6. Install the mobile app. Same account. Allow dispatch.
7. Install Claude in Chrome. Pin it.
8. Turn on memory. Read what it holds after a week.

## 4. Worked example — picking the door

Three tasks land on your desk on a Monday.

| Task | Door | Why |
|------|------|-----|
| "Is this supplier contract fair?" | **Chat** | You want to think, ask follow-ups, push back. |
| "Turn the last four weekly briefings into a monthly report for the investors, as a docx, in French." | **Cowork** | Clear outcome. Multi-step. You can walk away. |
| "Fix the feed-conversion formula in the ENGINE Apps Script and deploy to exec." | **Code** | It touches code and a repo. You want a diff and a plan first. |

If you are not sure, start in Chat. Think until the outcome is clear. Then hand it to Cowork or Code.

## 5. Exercise (45 minutes)

1. Run the setup checklist above.
2. Create a project called **AI course**. Bind it to `~/Claude/projects/learn`. Instructions: "You are my tutor for the AI-for-business course in docs/ai-business-course. Answer in Simplified Technical English. Save every exercise output into docs/exercises/."
3. In that project, run the same small task in Chat, then in Cowork: "Summarise module 01 in ten lines and save it as `docs/exercises/m01-summary.md`." Note what each door did differently.
4. Open the memory summary. Delete anything wrong.

## 6. Check yourself

1. **Which door for "describe an outcome and step away"?** Cowork.
2. **Where do standing instructions for one folder live?** In that folder's CLAUDE.md.
3. **Memory or context files: which holds thousands of documents?** Context files. Memory holds a small set of essential facts.
