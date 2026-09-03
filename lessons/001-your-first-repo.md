# Lesson 001 — Your first repo

**Date:** 2026-09-03
**From session:** Building the learn-agentic tool itself

## What you did

You created this repo and pushed it to GitHub with four commands.

## The principle

A git repo is a folder with a history. Git records snapshots, called
commits. Each commit has a message that says why the change exists.
GitHub is a copy of that history on a server. `push` sends your local
history to the server. Nothing is shared until you push.

## The commands, explained

- `git init` — makes this folder a repo. It adds a hidden `.git` folder
  that holds all history. Delete `.git` and the history is gone; the
  files stay.
- `git add -A` — stages every changed file. Staging means: put it in
  the next snapshot. Nothing is recorded yet.
- `git commit -m "message"` — records the snapshot with your message.
  This is local only.
- `git push` — sends commits to GitHub.

## Why the message matters

The diff shows what changed. Only the message can say why. A repo with
good messages is a logbook. A repo with "update" messages is noise.

## Check yourself

1. After `git commit`, is your change on GitHub? (No. Only after push.)
2. What is in the `.git` folder? (The full history of every commit.)
3. If you delete a file and commit, is it gone forever? (No. Earlier
   commits still hold it.)
