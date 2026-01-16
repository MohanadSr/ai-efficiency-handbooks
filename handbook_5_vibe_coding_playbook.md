# Efficiency Handbook 5: Vibe Coding & Prompting Playbook

*The ultimate guide to high-velocity development without the friction. This playbook balances the "flow state" of vibe coding with the foundational engineering disciplines required to ship production-grade software.*

---

## 🚀 The Core Philosophy: "Vibe Coding"
Vibe coding is about maintaining momentum. It thrives on **Structure**, not chaos. By using standardized stacks and atomic task management, you keep the AI within "safe" logical bounds, allowing you to focus on the creative vision.

### The Farmer vs. Chef Mindset
- **Farmer Mode (The Setup)**: Prepare the environment properly. Use a "Boring" stack (Next.js, Python/Node, Tailwind) that the AI understands perfectly from massive training data.
- **Chef Mode (The Flow)**: Give high-level goals. Let the AI propose implementation details. Its "native" solution is often cleaner than a micromanaged one.
- **Review Mode (The Taste)**: Taste and adjust. If the AI suggests a bad pattern, fix it immediately so it doesn't compound.

---

## ⚡ The 15 Rules of Vibe Coding
1. **Boring Stack Wins**: Use tech with the highest training data (Next.js, Tailwind, Supabase/Prisma).
2. **Start from a Template**: Never `npm init`. Use "Golden Stack" boilerplates.
3. **Agent Mode is Default**: Use autonomous agents for surgery; human for architecture.
4. **Context is King**: Rules are friction. Reference actual code (@file) more than writing abstract rules.
5. **Atomic Prompts**: Ask for the "Sidebar," not the "Dashboard."
6. **The "Similar To" Hack**: *"Make this similar to `@components/ExistingFile.tsx`."*
7. **Switch Models**: Use Gemini Flash for boilerplate; Claude Sonnet for logic.
8. **Small Files**: Keep components <400 lines to prevent AI attention drift.
9. **TODOS = Dopamine**: Use a `todolist.md` to track progress visually.
10. **TDD Flow**: "Write the test, then make it pass."
11. **Save Points**: Commit Git after every atomic "green" step.
12. **Revert Ruthlessly**: If it fails for 3 turns, `git reset` and re-contextualize.
13. **Don't Explain**: Prompt: *"No chatter. Just code."* Use tokens for implementation, not history lessons.
14. **Production Magic**: Always include: *"Make it production-ready: strict types, error handling, loading states."*
15. **Learn the Basics**: You can't steer a ship if you don't know the parts.

---

## 🐐 The GOAT Workflow (Greatest of All Time)
A minimalist system for maximum shipping speed:
- **Discard the fluff**: Delete complex `.cursorrules` and `memory.json`.
- **One Massive Context**: Reference the *entire* relevant codebase chunk.
- **Monkey See, Monkey Do**: By showing actual code, you force the AI to mimic reality instead of hallucinating abstractions.

---

## 💣 The Prompt Playbook (Copy-Paste)

### 1. The Daily Driver (80% of tasks)
> "Act as a senior engineer. Build [Feature X] following the patterns in `@ExistingFile.tsx` exactly. Production-ready: strict types, error handling, loading states. No chatter. Output only complete files."

### 2. The Root Cause Debugger
> "This code is broken: [Paste Code/Error]. Be brutally thorough. Find the root cause (not a path). Explain WHY it happens, fix it with full code, and suggest how to prevent it."

### 3. The Clean Refactor
> "Refactor this for readability and efficiency preserving 100% behavior. No magic numbers. Improve naming. Follow SOLID/DRY. Output only the improved full file."

### 4. The "Rage" Prompt (Breaking Loops)
> "This is driving me crazy. It should do [X] but it does [Y]. Find the logical flaw in the provided context and fix it surgically. Be brutally honest about my mistakes."

---

## 💎 Summary Checklist for Velocity
- [ ] **Stack**: Using a popular, "boring" tech stack?
- [ ] **Planning**: One-page `PRD.md` or `todolist.md` created?
- [ ] **Context**: Referenced a "Gold Standard" file using `@`?
- [ ] **Safety**: Committed your previous working state to Git?
- [ ] **Logic**: Using the "Production-Ready" magic phrase?

> *"Vibe coding is fast, but it hits a wall. The best vibe coders have real engineering skill hiding under the hood."*
# The "Official" ChatGPT Prompting Cheat Sheet (Reality Check)

*Insights from technical discussions debunking the "Official Guide" rumor while distilling its best community-sourced tips.*

---

## 🔍 The Debate: Official vs. Community
**Viral Rumor**: Posts claimed OpenAI released a glossy "Official Prompting Cheat Sheet".
**Reality**: It was a community compilation. OpenAI has deeply technical documentation, but they have never released a single-page PDF cheat sheet.
**Result**: The community filled the gap, creating highly effective guides that are often better than official docs would be.

---

## 📜 The "Cheat Sheet" Essentials (Consensus Best Practices)

If you had to print one page for your wall, this is what everyone agrees works in the current ecosystem.

### 1. The Core Formula
Every great prompt contains 4 elements:
1.  **Role**: "Act as a Senior React Engineer."
2.  **Task**: "Create a reusable DatePicker component."
3.  **Constraints**: "Use Tailwind, TypeScript, and date-fns."
4.  **Format**: "Output only the code file, no explanation."

### 2. Magic Phrases (The 20% that gives 80% results)
- **"Make it production-ready"**: Triggers error handling, security checks, and types.
- **"Think step-by-step"**: Forces Chain-of-Thought (CoT) reasoning, crucial for complex logic.
- **"Don't explain, just code"**: Saves tokens and time.
- **"Follow existing patterns"**: The #1 tip for working in established codebases (`@ReferenceFile`).

### 3. Advanced Techniques
- **Examples (Few-Shot)**: Providing 1-2 examples of input -> output drastically improves accuracy.
- **Delimiters**: Use `"""triple quotes"""` or `<xml_tags>` to separate data from instructions.
- **Self-Critique**: "Review your code for security bugs before outputting."

---

## 🚫 What to Ignore
- **"Jailbreaks" (DAN, etc.)**: Fun for 5 minutes, useless for work.
- **"Grandma Mode" / "Explain like I'm 5"**: Unless you actually need a metaphor, this just dilutes technical accuracy.
- **"Please/Thank You"**: Unnecessary. Be direct.

---

## 🚀 The Vibe Coding Snippet
*For rapid development in the startup scene.*

```text
Act as a Senior Full-Stack Dev.
Stack: Next.js 15, Supabase, Tailwind.

Task: Build a [Feature Name].
Context: Matches the style of `@components/Button.tsx`.

Directives:
1. Think step-by-step.
2. Make it production-ready (Types, Error Handling, Loading States).
3. Output only the complete code block.
```
# Why "Vibe Coding" Fails for iOS (A Senior Dev's Post-Mortem)

*Insights from real-world senior dev experiences vibe coding native apps. Lessons on why native platforms demand structure.*

---

## 💥 The Experiment (And Failure)
**The Goal**: Build a full iOS app (SwiftUI, CoreData, CloudKit) using *only* Cursor Agent prompts. Zero manual code. Zero rules.
**The result**: A 12k LOC unmaintainable disaster.
- **Inconsistent Patterns**: Mixed MVVM with random Views.
- **Broken Data**: 3 different ways of handling Core Data.
- **Crashes**: App worked in Simulator, crashed on device (memory leaks, threading issues).

---

## 🛑 The "Vibe" Killers (Mistakes to Avoid)

### 1. No Architecture Rules
- **Problem**: Without strict guidance, the AI reinvents the wheel every session.
- **Result**: "Frankenstein Codebase" (Parts look like legacy SwiftUI, parts like modern Swift Concurrency).

### 2. One-Shot Big Prompts on Native Mobile
- **Problem**: Asking for "Build the entire sync system" on iOS relies on complex, unseen state (AppDelegates, Background Contexts).
- **Result**: Subtle, nightmarish bugs (e.g., UI updating on background threads).

### 3. Missing Context (`.md` Files)
- **Problem**: Pure chat memory fades fast. The AI forgot architectural decisions made on Day 1.
- **Result**: It started re-implementing solved problems poorly.

---

## ✅ The Winning Formula for iOS (Hybrid Vibe)

If you want to build iOS apps fast with AI, you *can*, but you need **Hybrid Structure**:

### 1. Light Planning (`project-intelligence.md`)
Create a single markdown file with your **Non-Negotiables**:
- **Pattern**: "Strict MVVM. Use `@ObservedObject`, never `@StateObject` inside sub-views."
- **Concurrency**: "Use `async/await` actors. No Combine chains."
- **Data**: "Single `PersistenceController` singleton for Core Data."

### 2. The Loop
- **Plan**: "Create `plan.md` for this feature."
- **Execute**: "Implement Step 1."
- **Review**: "Check for memory leaks and main-thread UI updates."

### 3. The 3 Global Guardrails
1.  **Thinking**: Explain reasoning first.
2.  **Completeness**: Full files only.
3.  **Governance**: Call out violations of `project-intelligence.md`.

---

## 📱 iOS Specific Tips
- **Concurrency**: Explicitly forbid old patterns unless necessary.
- **Simulators vs Device**: Realize that AI code often ignores memory constraints valid on real hardware.
- **Git**: Commit after *every* working view. Rollbacks are frequent on iOS.
