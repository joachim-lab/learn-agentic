# learn-agentic

A living learning repo. Each work session with Claude produces one lesson.
The repo itself is the practice ground for git and GitHub.

## How this works

1. You do real work with Claude (ERP patches, scripts, tools).
2. At the end of the session, you say: "capture the lesson".
3. Claude writes one numbered file into `lessons/`.
4. You commit and push it. The commit is part of the training.

## Curriculum map

Progress marks: [ ] not started · [~] in progress · [x] solid

### 1. Coding principles
- [ ] Functions, inputs, outputs, return values
- [ ] Data structures: arrays, objects, maps
- [ ] Control flow: loops, conditions, early exit
- [ ] Errors: throw, catch, fail loudly vs silently
- [ ] Why simple beats complex; one path, no fallbacks

### 2. Git and GitHub
- [~] init, add, commit, push (lesson 001)
- [ ] Reading a diff before you commit
- [ ] Branches and when one person needs them
- [ ] Pull requests, even solo
- [ ] .gitignore and what never goes in a repo

### 3. Infrastructure
- [ ] Where code runs: your machine, a sandbox, a server, a cloud
- [ ] Environments: dev vs prod, and why you only use exec
- [ ] Deploys: what clasp push actually does
- [ ] Secrets, scopes, and OAuth

### 4. Agents and agentic work
- [ ] What an agent loop is: model, tools, results, repeat
- [ ] Tools and MCP: how Claude touches the world
- [ ] Skills: packaged instructions, and when to make one
- [ ] Context windows, memory, and handovers
- [ ] Verification: why the agent must check its own work

### 5. AI for business with Claude (course)
- [ ] Full course in `docs/ai-business-course/` — 17 modules + glossary. Start at `00-README.md`.
- [ ] Modules 01–06 foundations · 07–09 skills, tools, outputs · 10–13 agents and loops · 14–17 control, team, capstone

## Files

- `lessons/` — one file per lesson, numbered, newest has highest number
- `glossary.md` — terms in plain language, added as they appear
- `docs/ai-business-course/` — the AI-for-business course, one Markdown file per module
- `questions-log.md` — your open questions; answered ones move into lessons
