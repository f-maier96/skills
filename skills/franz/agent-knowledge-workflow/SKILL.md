---
name: agent-knowledge-workflow
description: Use at the START or RESUMPTION of work on any of Franz's projects (Moncon, faratron, Zweites-Gehirn vault, side projects) — before reading code, changing files, or continuing a session. Bootstraps shared context so every agent (Claude Code, Codex, Hermes) works from the same current truth: pulls the knowledge repo, reads AGENTS.md and the latest handover, checks git status, then routes to the right skill for spec, tickets, build, review, debug, or handoff. Use when an agent needs to find the current state of a project, picks up an unfamiliar repo, or is told to "continue where we left off".
---

Thin router on repo level. This skill does **not** contain the working rules — it makes sure every agent loads them and then points to the right specialist skill.

**Single source of truth:** the working rules and the Start / Working / End routines live in `AGENTS.md`. Never restate or paraphrase them here. Read the file, follow it.

## Start (before touching anything)

1. Confirm the working directory and run `git status`.
2. `git fetch`, then `git pull --ff-only` **only if** no local changes would conflict — for both the knowledge repo and the project repo.
3. Read `AGENTS.md` (repo root, and the knowledge-repo master if this is a code project). It is the authority for rules and routines.
4. Read tool-specific rules if present: `CLAUDE.md`, `.cursorrules`, `.github/copilot-instructions.md`, project README/agent files.
5. Read the relevant project note and the **latest handover** before starting.
6. If a RAG/MCP knowledge tool is available, use it for context search — Git is truth, RAG is search.
7. For anything non-trivial, produce a short plan before changing files.

## Route to the right skill

Do not improvise a phase this repo already has a skill for. Match the work to the skill and invoke it:

| You are about to… | Invoke |
|---|---|
| Align on a fuzzy idea / sharpen domain terms | `/grill-with-docs` |
| Research a question with sources | `/research` |
| Turn the discussion into a spec | `/to-spec` |
| Break a plan/spec into tracer-bullet tickets | `/to-tickets` |
| Build a feature or fix | `/implement` (test-first via `/tdd`) |
| Review changes before merge | `/code-review` |
| Diagnose a bug or failure | `/diagnosing-bugs` |
| Hand off / end a session | `/handoff` |

## Non-negotiables (enforced by AGENTS.md — do not re-derive)

- Never work directly on `main`; one branch/worktree per task.
- Small, reviewable changes; no mixed commits.
- Never read, store, commit, or expose secrets.
- No production deploy, payment, trading, customer email, or social post without explicit go.
- At session end, update the project handover per the `AGENTS.md` End routine (or `/handoff`).

If `AGENTS.md` is missing, stop and ask Franz before proceeding — the shared rules must be loaded first.
