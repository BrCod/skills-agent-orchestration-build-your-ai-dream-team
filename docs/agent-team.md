# Agent team

For Mona's Project Pulse dashboard, I will use a four-person custom agent team orchestrated through GitHub Copilot CLI inside a GitHub Codespace. The shared definitions live under the repository's `.github/agents/` folder and are designed to split planning, design, programming, and coordination into clear responsibilities.

- Planner — Model: Claude Opus 4.7 (copilot). Responsibility: research the repository, review dependencies and constraints, identify edge cases, and produce a structured implementation plan for the dashboard work. Definition: `.github/agents/planner.agent.md`
- Designer — Model: Gemini 3.1 Pro (copilot). Responsibility: shape the Product Pulse dashboard UX/UI, focusing on accessibility, information hierarchy, interaction flow, and polished visual design with clear project cards, badges, spacing, and responsive layout. Definition: `.github/agents/designer.agent.md`
- Coder — Model: GPT-5.5 (copilot). Responsibility: implement the code changes, fix bugs, and create any required support files or runnable app configuration needed for the dashboard. Definition: `.github/agents/coder.agent.md`
- Orchestrator — Model: Claude Opus 4.7 (copilot). Responsibility: coordinate the Planner, Designer, and Coder agents by breaking the work into phases, assigning file scopes, running tasks in the right order, and verifying the combined result. Definition: `.github/agents/orchestrator.agent.md`

This workflow uses GitHub Copilot CLI in a Codespace to orchestrate the entire build process from planning through implementation and integration.
