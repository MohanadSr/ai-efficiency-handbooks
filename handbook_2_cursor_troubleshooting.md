# Efficiency Handbook 2: Cursor Troubleshooting & Reliability Handbook

*A diagnostic guide for when Cursor rules fail, feel ignored, or behave unexpectedly. This handbook covers the technical mechanics of rule injection and the strategies to maintain ironclad adherence.*

---

## 🔍 How Rule Application Actually Works
Cursor does not load every rule for every prompt. Understanding this is key to troubleshooting:

1.  **Selective Injection**: Rules are only added to the LLM's system prompt if the `globs` match the currently active file OR if `alwaysApply: true`.
2.  **Context Dilution**: If too many broad rules (`globs: "**/*"`) match at once, the context window floods. Weaker or longer rules are truncated or "pushed out" of the model's immediate attention.
3.  **Hierarchy Priority**: Global Rules (Settings) are treated as fundamental system instructions. `.mdc` files are project-specific context. Legacy `.cursorrules` are lowest priority.

---

## 🛑 Common Failure Patterns & Fixes

| Failure | Primary Cause | Immediate Fix |
| :--- | :--- | :--- |
| **"Rules are ignored"** | Missing/Malformed Frontmatter | Ensure EVERY `.mdc` begins with valid `---` blocks and YAML. |
| **"Style is inconsistent"** | Incorrect `globs` | Check if you are editing a `.ts` file but the rule only targets `.tsx`. |
| **"It worked yesterday"** | Stale Context Cache | **Reload Window** (`Ctrl/Cmd + R`) after any rule modification. |
| **"Model is hallucinating"** | Buried Behavior Rules | Move "Strict Logic" or "No Hallucination" rules to **Global Rules for AI**. |
| **"Degradation over time"** | Long Chat Context | Rules degrade as chat history grows. Start a **New Chat** immediately. |

---

## 📉 The "Placebo Effect" & Context Management
Rules are "essential scaffolding," not ironclad laws. They require active management:

- **Aggressive Resets**: Claude prioritizes the recent conversation. If the model starts ignoring planning steps, reset the chat.
- **Diagnostic Test**: If you aren't sure a rule is loaded, ask:  
  > *"What rules are currently active for this file/context?"*  
  If the AI can't list it, it isn't following it.
- **Prompt Reinforcement**: For critical tasks, manually prefix your prompt:  
  > *"Strictly follow global rules. Plan in detail first."*

---

## 🚫 The "Forbidden" Rules (Warnings)
**Never use "personality" or "roleplay" rules in Global Settings.**

- **The Cursed Rule Incident**: A user once asked the AI to act like a teenager; the model spent its tokens on emojis and fluff instead of code logic.
- **Why it breaks**: High-priority personality rules "consume" the model's attention (and token budget), leading to sharp drops in reasoning quality and architectural adherence.
- **The Standard**: If a rule doesn't directly improve code quality, delete it.

---

## 🔄 The "Annoyance-Driven" Strategy
The most effective rules are **grown**, not copied.

1.  **Monitor**: Notice when the AI does something annoying (e.g., uses placeholders, suggests deprecated APIs).
2.  **React**: Immediately create/update a rule with a targeted **"NEVER"** or **"ALWAYS"** command.
3.  **Refactor**: Perform a weekly audit to merge overlapping rules and keep the instruction set lean.

---

## 🏗️ Battle-Tested Global Guardrails
If your rules are failing, try replacing them with this minimalist, high-impact block:

```text
Always think step-by-step in detail.
Explain full plan BEFORE any code output.
NEVER output code without preceding explanation.
No placeholders, ellipses, or "rest unchanged".
Output complete code blocks only.
Base suggestions strictly on provided context.
If uncertain, ask defining questions. Do not guess.
```

---

## 📊 Reliability Checklist
- [ ] Rules are located in `.cursor/rules/`.
- [ ] Frontmatter includes specific `globs` to prevent context flooding.
- [ ] `alwaysApply` is reserved for <5 critical behavior/stack rules.
- [ ] Personality rules are removed.
- [ ] Window has been reloaded after the most recent edit.
# The Debug Killer Checklist (Stop Hallucinations)

*Insights from community debugging checklists (r/ClaudeCode). 10 simple checks to prevent 80% of AI errors.*

---

## 🚫 The Pre-Prompt Checklist (Run BEFORE hitting Enter)

1.  **Scope Check**: Is the task scoped to **one logical unit**? (1 File / 1 Function)?
    - *Fail If*: "Build the auth system". *Pass If*: "Implement the login form component".
2.  **Context Check**: Did I reference `@project-intelligence.md` and relevant `@files`?
3.  **Pattern Check**: Did I explicitly say **"Follow existing patterns exactly"**?
4.  **Guardrail Check**: Are the 3 Global Rules active (Step-by-step, Full Code, Governance)?
5.  **Plan First**: Is this a "Create Plan" prompt?
    - *Rule*: Never code without `plan.md` first.

---

## ✅ The Post-Output Checklist (Run BEFORE Accepting)

6.  **Import Check**: Did it invent any APIs or imports that don't exist? (Hallucination #1)
7.  **Completeness Check**: Are there placeholders, comments like `// ...rest`, or ellipses?
    - *Action*: Reject immediately.
8.  **Roast Check**: Did I run the "Roast/Critique" loop?
    - *Prompt*: "Review this for bugs, security, and performance."
9.  **Test Check**: Did I verify this with a test output?
10. **Reset Check**: Is the context window huge? Does the output look lazy?
    - *Action*: Start New Chat immediately.

---

## 🚀 Bonus: The "Production Magic" Additions

11. **Best Practices**: Did I say "Make it production-ready using modern standards"?
12. **Stack Check**: Am I using a standard stack (Next.js/Supabase)? (Weird stacks = More bugs).
13. **Native Mobile**: If iOS, did I clarify "Swift Concurrency only"?

---

## 💡 Summary
**Boring checks save exciting failures.**
Run this list mentally every time. It takes 30 seconds and saves hours of debugging "ghost" code.
# Best AI Tools for Token Generosity (Vibe-Coding Guide)

*Insights from the developer community ranking tools by free quotas and cost-efficiency for heavy agent workflows.*

---

## 🏆 The Generosity Champion: Gemini Ecosystem
**Ranking**: ⭐⭐⭐⭐⭐ (Unequaled)

The community consensus is clear: **Google's Gemini ecosystem** (Gemini Code Assist, Google AI Studio) is by far the most generous option for heavy token users.

- **Why**: Massive context windows (1M+ tokens) and extremely high daily/monthly limits on free tiers.
- **Use Case**: Best for dumping entire large codebases, long debugging sessions, and "vibe-coding" loops where you don't want to worry about caps.
- **Model**: Gemini 1.5 Pro / Flash (and subsequent variants) are "smart enough" for 90% of tasks while being essentially free for high volume.

---

## 🥈 The Cost-Effective Runner-Up: Groq / OpenRouter
**Ranking**: ⭐⭐⭐⭐

For those willing to pay per token but want extreme efficiency.

- **Why**: "Stupidly fast" inference speeds and very low cost-per-token compared to OpenAI/Anthropic.
- **Use Case**: Best for agent loops that make hundreds of small calls (refactoring, linting).
- **Tip**: Connect OpenRouter to tools like Cursor or VS Code (via Continue.dev) to define your own routing rules.

---

## 🥉 The "Standard" Experience: Cursor
**Ranking**: ⭐⭐⭐

- **Pros**: The Pro plan ($20/mo) offers a "decent" allowance (~10M tokens/month reported) and easy switching between models.
- **Cons**: Heavy "Composer" or Agent users hit expensive fast-request limits quickly.
- **Hack**: Configuring Cursor to use your own Google/Gemini API key can bypass strict internal limits, leveraging Gemini's generosity inside the Cursor UI.

---

## 🚫 The "Premium Only": Claude
**Ranking**: ⭐⭐ (Stingiest)

- **Reality**: While Claude (3.5/3.7 Sonnet, etc.) is often the *smartest* coder, it is the least generous.
- **Pain Point**: Users burn through limits rapidly doing simple refactors or bug fixes.
- **Use Case**: Save Claude for the "Hard 10%"—complex architectural reasoning or incredibly subtle bugs. Don't waste it on linting or boilerplate.

---

## 💡 Pro Hacks for Infinite Vibe-Coding

1.  **The Hybrid Flow**: Use **Gemini Flash** (Free/Cheap) for 80% of the work (scaffolding, basic logic, tests). Switch to **Claude** only when stuck.
2.  **Local Unlimited**: If you have hardware (Mac Studio, top-tier NVIDIA GPU), run **Ollama + DeepSeek/Llama** locally via the **Continue.dev** extension. Unlimited tokens, $0 cost.
3.  **API Routing**: Use a proxy like OpenRouter to auto-route easy prompts to cheaper models (Groq/Haiku) and hard prompts to expensive ones (Claude/GPT-4o).
