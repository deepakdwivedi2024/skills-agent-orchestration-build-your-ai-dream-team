# Project Pulse implementation plan

## Summary

Project Pulse is a small static dashboard meant to help contributors quickly review active work across projects. The implementation should follow the repo brief, keep the workflow split between the Designer and Coder, and let the Orchestrator keep the build coordinated and verifiable. The app should be lightweight, readable, and runnable from a VS Code launch configuration that opens the dashboard rather than a directory listing.

## File assignments

- `app/project-data.json` — Coder-owned source of truth for project data. Must contain a top-level `projects` array with `name`, `owner`, `status`, `recentActivity`, and `priority`.
- `app/index.html` — Coder-owned page shell that loads data, renders project cards, and wires the dashboard structure to the stylesheet.
- `app/styles.css` — Designer-owned visual system for layout, badges, cards, spacing, contrast, and responsiveness. Must include clear hooks such as `.dashboard` and `.project-card`.
- `.vscode/launch.json` — Coder-owned preview support to serve the `app/` directory and open `index.html`.
- `docs/project-pulse-plan.md` — Planner-owned plan and validation checklist.
- `docs/agent-team.md` — documentation of the agent roles and model assignments; referenced as project context but not part of the implementation logic.

## Ordered implementation steps

### 1. Confirm the data contract and project scope

- Confirm the required dashboard fields from the project brief: active projects, owner, status, recent activity, priority, and contributor-friendly summaries.
- Define the JSON schema in `app/project-data.json` before any HTML rendering is built.
- Dependencies: none beyond the project brief and agent-role guidance.
- Ownership: Coder, with Orchestrator review.

### 2. Draft the dashboard structure and interactions

- Build the semantic HTML skeleton in `app/index.html` with a dashboard container, project header, card grid, and status/priority presentation.
- Keep the structure intentionally simple so the content is easy to populate from JSON and easy to style.
- Dependencies: data schema must exist first so the UI can render known fields without guessing.
- Ownership: Coder; visual decisions are aligned with Designer guidance.

### 3. Apply the visual design system

- Use `app/styles.css` to establish hierarchy, spacing, badge styles, card elevation, and responsive behavior.
- Apply consistent treatment to status, recent activity, and priority so each card is scannable at a glance.
- Dependencies: HTML structure and card classes must already exist so the styling matches the final layout.
- Ownership: Designer, with Coder support for technical integration.

### 4. Connect data to the UI and preview behavior

- Ensure the page loads the project data source and renders a card for each project in the array.
- Validate that the dashboard still works if any project is missing a field or has a long label.
- Dependencies: the JSON contract and page structure must be stable before rendering logic is tested.
- Ownership: Coder.

### 5. Add the launch configuration

- Create `.vscode/launch.json` so the dashboard opens from the `app/` directory and serves `index.html` rather than the folder view.
- Dependencies: the rest of the app content must already be in place to avoid a broken preview.
- Ownership: Coder.

### 6. Validate and verify the integrated result

- Check that the dashboard loads cleanly in the browser preview and that all required fields display.
- Confirm the page looks like Project Pulse, not a generic HTML shell.
- Dependencies: all app files and launch config must be present.
- Ownership: Orchestrator with Planner and Designer review.

## Dependencies between steps

- The project brief and agent definitions establish scope before the dashboard is planned.
- `app/project-data.json` is the dependency for the initial page rendering work.
- `app/index.html` depends on the chosen project-card structure and the data shape.
- `app/styles.css` depends on the final HTML structure and class names.
- `.vscode/launch.json` depends on the completed app so it can reliably open the dashboard preview.
- Validation is the final gate and depends on the working combination of all required files.

## Parallel work

The workflow is mostly sequential, but a few tasks can be parallelized safely:

- The Designer can prepare the visual direction and CSS class structure while the Coder defines the JSON schema, as long as the HTML class names are kept stable.
- The Planner can keep the roadmap and validation checklist updated while the Coder builds the data and markup.
- Orchestrator coordination can happen continuously without blocking the design and implementation work, provided no file scope conflicts are introduced.

## Work that must remain sequential

- Data contract before rendering.
- HTML structure before styling integration.
- Styling before launch preview verification.
- Launch configuration before final browser validation.
- Orchestrator signoff before the dashboard is considered complete.

## Edge cases to handle

- Empty or missing `projects` data.
- Invalid or malformed JSON in `app/project-data.json`.
- Very long project names or owner labels.
- Status values that do not match a known pattern.
- Missing `priority` or `recentActivity` values.
- Browser rendering differences across default desktop widths.
- Launch configuration serving the wrong directory or opening the folder listing instead of `index.html`.

## Validation expectations

The project is ready when all of the following are true:

- `app/project-data.json` parses cleanly and contains a top-level `projects` array.
- `app/index.html` references the stylesheet and renders a dashboard with project cards.
- `app/styles.css` includes clear dashboard and card styling hooks, readable spacing, and visual contrast.
- The dashboard displays status, owner, recent activity, and priority for each project.
- `.vscode/launch.json` exists and opens `index.html` from the `app/` directory.
- The final result matches the brief for a polished, contributor-friendly Project Pulse dashboard.

## Open questions

- None at this stage; the repository brief is sufficiently specific to proceed without assumptions beyond the required app files and launch behavior.
