# Module 01 — Fundamentals of AI

**Time:** 45 minutes
**Goal:** You can explain what a language model is, what it does well, what it does badly, and why context decides the result.

## 1. Why it matters

You will manage agents. A manager who does not know what a worker can do makes bad assignments. This module gives you the mental model. It is short. It is enough for business use.

## 2. The concepts

### 2.1 A model predicts the next word

A large language model (LLM) is a program trained on a very large amount of text. It learned one thing: given some text, predict what comes next. It does this one token at a time. A token is a piece of a word. About 750 words make 1,000 tokens.

That sounds simple. It is not. To predict the next word well, the model had to learn grammar, facts, reasoning patterns, code, and style. The result is a system that can write, summarise, translate, plan and reason.

Claude, GPT and Gemini are all LLMs. They differ in training, size and tuning. The mechanism is the same.

### 2.2 What the model does not have

The model has no memory between conversations unless a memory system adds it. It has no live access to the internet unless a tool gives it. It has no idea what happened after its training cut-off unless you tell it. It does not know your business unless you show it.

This is the most important point in the course. **The model only knows what is in front of it.** What is in front of it is called the *context*. Module 04 is about that.

### 2.3 Hallucination

Sometimes the model produces text that sounds right and is wrong. This is called hallucination. The model is not lying. It is predicting a plausible next word with no fact to anchor it.

Theo Tabba's picture is useful: think of an eager new hire who wants to impress you. He will "fake it until he makes it" rather than say "I do not know". Your job as manager is to remove the need to fake it. You do that with context, tools and verification.

Three rules reduce hallucination:

1. Give the facts. Do not make the model guess numbers, names or dates.
2. Give tools. A model with a web search or a database does not need to invent.
3. Ask for verification. "Base every claim on the transcript. Mark anything you cannot find in it."

### 2.4 The context window

The model reads a fixed amount of text at once. That is the context window. Claude's is 200,000 tokens or more. That is about 500 pages. Everything must fit: your instructions, the files, the conversation so far, and the answer.

When the window is nearly full, quality drops. Old parts get compressed or dropped. This is why long chats get worse. It is also why agents use sub-agents: each one gets a fresh window. Module 11 covers that.

### 2.5 Models are not all the same

At any time a vendor sells several models. A large one reasons best and costs most. A small one is fast and cheap. In September 2026 Claude has Opus (strongest), Sonnet (everyday work) and Haiku (fast and cheap). Anthropic also ships the Fable line for the highest-stakes reasoning. Names change. The rule does not: **use the strongest model to plan and review. Use a cheaper model to execute in bulk.** Ryan Carson calls this model routing. It is how he cut a 20,000-dollar month down to a viable budget.

### 2.6 From chat to agent

A chat is a turn-by-turn exchange. You type. The model answers. You type again.

An agent is different. Barry Zhang at Anthropic gives the definition the whole course uses: **an agent is a model using tools in a loop.** The model reads a goal, picks a tool, sees the result, decides the next step, and repeats until done. You can walk away. Claude Cowork and Claude Code are agents. Module 11 goes deep.

### 2.7 The four D's of AI fluency

Claude Academy teaches the 4Ds. They describe your job.

| D | Question you ask |
|---|------------------|
| **Delegation** | What should I hand to AI, and what stays with me? |
| **Description** | How do I explain the task so it can succeed? |
| **Discernment** | Is the output good? How do I know? |
| **Diligence** | Am I using it responsibly? Who is accountable? |

> "Validation builds confidence, but it doesn't eliminate responsibility." — Claude Academy, Claude 101

## 3. How this shows up in Claude

- **Context window:** Claude tells you when a chat gets long. Start a new chat. Put durable facts in a project or a file, not in the chat.
- **Hallucination:** Claude cites sources when it searches. Ask for citations. Ask "what did you assume?"
- **Model choice:** The model picker is at the bottom of the chat box. Pick the strong model for planning. Pick Sonnet for routine drafting.
- **Memory:** Claude keeps a memory of you across chats. It is a curated set of topics, not a transcript. You can see it, edit it and turn it off in Settings.

## 4. Worked example — Tsara Tilapia

**Problem:** You ask Claude "How much feed did we use in August?" in a fresh chat. Claude invents a plausible number.

**Why:** The model has no access to your feed sheet. It has no context. It predicts a plausible answer because that is what it does.

**Fix:** Give access. Connect Google Drive. Or export the sheet to CSV and attach it. Then ask: "Read the attached August feed log. Sum the kg column. Show the formula you used." Now the model has a fact and a tool. The number is right, and you can check it.

**Lesson:** The quality of the answer is set by what you put in front of the model, not by how clever the model is.

## 5. Exercise (30 minutes)

1. Open a new Claude chat. Ask a question about your business that Claude cannot know. Note the answer.
2. Attach the file that holds the real answer. Ask again. Compare.
3. Ask Claude: "List the assumptions you made in your first answer." Read them.
4. Write three lines in `learn/questions-log.md`: one thing the model did well, one thing it faked, one thing you will always provide next time.

## 6. Check yourself

1. **What is the only thing a model can use to answer?** The context in front of it: instructions, files, tools' results, the chat so far.
2. **Why do long chats get worse?** The context window fills. Old content gets compressed or dropped.
3. **What is an agent, in seven words?** A model using tools in a loop.
