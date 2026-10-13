# Project Pulse agent team

I will use a custom GitHub Copilot CLI agent team to build Mona's Project Pulse dashboard in this repository. Each agent has a defined file scope and a specific role in the workflow:

| Agent | Model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 (copilot) | Coordinates the overall build, delegates work to specialists, sequences phases, and verifies that the integrated dashboard is coherent and complete. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 (copilot) | Researches the repo, reads relevant docs and code, identifies dependencies and edge cases, and produces the implementation plan with file ownership and validation expectations. | `.github/agents/planner.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements the assigned application logic and support files, follows existing repo patterns, and validates the resulting behavior before reporting back. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Shapes the dashboard's usability, accessibility, information hierarchy, visual clarity, and responsive behavior so the frontend feels polished and intentional. | `.github/agents/designer.agent.md` |

The team works as a sequential-but-parallelizable workflow. The Orchestrator starts by asking the Planner for a repo-informed plan, then breaks it into clear phases with file ownership and dependency ordering. The Planner identifies risks and validation steps, the Designer focuses on the experience and styling, and the Coder implements the code within the assigned file scopes. The Orchestrator then reviews the combined result, keeps overlapping work sequential when needed, and confirms the final outcome. Git operations stay under my control instead of being automated by the agents.
