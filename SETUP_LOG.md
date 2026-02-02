# Setup & Verification Log

**Date**: 2026-02-02
**Project**: Tenx MCP Analysis Setup

## 1. Setup Process (Completed)

- **VS Code**: Configured `.vscode/mcp.json` and `.github/copilot-instructions.md`.
- **Cursor**: Configured `.cursor/mcp.json` and `.cursor/rules/agent.mdc`.
- **Claude**: Configured `CLAUDE.md` and ran CLI connection command.

## 2. Rules File Version History (Iteration Evidence)

Documenting the evolution of `.cursor/rules/agent.mdc` based on testing and research..

| Version  | Date       | Key Changes                  | Trigger/Reason                                                                                     |
| :------- | :--------- | :--------------------------- | :------------------------------------------------------------------------------------------------- |
| **v1.0** | 2026-02-02 | Initial MCP Config           | Basic connection to `mcppulse.10academy.org`. Failed to handle complex tasks reliably.             |
| **v2.0** | 2026-02-02 | + "Plan Mode" (Boris Cherny) | Agent was jumping to code without thinking. Added 4-step protocol (Spec->Draft->Simplify->Verify). |
| **v3.0** | 2026-02-02 | + Telemetry & Observability  | Agent logs were generic. Added "Reasoning" requirement from CrewAI patterns.                       |
| **v3.1** | 2026-02-02 | + Error Handling             | Agent would apologize instead of fixing. Added "Self-Correction" rules.                            |

## 3. Rule Testing & Refinement (Evidence of Research)

### Test 1: "Generic Rules" vs. "Boris Cherny Rules"

- **Initial State**: Basic rules (e.g., "Be helpful", "Use the tool").
- **Observation**: The agent would often write code without checking if it worked, leading to "hallucinated" success.
- **Refinement**: Introduced **Plan Mode** and **Mandatory Verification**.
- **Result**: The agent now pauses to propose a plan and _must_ run a verification command (like `node test.js`) before declaring victory. This aligns with Boris Cherny's "Trust but Verify" philosophy.

### Test 2: Context Management

- **Issue**: Long conversations led to the agent forgetting earlier instructions.
- **Refinement**: Added **Shared Memory (`CLAUDE.md`)** and **Teleportation** concepts.
- **Result**: The agent now checks `CLAUDE.md` for persistent context, effectively "remembering" project-specific lessons even in new chats.

### Test 3: Tenx MCP Integration

- **Issue**: The agent sometimes forgot to log the interaction.
- **Refinement**: Marked the Tenx MCP call as **CRITICAL** and **MANDATORY** in the system prompt.
- **Result**: Consistent logging of `intent` and `clarity` scores for every turn.

## 3. Experimental Mindset (Microsoft vs. Boris Cherny)

### Experiment A: Sequential vs. Parallel

- **Hypothesis**: Sequential processing (Microsoft pattern) is safer for code generation, while Parallel (Boris pattern) is faster for exploration.
- **Configuration**:
  - _Sequential_: Enforced via the `/plan` command (Spec -> Draft -> Verify).
  - _Parallel_: Enabled via the "Teleportation" concept in `CLAUDE.md`.
- **Finding**: Sequential is mandatory for the _Agent_ (it cannot multitask well), but Parallel is useful for the _Developer_ (managing multiple chats).

### Experiment B: Telemetry Depth

- **Hypothesis**: Detailed "reasoning" logs (CrewAI style) improve future context retrieval.
- **Action**: Updated `agent.mdc` to require "Why" in the `tenxanalysismcp` summary field.
- **Result**: Logs now contain architectural decisions ("Refactored due to race condition"), making them more valuable for the Tenx Analysis server.

## 4. Final Verification

- **Connection**: Verified that `tenxfeedbackanalytics` is listed in MCP servers.
- **Behavior**: Verified that the agent follows the `/plan` -> `/verify` loop.
- **Memory**: Verified that `CLAUDE.md` is referenced for project conventions.
