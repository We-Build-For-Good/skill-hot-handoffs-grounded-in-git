# Hot Handoffs Grounded in Git: Multi-Model Engineering Protocol

> **An open-source AI engineering protocol from [We Build for Good](https://webuildforgood.com)**  
> *Zero conversational drift. Ground every AI handoff in git truth.*

---

## Overview

`hot-handoffs-grounded-in-git` is an operational protocol for multi-model AI software development teams (Claude Code, Cursor, Antigravity/Gemini, OpenAI Codex).

It eliminates the most expensive failure mode in multi-agent workflows: **conversational context loss and hallucinated progress between shifts**.

---

## Why This Exists

When an AI agent finishes a prompt or reaches token exhaustion, it typically summarizes its work in conversational prose:
> *"I completed the user profile refactor, fixed all linter errors, and updated the documentation."*

When the next agent takes over, it reads this prose and assumes it is factual. But frequently:
* Changes were left uncommitted in a temporary worktree.
* Tests failed on an unhandled edge case.
* The branch was out of date with origin.

`hot-handoffs-grounded-in-git` mandates that conversational claims are strictly invalid. Every handoff must be anchored in four verifiable facts: branch name, head commit hash, clean working tree, and raw test exit codes.

---

## Installation

### For Claude Code
```bash
git clone https://github.com/We-Build-For-Good/skill-hot-handoffs-grounded-in-git.git ~/.claude/skills/hot-handoffs-grounded-in-git
```

### For Cursor
```bash
mkdir -p .cursor/skills
git clone https://github.com/We-Build-For-Good/skill-hot-handoffs-grounded-in-git.git .cursor/skills/hot-handoffs-grounded-in-git
```

### For Antigravity / Open Agent Skills
```bash
mkdir -p .agents/skills
git clone https://github.com/We-Build-For-Good/skill-hot-handoffs-grounded-in-git.git .agents/skills/hot-handoffs-grounded-in-git
```

---

## How to Use It

1. When an agent is wrapping up a session or handing off work:
   * *"Write a clean session handoff following hot-handoffs-grounded-in-git."*
2. When an incoming agent starts a session:
   * *"Orient yourself using the latest handoff and verify the ground truth in git."*

The incoming agent will independently check `git status`, verify the commit hash, run the test command, and start the next atomic task in under 30 seconds without asking redundant questions.

---

## License

MIT License. Developed and maintained by [We Build for Good](https://webuildforgood.com).
