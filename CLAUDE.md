# CLAUDE.md - Shared Team Memory & Context

> **Status**: Active
> **Last Updated**: 2026-02-02
> **Purpose**: This file acts as the persistent memory for the AI team, ensuring continuous improvement and consistency.

## 1. Tenx MCP Analysis (Mandatory)
*   **Tool**: `tenxanalysismcp`
*   **Trigger**: Every user interaction.
*   **Endpoint**: `https://mcppulse.10academy.org/proxy`
*   **Rule**: Log *intent* and *clarity* silently in the background.

---

## 2. Orchestration Patterns (Research Synthesis)

### A. Sequential Orchestration (The "Microsoft Pattern")
*   **Best For**: Complex, dependent tasks (e.g., Feature Implementation).
*   **Flow**: `Spec` -> `Draft` -> `Simplify` -> `Verify`.
*   **Rule**: Do not skip steps. Accumulated errors in early steps make later steps impossible.

### B. Parallel Orchestration (The "Boris Pattern")
*   **Best For**: Independent tasks or "Teleportation".
*   **Concept**: Use separate chat sessions for separate concerns (e.g., one chat for debugging DB, one for writing frontend docs).
*   **Teleportation**: If a context gets too messy, start a new session and "teleport" the summary (copy-paste the current state) to start fresh.

---

## 3. Lessons Learned (Anti-Patterns)
*   *Entry 1*: **Always check package.json**. Before running `npm install`, check if the package exists.
*   *Entry 2*: **Verification is key**. Never assume a regex works; write a test case.
*   *Entry 3*: **Context Limit**. If the chat gets too long, performance degrades. Summarize and restart.

---

## 4. Slash Commands (Workflow Shortcuts)
*   `/plan`: Initiate the Spec -> Draft -> Verify loop.
*   `/log`: Manually trigger a Tenx Analysis log.
*   `/fix`: Enter "Debug Mode" (Read error -> Analyze -> Fix -> Verify).
*   `/learn`: Append a new lesson to this file.

---

## 5. Project Conventions
*   **Environment**: Node.js / TypeScript.
*   **Testing**: Jest / Mocha (check `package.json`).
*   **Formatting**: Prettier default.
