---
name: hot-handoffs-grounded-in-git
description: Multi-model AI handoff protocol across frontier models (Claude, Gemini, Codex, ChatGPT) where every claim must be grounded in an exact git commit hash, diff, or test output. Eliminates conversational hallucinations, unverified "done" claims, and context loss between AI shifts.
license: MIT
metadata:
  author: We Build for Good
  version: "1.0.0"
---

# Hot Handoffs Grounded in Git: Multi-Model Engineering Protocol

When multiple AI models (Claude Code, Antigravity/Gemini, Cursor, OpenAI Codex) share a codebase across shifts, the primary point of failure is **the handoff**.

Standard AI agents hand off work using conversational summaries (e.g. "I fixed the authentication bug and updated tests"). The incoming agent reads this, assumes it is true, and builds on top of imaginary progress: only to discover hours later that the code was never committed, the tests were failing, or the branch had drifted.

This protocol establishes a strict rule: **Conversational claims are invalid. Git is the single source of truth.**

---

## The Prime Directive

**If a claim is not verifiable in git or system exit codes, it did not happen.**

An outgoing agent cannot declare a task "done" through text alone. It must cite:
1. The exact git commit hash.
2. The working branch.
3. The exact test command executed and its exit code.

---

## The Four Handoff Anchors

Every handoff document (e.g. `HANDOVER.md` or continuation queue entry) must contain four verified anchors:

### 1. Branch & Head Commit
* Exact branch name: e.g. `fix/auth-token-refresh`
* Head commit hash: e.g. `c4b12a8`
* Commit message: e.g. `fix(auth): handle expired refresh token gracefully`

### 2. Working Tree State
* State must be explicitly verified via `git status --short`.
* If changes are in flight, state whether they are uncommitted or stashed.
* A clean working tree is always preferred before handoff.

### 3. Verification Evidence
* The exact terminal command executed: e.g. `pnpm test:auth`
* The exact exit code: `exit 0`
* Relevant passing assertions count: e.g. `14 passed, 0 failed`
* If a test is failing, paste the exact failure trace rather than summarizing it.

### 4. The Next Atomic Step
* Not a vague ambition ("improve performance").
* A concrete, bounded next action: e.g. "Wire the refresh token handler into `src/client.ts` line 42, then run `pnpm test:e2e`."

---

## The Incoming Agent Protocol (30-Second Orientation)

When an incoming AI agent takes over a session:

1. **Do not trust the previous agent's prose.**
2. Run `git status` and `git log -n 3` immediately to verify the ground truth.
3. Verify that the head commit matches the handoff document.
4. Run the cited verification command yourself to confirm tests are truly green.
5. If the tests pass and the branch matches, begin the next atomic step immediately without asking the human founder for redundant orientation.

---

## Canonical Handoff Schema

```markdown
# Session Handoff

## 1. Ground Truth
- Branch: `feature/export-pdf`
- Head Commit: `9f30b12`
- Working Tree: Clean (0 uncommitted files)

## 2. Verified Work Completed
- Built PDF layout renderer in `src/export/pdf.ts` (Commit `9f30b12`)
- Added unit tests in `tests/export.test.ts` (Commit `9f30b12`)
- Ran: `pnpm test tests/export.test.ts` (Exit code: 0, 8 passed)

## 3. Current Blockers or Surprises
- None. PDF generation completes in 140ms on local test fixture.

## 4. Next Atomic Step
- Connect `ExportButton.tsx` to call `generatePdf()` and test download trigger in browser.
```
