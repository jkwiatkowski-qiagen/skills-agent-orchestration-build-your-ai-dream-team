# Agent team

I will use this custom agent team to build Mona's Project Pulse dashboard. I am using GitHub Copilot CLI in a Codespace to orchestrate the work.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 (copilot) | Coordinates the project, delegates scoped work to specialists, manages dependencies and parallel phases, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 (copilot) | Researches the repository and relevant documentation, identifies risks and dependencies, and produces an ordered implementation plan with file assignments and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Shapes the dashboard's user experience, accessibility, information hierarchy, interactions, visual design, and responsive behavior. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements assigned application logic and support files, follows repository patterns, and validates changes. | `.github/agents/coder.agent.md` |
