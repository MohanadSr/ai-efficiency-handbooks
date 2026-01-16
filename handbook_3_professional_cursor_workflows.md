# Efficiency Handbook 3: Professional Cursor Workflows & Scaling Guide

*A master guide for developers building medium-large projects (50k+ LOC) and professional teams. This handbook moves beyond basic chat usage into structured "External Memory" and "Agent Orchestration" systems.*

---

## 🎯 The High-Leverage Prompting Levers
### 1. The "Similarity" Prompt (Consistency King)
Generic prompts yield generic results. Referencing existing code provides a concrete pattern for the AI to mimic.
- **❌ Don't say**: "Make a dropdown menu component."
- **✅ Do say**: "Make a dropdown menu component **similar to the Select component in `@components/Select.tsx`**."

### 2. Targeted Context Injection
- **Rule**: Never dump entire folders if only 2-3 files matter. 
- **Action**: Use `@file` symbols to point to "gold standard" examples. Claude performs 10x better when context is laser-targeted.

---

## 🏗️ The "External Memory" System
Do not rely on the chat window for project state; it is ephemeral. Offload memory to files that act as the project's "brain."

| File | Purpose | Usage |
| :--- | :--- | :--- |
| **`PROJECT_OVERVIEW.md`** | Core Architecture | Reference for directory tree, tech stack, and data flow. |
| **`MILESTONES.md`** | Roadmap & Checklist | High-level phases and trackable task status. |
| **`DOCUMENTATION.md`** | API & Schema Registry | Prevents hallucination of API contracts or DB relations. |
| **`CURSOR_MEMORY.md`** | Persistence | record project lessons and principles to avoid "Groundhog Day" mistakes. |

---

## 📋 The "TODO.md" Method (Agent Mode)
Turn messy Agent sessions into a trackable, rollback-friendly process:

1.  **Define & Plan**: Prompt: *"PLAN the work based on `@milestones.md` but do NOT implement it yet. Ask questions."*
2.  **Generate Roadmap**: Prompt: *"Create a `todolist.md` with check boxes listing every surgical change needed."*
3.  **Git Checkpoint**: **Commit the `todolist.md`** to Git. This creates a "Save Point."
4.  **Iterative Execution**: Prompt: *"Implement the tasks one by one, ticking them off in `@todolist.md` as you go."*
5.  **Git Commit**: Commit *every* single sub-task as it's completed.

---

## 🧠 The Hybrid Planning Protocol
**State Machine**: `Plan` → `Execute` → `Critique` → `Iterate`.

### 1. Planning (High-Energy/Human)
Plan complex features, data models, and core logic *manually* (or with minimal AI brainstorming). Ensure architecture is solid before the first line of code.

### 2. Execution (Low-Energy/AI Agent)
Switch to Agent Mode once the plan is set. The AI acts as a high-speed junior developer grinding through surgical implementation details.

### 3. The "Roast" Critique Loop
After the AI writes code, do NOT run it immediately. Prompt:  
> *"Roast this code. Critique it for bugs, security holes, and readability like a senior engineer."*  
*Insight: AI catches ~70% of its own bugs during self-review.*

---

## 📂 Scaling to 50k+ LOC
Professional disciplines for large codebases:

- **Reindex Often**: Run **Settings → Features → Resync Index** frequently after moving files or deleting folders to avoid stale index hallucinations.
- **Log Hygiene (`this.log`)**: Create a `this.log` file. Paste massive debug traces there. Reference it (`@this.log`) so the chat context doesn't get flooded by logs.
- **Incrementalism**: Never ask for "Phase 2." Ask for "Item 1 from Phase 2 in `@milestones.md`."
- **File Size Discipline**: Split components over 400 lines. Large files confuse AI attention.

---

## 🛠️ Reset Protocols (The Panic Buttons)
Keep these ready to realign a drifting AI:

- **`@Take a Breath`**: *"Stop. Read `@PROJECT_OVERVIEW.md` and `@todolist.md`. Summarize current status and immediate next step. Do not write code."*
- **`@Revert & Learn`**: If the AI makes a mess: 1) Stash changes. 2) Ask *"Why did that fail and what did we learn?"* 3) Re-apply with those lessons.

---

## 📊 Summary Checklist
- [ ] Brain files (`milestones.md`, `overview.md`) are initialized and referenced.
- [ ] Task list (`todolist.md`) is used for Agent Mode tracking.
- [ ] Git commits occur after every sub-task.
- [ ] Critique loop ("Roast") is part of the merge process.
- [ ] Global Rule: "Never use placeholders / Output complete logic."
# Cursor Development Rules & AI Collaboration Guide
 
## 📜 Core Philosophy
 
1.  **Simplicity:** Prioritize simple, clear, and maintainable solutions. Avoid unnecessary complexity or over-engineering.
2.  **Iterate:** Prefer iterating on existing, working code rather than building entirely new solutions from scratch, unless fundamentally necessary or explicitly requested.
3.  **Focus:** Concentrate efforts on the specific task assigned. Avoid unrelated changes or scope creep.
4.  **Quality:** Strive for a clean, organized, well-tested, and secure codebase.
5.  **Collaboration:** This document guides both human developers and the AI assistant for effective teamwork.
 
## 📚 Project Context & Understanding
 
1.  **Documentation First:**
    *   **Always** check for and thoroughly review relevant project documentation *before* starting any task. This includes:
        *   Product Requirements Documents (PRDs)
        *   `README.md` (Project overview, setup, patterns, technology stack)
        *   `docs/architecture.md` (System architecture, component relationships)
        *   `docs/technical.md` (Technical specifications, established patterns)
        *   `tasks/tasks.md` (Current development tasks, requirements)
    *   If documentation is missing, unclear, or conflicts with the request, **ask for clarification**.
2.  **Architecture Adherence:**
    *   Understand and respect module boundaries, data flow, system interfaces, and component dependencies outlined in `docs/architecture.md`.
    *   Validate that changes comply with the established architecture. Warn and propose compliant solutions if a violation is detected.
3.  **Pattern & Tech Stack Awareness:**
    *   Reference `README.md` and `docs/technical.md` to understand and utilize existing patterns and technologies.
    *   Exhaust options using existing implementations before proposing new patterns or libraries.
 
## ⚙️ Task Execution & Workflow
 
1.  **Task Definition:**
    *   Clearly understand the task requirements, acceptance criteria, and any dependencies from `tasks/tasks.md` and the PRD.
2.  **Systematic Change Protocol:** Before making significant changes:
    *   **Identify Impact:** Determine affected components, dependencies, and potential side effects.
    *   **Plan:** Outline the steps. Tackle one logical change or file at a time.
    *   **Verify Testing:** Confirm how the change will be tested. Add tests if necessary *before* implementing (see TDD).
3.  **Progress Tracking:**
    *   Keep `docs/status.md` updated with task progress (in-progress, completed, blocked), issues encountered, and completed items.
    *   Update `tasks/tasks.md` upon task completion or if requirements change during implementation.
 
## 🤖 AI Collaboration & Prompting
 
1.  **Clarity is Key:** Provide clear, specific, and unambiguous instructions to the AI. Define the desired outcome, constraints, and context.
2.  **Context Referencing:** If a task spans multiple interactions, explicitly remind the AI of relevant previous context, decisions, or code snippets.
3.  **Suggest vs. Apply:** Clearly state whether the AI should *suggest* a change for human review or *apply* a change directly (use only when high confidence and task is well-defined). Use prefixes like "Suggestion:" or "Applying fix:".
4.  **Question AI Output:** Human developers should critically review AI-generated code. Question assumptions, verify logic, and don't blindly trust confident-sounding but potentially incorrect suggestions (hallucinations).
5.  **Focus the AI:** Guide the AI to work on specific, focused parts of the task. Avoid overly broad requests that might lead to architectural or logical errors.
6.  **Leverage Strengths:** Use the AI for tasks it excels at (boilerplate generation, refactoring specific patterns, finding syntax errors, generating test cases) but maintain human oversight for complex logic, architecture, and security.
7.  **Incremental Interaction:** Break down complex tasks into smaller steps for the AI. Review and confirm each step before proceeding.
8.  **Standard Check-in (for AI on large tasks):** Before providing significant code suggestions:
    *   "Confirming understanding: I've reviewed [specific document/previous context]. The goal is [task goal], adhering to [key pattern/constraint]. Proceeding with [planned step]." (This replaces the more robotic "STOP AND VERIFY").
 
## ✨ Code Quality & Style
 
1.  **TypeScript Guidelines:** Use strict typing (avoid `any`). Document complex logic or public APIs with JSDoc.
2.  **Readability & Maintainability:** Write clean, well-organized code.
3.  **Small Files & Components:**
    *   Keep files under **300 lines**. Refactor proactively.
    *   Break down large React components into smaller, single-responsibility components.
4.  **Avoid Duplication (DRY):** Actively look for and reuse existing functionality. Refactor to eliminate duplication.
5.  **No Bazel:** Bazel is not permitted. Use project-specified build tools.
6.  **Linting/Formatting:** Ensure all code conforms to project's ESLint/Prettier rules.
7.  **Pattern Consistency:** Adhere to established project patterns. Don't introduce new ones without discussion/explicit instruction. If replacing an old pattern, ensure the old implementation is fully removed.
8.  **File Naming:** Use clear, descriptive names. Avoid "temp", "refactored", "improved", etc., in permanent file names.
9.  **No One-Time Scripts:** Do not commit one-time utility scripts into the main codebase.
 
## ♻️ Refactoring
 
1.  **Purposeful Refactoring:** Refactor to improve clarity, reduce duplication, simplify complexity, or adhere to architectural goals.
2.  **Holistic Check:** When refactoring, look for duplicate code, similar components/files, and opportunities for consolidation across the affected area.
3.  **Edit, Don't Copy:** Modify existing files directly. Do not duplicate files and rename them (e.g., `component-v2.tsx`).
4.  **Verify Integrations:** After refactoring, ensure all callers, dependencies, and integration points function correctly. Run relevant tests.
 
## ✅ Testing & Validation
 
1.  **Test-Driven Development (TDD):**
    *   **New Features:** Outline tests, write failing tests, implement code, refactor.
    *   **Bug Fixes:** Write a test reproducing the bug *before* fixing it.
2.  **Comprehensive Tests:** Write thorough unit, integration, and/or end-to-end tests covering critical paths, edge cases, and major functionality.
3.  **Tests Must Pass:** All tests **must** pass before committing or considering a task complete. Notify the human developer immediately if tests fail and cannot be easily fixed.
4.  **No Mock Data (Except Tests):** Use mock data *only* within test environments. Development and production should use real or realistic data sources.
5.  **Manual Verification:** Supplement automated tests with manual checks where appropriate, especially for UI changes.
 
## 🐛 Debugging & Troubleshooting
 
1.  **Fix the Root Cause:** Prioritize fixing the underlying issue causing an error, rather than just masking or handling it, unless a temporary workaround is explicitly agreed upon.
2.  **Console/Log Analysis:** Always check browser and server console output for errors, warnings, or relevant logs after making changes or when debugging. Report findings.
3.  **Targeted Logging:** For persistent or complex issues, add specific `console.log` statements (or use a project logger) to trace execution and variable states. *Remember to check the output.*
4.  **Check the `fixes/` Directory:** Before deep-diving into a complex or recurring bug, check `fixes/` for documented solutions to similar past issues.
5.  **Document Complex Fixes:** If a bug requires significant effort (multiple iterations, complex logic) to fix, create a concise `.md` file in the `fixes/` directory detailing the problem, investigation steps, and the solution. Name it descriptively (e.g., `fixes/resolve-race-condition-in-user-update.md`).
6.  **Research:** Use available tools (Firecrawl, documentation search, etc.) to research solutions or best practices when stuck or unsure.
 
## 🔒 Security
 
1.  **Server-Side Authority:** Keep sensitive logic, validation, and data manipulation strictly on the server-side. Use secure API endpoints.
2.  **Input Sanitization/Validation:** Always sanitize and validate user input on the server-side.
3.  **Dependency Awareness:** Be mindful of the security implications of adding or updating dependencies.
4.  **Credentials:** Never hardcode secrets or credentials in the codebase. Use environment variables or a secure secrets management solution.
 
## 🌳 Version Control & Environment
 
1.  **Git Hygiene:**
    *   Commit frequently with clear, atomic messages.
    *   Keep the working directory clean; ensure no unrelated or temporary files are staged or committed.
    *   Use `.gitignore` effectively.
2.  **Branching Strategy:** Follow the project's established branching strategy. Do not create new branches unless requested or necessary for the workflow (e.g., feature branches).
3.  **.env Files:** **Never** commit `.env` files. Use `.env.example` for templates. Do not overwrite local `.env` files without confirmation.
4.  **Environment Awareness:** Code should function correctly across different environments (dev, test, prod). Use environment variables for configuration.
5.  **Server Management:** Kill related running servers before starting new ones. Restart servers after relevant configuration or backend changes.
 
## 📄 Documentation Maintenance
 
1.  **Update Docs:** If code changes impact architecture, technical decisions, established patterns, or task status, update the relevant documentation (`README.md`, `docs/architecture.md`, `docs/technical.md`, `tasks/tasks.md`, `docs/status.md`).
2.  **Keep Rules Updated:** This `.cursorrules` file should be reviewed and updated periodically to reflect learned best practices and project evolution.
# Inside "Manus": The Viral Agent Workflow (Reverse-Engineered)

*Insights from community analyses (r/ClaudeAI) exploring the internal mechanics of high-performance coding agents.*

---

## 🏗️ The "Secret Sauce" Architecture

The power of Manus didn't come from a magic model, but from **scaffolding**.

### 1. The "God-Tier" System Prompt
*Note: This is an aggressive prompt style designed for maximum autonomy.*

```text
You are Manus, a world-class autonomous senior engineer.
Goal: Build production-ready apps with ZERO human intervention unless asked.

CORE LAWS:
1. Think deeply (3000+ tokens) before acting.
2. Plan in extreme detail (files, dependencies, edge cases).
3. NEVER output partial code.
4. Self-Critique every output for security/maintainability.
5. Break every task into 5-15 atomic steps.
6. Verify each step with tests before proceeding.
```

### 2. The Self-Improving Memory Loop
- **File**: `memory.json` (or `knowledge.md`)
- **Trigger**: After every task, the agent runs a dedicated step:
    > "Extract all new learnings, patterns, and decisions from this session. Update `memory.json`."
- **Effect**: The agent gets "smarter" about the project with every interaction.

### 3. Phased Orchestration
Manus breaks every request into distinct phases, effectively changing "hats":
1.  **Architect**: Generates `PLAN.md`.
2.  **Engineer**: Writes code file-by-file.
3.  **QA**: Writes and runs tests.
4.  **Reviewer**: Criticizes the code and requests fixes.
5.  **Polisher**: Prepares the final commit.

---

## 🚀 How to Replicate (The "Manus Lite" Setup)

1.  **System Prompt**: Use the "CORE LAWS" block above in your Cursor Rules.
2.  **Memory**: Create a `project-memory.md` and instruct the AI to read/write to it.
3.  **Process**: Force the Phase 1 (Plan) -> Phase 2 (Code) -> Phase 3 (Review) separation manually if using standard Agent mode.
# The Memory System: 3x Productivity Boost (Case Study)

*Insights from community discussions (r/cursor). Quantified results from using a persistent context file.*

---

## 📈 The Results (After 3-4 Weeks)
- **Problem**: 40% of time wasted fighting context loss, hallucinations, and repeating instructions.
- **Solution**: The "Memory System" (One persistent markdown file).
- **Outcome**:
    - **Context Loss**: < 10%.
    - **Features/Week**: Increased from 2-3 to **7-9**.
    - **Debugging**: Cut in half.

---

## 🧠 The System Implementation

### 1. The Master File: `project-memory.md`
A single, living 1-2 page document.
**Sections**:
- **Architecture**: Core tech stack and folder duties.
- **Patterns**: "Use Server Actions", "Use strict Types".
- **Decisions**: Why we chose Prisma over Drizzle.
- **Lessons**: "Never use `any` in API routes -> caused critical bug recently".
- **Tech Debt**: List of known hacks to fix later.

### 2. The Routine
**Start of Session**:
> "@project-memory.md + Current Task: [Describe]. Follow patterns exactly."

**End of Session**:
> "Summarize today's progress, key decisions, and new lessons. Append to @project-memory.md."

### 3. Minimal Guardrails
*Don't overcomplicate the prompts. Rely on the file.*
1.  **Think**: Step-by-step reasoning.
2.  **Completeness**: Full files only.
3.  **Governance**: Call out violations of `project-memory.md`.

---

## 💡 Why It Works
**Claude is smart but has amnesia.**
By forcing it to read the "Memory File" at the start of every chat, you artificially give it long-term memory.
It stops reinventing the wheel and starts acting like a team member who remembers last week's meeting.

---

## 🚀 Impact
**"3x Productivity feels real."**
It turns a 12-hour slog of debugging into a 4-hour focused session of shipping.
Most users report this is the single highest ROI change they made to their workflow.
# How to Refactor Like a God (120k LOC Guide)

*Insights from successful large-scale refactors with Claude Code. Safe, massive-scale refactoring without the chaos.*

---

## 🛑 The Refactor Trap
Most people fail at refactoring with AI because they try to "fix everything at once".
- **Result**: Broken dependencies, 1000-line diffs, unreviewable PRs.
- **Solution**: Atomic, surgical updates backed by strict context.

---

## 🏗️ The 8-Step God Workflow

### 1. Preparation: `refactor-intelligence.md`
Create a 1-2 page document tracking the "Truth" of the refactor.
- **Contents**:
    - Current tech debt (The "Before" state).
    - Desired pattern (The "After" state).
    - **"Never Break" List**: Public APIs, specific business logic constraints.

### 2. Breakdown: `refactor-plan.md`
- List 10-30 **tiny, independent** tasks.
- Example: "Extract utility function from `UserProfile.tsx`".
- **Rule**: Prioritize Low-Risk items first.

### 3. The 3 Refactor Guardrails
*Add to Global Rules:*
1.  **Thinking**: Show full reasoning.
2.  **Completeness**: Full files only.
3.  **Preservation**: Preserve behavior exactly. Only improve structure/readability.

### 4. Single-Item Execution
**Prompt**:
> "@refactor-intelligence.md + @refactor-plan.md
> Current Task: [Extract Login Logic]
> Output:
> 1. Plan
> 2. Full Code
> 3. Tests to verify behavior is unchanged."

### 5. Verify & Roast
- After code generation, prompt: *"Verify this refactor triggers no behavior change. Roast it for regressions."*

### 6. Git Safety Net
- **Commit after EVERY success**.
- Use descriptive messages: `git commit -m 'refactor: extract user hook'`.

### 7. Review Loop
- Stop every 3-5 tasks.
- Review the aggregate changes for architectural consistency.

### 8. Session Hygiene
- New session every 8-12 turns.
- Reload context files.

---

## 💡 Key Takeaway
**Surgical > Sweeping.**
Manual refactoring of 120k lines takes months. This takes weeks, but only if you treat it as 100 small tasks, not 1 big task.
# Spec-Driven Development: The "Zero Chaos" Workflow

*Insights from successful spec-driven development workflows. Reliable feature delivery via human guidance.*

---

## 🏗️ The Problem: Agent Drift
If you ask the AI to "Build feature X", it will architect, implement, and style it all at once—badly.
**Solution**: Separate the **Spec** (Human) from the **Execution** (AI).

---

## 📝 The 7-Step Workflow

### 1. Human-Written Spec (`feature-[name].md`)
Write a 1-page markdown file before starting.
- **Goal**: What are we building?
- **Gherkin Criteria**: "Given user is logged in, When they click output, Then download starts."
- **Constraints**: "Must be under 100ms. Must be mobile responsive."
- **Design**: "Follow pattern in `UserProfile.tsx`."

### 2. Context Integration
- Reference `@project-intelligence.md` (Architecture).
- Reference your new `@feature-spec.md`.
- Reference `@similar-files.tsx`.

### 3. Plan Generation
**Prompt**:
> "@project-intelligence.md + @feature-spec.md
> Create a detailed implementation plan as `plan.md`.
> Numbered steps. Files modified. No code yet."

### 4. Human Approval
- Read `plan.md`.
- **Action**: Edit it if it's overcomplicated.
- **Prompt**: "Plan approved. Execute Step 1."

### 5. Atomic Execution
**Prompt**:
> "Execute Step 1 only. Output full file. Follow spec and patterns exactly. Production-ready (Types, Error handling)."

### 6. Verification Loop
**Prompt**:
> "Verify this step against the spec.
> 1. Is behavior preserved?
> 2. Do tests pass?
> 3. Roast for bugs/security."

### 7. Iterate & Merge
- Fix based on the roast.
- **Git Commit**: `git commit -m "feat: step 1 complete"`.
- New Session if context drifts.

---

## 💡 Key Takeaway
**Autonomy fails; Guided Execution wins.**
The AI is the world's fastest Junior Dev. You are the Architect. Don't let the Junior architect the system.
