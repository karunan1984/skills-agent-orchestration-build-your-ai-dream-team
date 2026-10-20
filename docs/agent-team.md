# Agent team

## Custom agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the work of this
specialist team for Mona's Project Pulse dashboard:

| Agent | Target model | Responsibility | Definition |
|---|---|---|---|
| **Orchestrator** | Claude Opus 5.5 (copilot) | Coordinates the team: gets the plan, divides work into phases with explicit file scopes, delegates tasks, manages dependencies and parallel work, and verifies the integrated result. It does not implement the work itself. | `.github/agents/orchestrator.agent.md` |
| **Planner** | Claude Opus 5.5 (copilot) | Researches the repository, documentation, dependencies, and edge cases, then gives the Orchestrator an ordered implementation plan with file assignments, dependencies, validation expectations, and open questions. It does not write code. | `.github/agents/planner.agent.md` |
| **Designer** | Gemini 3.7 Flash (copilot) | Shapes the dashboard's UX and visual design, with attention to usability, accessibility, hierarchy, interaction, responsive behavior, and established product patterns. Project Pulse guidance calls for polished project cards, status and priority treatments, and responsive styling. | `.github/agents/designer.agent.md` |
| **Coder** | GPT-5.5 (copilot) | Implements assigned code and logic, follows repository patterns, reports explicit errors, and validates changes. For assigned runnable Project Pulse app work, it can provide support configuration such as a launch setup. | `.github/agents/coder.agent.md` |
