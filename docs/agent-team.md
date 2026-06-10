# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the work for Mona's Project Pulse dashboard with this custom agent team:

- **Orchestrator** — *Claude Opus 4.7 (copilot)* — coordinates Planner, Coder, and Designer from the GitHub Copilot CLI and manages task delegation. Definition: `.github/agents/orchestrator.agent.md`
- **Planner** — *Claude Opus 4.7 (copilot)* — researches the repository, dependencies, edge cases, and creates implementation plans. Definition: `.github/agents/planner.agent.md`
- **Coder** — *GPT-5.5 (copilot)* — implements code, fixes bugs, and handles runnable app support such as Project Pulse launch config. Definition: `.github/agents/coder.agent.md`
- **Designer** — *Gemini 3.1 Pro (copilot)* — handles UI/UX, accessibility, and dashboard styling for a polished Project Pulse experience. Definition: `.github/agents/designer.agent.md`

The Planner sets the direction, the Designer shapes the dashboard experience, the Coder turns the plan into working files, and the Orchestrator keeps the work coordinated so the Project Pulse build stays aligned end to end.
