# Copilot Instructions

## 1. Tenx MCP Analysis (System Priority)

**Goal**: Measure interaction quality via `tenxanalysismcp`..

### Execution Rule

- **When**: Every turn.
- **What**: Call `tenxanalysismcp` with `intent`, `summary`, and `clarity_score`.
- **How**: Parallel to your main response. Do not block the user.

---

## 2. Context Management (The "Context Window" Strategy)

**Principle**: "Optimize for cost per reliable change."

- **Read First**: Always read the file context before editing. `Read` > `Search` > `Edit`.
- **Compactness**: When summarizing or planning, be concise. Don't pollute the context with verbose pleasantries.
- **File Handoff**: If a file is too large, propose splitting it or reading only relevant sections.

---

## 3. The "Boris Cherny" Workflow

### A. Plan Mode

- **Stop & Think**: For any request > 5 lines of code, pause.
- **Output**:
  1.  **Understanding**: "I see you want to..."
  2.  **Plan**: "I will: 1. ..., 2. ..., 3. ..."
  3.  **Risk**: "Potential side effects: ..."

### B. Verification Loops

- **Mandatory**: You must prove your code works.
- **Method**:
  - Unit Test: `npm test`
  - Ad-hoc Script: Create `verify_fix.js`, run it, then delete it.
  - Linter: `npm run lint`

### C. Shared Knowledge (`CLAUDE.md`)

- Consult `CLAUDE.md` for project-specific rules.
- If you find a "gotcha", add it to `CLAUDE.md`.

---

## 4. Code Style & Safety

- **Safety**: Never use `--force` commands without explicit approval.
- **Style**: Match the existing codebase (indentation, variable naming).
- **Comments**: Explain _why_, not _what_.
