# Efficiency Handbook 7: Stack-Specific Implementation Guides

*Tailored best practices and operational protocols for modern development stacks. This handbook covers Next.js, Ruby on Rails, Flutter migrations, and the rules for maintaining living documentation.*

---

## ⚛️ Next.js Mastery (App Router)
Next.js projects in Cursor should strictly adhere to modern (v14+) patterns to leverage the AI's full potential.

### Core Golden Rules
1. **App Router Only**: Always target the `app/` directory. Use folders for route groups (e.g., `(marketing)`) and `layout.tsx` for shared UI.
2. **Server Components by Default**: Never use `'use client'` unless interactivity (state/effects) is mandatory.
3. **Native Fetch**: Prefer `async/await` with `fetch` in Server Components over Client-side hooks.
4. **Server Actions**: Use `'use server'` for mutations instead of traditional API routes.
5. **SEO First**: Always include `export const metadata` in page files.

---

## 💎 Ruby on Rails "Gold Standard"
For Rails (v7+), consistency is key to avoiding "heavy framework" hallucinations.

### Recommended Structure
Reference the [Maybe Finance](https://github.com/maybe-finance/maybe) repository for production-grade modular rules:
- **Models**: `app/models/**/*.rb` (Active Record patterns).
- **Controllers**: Skinny controllers; extract logic to Service Objects.
- **Frontend**: **Prefer Hotwire** (Turbo + Stimulus) over React/Vue.
- **Testing**: Use **RSpec** with Request Specs for integration.

---

## 📱 Flutter Migration & Advanced Tracing
Mobile migrations require strict scoping and methodical call-stack tracing to avoid logic drift.

### The Tracing Procedure (Version 3)
When `codebase_search` fails, follow this linear path:
1. **Identify Entry Point**: Find the widget or API Controller triggering the behavior.
2. **Locate Callee**: Identify the immediate next service call.
3. **Find Source**: Use DI mapping (grep `Bind<Interface>` or `AddScoped`) to find the concrete implementation file.
4. **Analyze & Iterate**: Move step-by-step through the call stack; never guess.

### Implementation Protocol
- **Modification Scope**: NEVER modify files outside the specific Flutter client directory.
- **Justify Creations**: Every new file must include a justification in `development_notes/changes_with_justification.md` confirming that existing functionality was searched and found insufficient.

---

## 📝 Rules for Living Documentation
Documentation files (`.mdc`) must remain living project memory. If they go stale, the AI will regress.

### Update Requirements
- **Frontend changes** → Update `frontend.mdc`.
- **Backend changes** → Update `backend.mdc`.
- **Architectural shifts** → ALWAYS update `main.mdc`.

### Status Indicators
Use these indicators in your documentation at a glance:
- ✅ **Stable / Complete**: Feature is verified and in production.
- 🚧 **In Progress / Partial**: Active development; some components may be stubbed.
- ❌ **Broken / Deprecated**: Needs removal or immediate fixing.

---

## 📊 Summary Checklist
- [ ] **Next.js**: Is `next/image` and `next/font` being used for optimization?
- [ ] **Rails**: Are controllers skinny and using Service Objects?
- [ ] **Flutter**: Is the implementation documented in `development_notes/`?
- [ ] **Maintenance**: Did I update the relevant `.mdc` file after the last commit?
