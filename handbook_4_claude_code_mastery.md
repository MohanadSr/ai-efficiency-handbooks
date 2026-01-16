# Efficiency Handbook 4: Claude Code Mastery Guide

*A comprehensive guide to high-performance agentic coding with Claude Code and Cursor. This manual synthesizes advanced patterns, philosophy, and professional setups from the tool's creators and power users.*

---

## 🧠 Core Philosophy: Context Engineering
**Mindset**: Any issue in LLM-generated code is a result of your context management, not the model's intelligence.

### The Context Quality Curve
Quality degrades non-linearly. The last 20% of your context window is "poison" (Lost in the Middle syndrome).
- **0-40%**: Excellent attention/recall.
- **60-80%**: "Lost in the Middle" starts. Mistakes increase.
- **>80%**: Critical failures; forgotten instructions.

---

## 🛠️ Essential Mastery Patterns

### 1. Error Logging System (Pattern 1)
Agentic coding hides the decision-making loop. Reconstruct it using a `~/.claude/error-log.md`:
- **Format**: [Date] [Prompt] [Context %] [Failure Mode] [Root Cause] [Fix Applied].
- **Categories**: Wrong Output, Hallucination, Refusal, Infinite Loop, Context Rot.
- **Key Lesson**: Always re-state critical patterns if >50% context is used.

### 2. Slash Commands as Local Apps (Pattern 2)
Think of slash commands as "workflows-as-a-service."
- **Smart Commit**: Analyzes diffs and generates semantic commit messages.
- **PR Creator**: Uses `gh` to draft comprehensive PRs with summaries and test plans.
- **Deep Investigation**: Phase-based (Understand → Locate → Analyze → Report) troubleshooting.
- **Refactor Planner**: Generates a strictly *mental* plan before executing changes.

### 3. Hierarchical Memory Architecture
- **`CLAUDE.md` (The "Bible")**: Low-overhead, repo-level config. Includes build/test commands and code style.
- **`ARCHITECTURE.md` (The Brain)**: 1-page max source of truth for patterns and tech decisions.
- **`PROJECT_INTELLIGENCE.md`**: Tracks debt, decisions, and patterns. Reference it every session.
- **`thoughts/` Directory**: A persistent bucket for the AI to "think out loud" (symlink across repos to share knowledge).

### 4. Deterministic Safety (Hooks)
Use safety hooks to enable "Safe YOLO Mode" (`--dangerously-skip-permissions` + Guardrails).
- **Bash Safety**: Intercepts `rm -rf /`, force pushes, or database drops.
- **Write Safety**: Protects `.env`, `.pem`, and system paths from accidental modification.
- **Post-Tool Formatters**: Automatically runs `prettier` or `black` after every write tool use.

---

## 🏗️ The "Boris Rules" (Founder's Setup)
The exact discipline used by the creators of Claude Code:

1.  **Think step-by-step**: Show full reasoning BEFORE any code.
2.  **No Placeholders**: NEVER output "rest unchanged" or ellipses. Always full files.
3.  **Completeness**: Output COMPLETE files.
4.  **Root Causes**: Fix the underlying issue, never patch symptoms.
5.  **Consistency**: Respect existing style/naming 100%.
6.  **Ask First**: If ambiguous, ASK. Do not guess.
7.  **Robustness**: Add error handling and edge cases by default.
8.  **Self-Correction**: Double-check for bugs/security before outputting.

---

## 🔄 The Iteration Loop (Beast Mode)
**Plan** → **Refine** → **Execute** → **Roast** → **Commit/Revert**.

- **The Roast**: prompt: *"Roast this code. Critique for bugs, security, and performance like a lead engineer."*
- **Hygiene**: Start a new chat every 8-12 turns. Context reset is the only cure for hallucination spirals.
- **Surgical Execution**: Implement one atomic logical unit or file per prompt.

---

## ⚡ Speed Hacks for Startups
- **No PRDs**: Use "@startup-context.md + Build X. Prioritize MVP Speed."
- **Magic Phrase**: "Keep it simple & cheap. No unnecessary abstractions."
- **Boring Stack**: Use Next.js, Tailwind, and Supabase. Claude knows these perfectly; zero hallucination risk.

---

## 🧐 User Error Checklist (Reality Check)
If Claude Code isn't working for you, check these 5 habits:
1.  **Missing Memory**: You aren't using a `roadmap.md` or `intelligence.md`.
2.  **Context Dumping**: You are pasting massive logs or entire codebases instead of targeted `@file` refs.
3.  **Rule Overload**: Your rules are >10 lines. Claude is ignoring them. (Use 3-5 line Global Guardrails).
4.  **Blind Acceptance**: You aren't running the "Roast Loop."
5.  **Context Rot**: You are in turn #50 and wondering why it's confused.

> 💡 **Pro Tip**: Use the **Double-Escape Rewind** (`Esc` x2) to restore both code AND conversation state to any previous milestone.
