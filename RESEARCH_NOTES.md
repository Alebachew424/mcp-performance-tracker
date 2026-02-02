# Research Notes: AI Agent Orchestration

**Date**: 2026-02-02
**Purpose**: Documenting research into advanced AI agent patterns beyond the primary reference.

## 1. Source Diversity
I have consulted the following high-authority sources to broaden the "Boris Cherny" workflow:
1.  **Microsoft Azure Architecture Center**: "AI Agent Orchestration Patterns"
2.  **OpenAI Agents SDK**: "Orchestrating multiple agents"
3.  **CrewAI Framework**: "Role-playing, autonomous AI agents"
4.  **GitHub Blog**: "How to orchestrate agents using mission control"

## 2. Key Findings & Synthesis

### A. Comparative Analysis: Orchestration Patterns

| Pattern | Source | Philosophy | Application in this Project |
| :--- | :--- | :--- | :--- |
| **Plan Mode** | Boris Cherny | "A wrong fast answer is slower than a right slow answer." | Core protocol for complex coding tasks (Spec -> Draft -> Verify). |
| **Sequential Orchestration** | Microsoft Azure | Break complex tasks into dependent steps to reduce error accumulation. | Enforced via the `/plan` command; Agent cannot proceed without user sign-off. |
| **Role-Playing** | CrewAI / OpenAI | Assign specific personas (e.g., "QA Engineer") to narrow context. | Used during the "Verify" phase (Agent switches to "Tester" persona). |
| **Parallel Execution** | Boris Cherny | Run multiple independent streams (terminals) to maximize throughput. | Adopted for *User* workflow (multiple chats) but disabled for *Agent* internal logic (too hallucination-prone). |

### B. Observability & Telemetry (CrewAI & GitHub)
*   **Concept**: "Session logs show reasoning, not just actions." (GitHub)
*   **Application**: The `tenxanalysismcp` is our form of telemetry.
*   **Enhancement**: CrewAI suggests "Tracing" (inputs/outputs). We should explicitly log *why* a decision was made, not just *what*.

### C. The "Handoff" (OpenAI)
*   **Concept**: Specialized agents (Planner vs. Coder vs. Reviewer).
*   **Adaptation**: Since we are in a single-agent IDE context, we use "Personas".
    *   *Rule*: Explicitly switch modes: "Now acting as QA Engineer..."

## 3. Experimental Hypotheses
*   **Hypothesis 1**: Sequential orchestration (Microsoft style) reduces regression errors compared to "do it all" prompts.
*   **Hypothesis 2**: Explicit "telemetry" (logging intent via Tenx MCP) improves the agent's self-correction by forcing it to articulate its goal.

## 4. Curated Resource List
A collection of high-value references used to design this system:

*   **Primary Reference**:
    *   [Boris Cherny's "Claude Code" Thread](https://x.com/bcherny/status/1768349545301885232) - *The foundational workflow.*
*   **Orchestration & Patterns**:
    *   [Microsoft Azure: AI Agent Orchestration](https://learn.microsoft.com/en-us/azure/architecture/guide/ai/agent-orchestration) - *Source of "Sequential vs Parallel" concepts.*
    *   [OpenAI Cookbook: Orchestrating Agents](https://cookbook.openai.com/examples/orchestrating_agents) - *Source of "Handoff" patterns.*
    *   [CrewAI Documentation](https://docs.crewai.com/) - *Source of "Role-Playing" and Telemetry rules.*
*   **MCP & Tools**:
    *   [Model Context Protocol (MCP) Spec](https://github.com/modelcontextprotocol) - *Official spec for server integration.*
    *   [Tenx Analysis Server](https://mcppulse.10academy.org/) - *The target telemetry endpoint.*

## 5. Community Best Practices
*   **"Stop & Think"**: Universally recommended (Anthropic "Thinking", Microsoft "Reasoning").
*   **Deterministic Workflows**: OpenAI suggests "orchestrating via code" (scripts) is more reliable than "orchestrating via LLM". This validates our `npm test` verification rule.
