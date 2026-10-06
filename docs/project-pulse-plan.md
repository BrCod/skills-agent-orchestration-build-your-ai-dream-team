# Project Pulse dashboard implementation plan

## Goal

Build Mona's lightweight, static Project Pulse dashboard so contributors can quickly see active projects, owners, current status, recent activity, priority or risk, and a short contributor-friendly summary. The finished dashboard should have an accessible, responsive, polished card layout and a VS Code launch configuration that opens the dashboard UI.

## Responsibilities and file assignments

| Agent | Responsibility | Assigned files |
| --- | --- | --- |
| Planner | Research repository requirements and edge cases, define phases and file ownership, and document dependencies and validation expectations. | `docs/project-pulse-plan.md` |
| Designer | Define and implement the visual hierarchy, accessible presentation, responsive behavior, and polished card styling. Coordinate CSS hooks with the HTML structure. | `app/styles.css` |
| Coder | Implement semantic dashboard markup, load and render project data, provide representative data, configure the runnable preview, and fix implementation issues found during integration. | `app/index.html`, `app/project-data.json`, `.vscode/launch.json` |
| Orchestrator | Assign the scoped work, give both specialists the shared markup/data/CSS contract, sequence integration, and verify the combined result. | No implementation files; coordinate and review the assigned outputs. |

## Implementation phases

1. **Confirm the interface contract.** The Orchestrator gives Designer and Coder the same requirements: use `.dashboard` for the main dashboard and `.project-card` for each project; render a top-level `projects` array from JSON; include `name`, `owner`, `status`, `recentActivity`, and `priority` on every project, plus a short `summary` for the contributor-friendly description. The page title must be exactly `Project Pulse`.
2. **Build the dashboard outputs.** Designer creates responsive, accessible styling in `app/styles.css`. Coder creates `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`. The HTML must link to `styles.css`, load `project-data.json`, and visibly render each project's name, owner, status, recent activity, priority, and summary. The launch configuration must be strict JSON, named `Run Project Pulse Dashboard`, run `python3 -m http.server 5500` from `${workspaceFolder}/app`, and open `http://localhost:%s/index.html` using `serverReadyAction`.
3. **Integrate and validate.** After both assignments are complete, the Orchestrator checks the shared selectors and data contract, reviews the UI at desktop and narrow viewport sizes, runs the static checks, and launches the preview. Designer and Coder make any scoped corrections identified by that review.

## Dependencies and parallel work

- Phase 1 is a prerequisite for implementation: the HTML/CSS hooks and JSON fields need to be agreed before the agents work independently.
- In Phase 2, Designer's stylesheet and Coder's HTML, data, and launch configuration can proceed in parallel because their file assignments do not overlap. This is safe only if both follow the shared `.dashboard` / `.project-card` and project-data contract established in Phase 1.
- Within Coder's assignment, the HTML and data are coupled by the JSON field names and rendering behavior; implement them against the same contract. The launch configuration can be prepared alongside them, but its final preview check depends on all app files being in place.
- Phase 3 must run after both Phase 2 assignments finish. Integration findings may require a short sequential handoff if HTML/CSS hooks or data rendering need to be reconciled.

## Validation expectations

- Confirm all four assigned deliverables exist: `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`.
- Parse `app/project-data.json` and `.vscode/launch.json` as JSON. Check that project data has a top-level `projects` array and each entry provides `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
- Review `app/index.html` for the exact `Project Pulse` title, the stylesheet and JSON references, semantic/accessibility basics, and visible `.project-card` elements populated with the project fields.
- Review `app/styles.css` for `.dashboard` and `.project-card`, readable status and priority treatments, `border-radius`, `box-shadow`, and responsive layout rules. Check keyboard and screen-reader access to meaningful content and controls, if any.
- Start **Run Project Pulse Dashboard** from VS Code. Confirm the server uses `app/` as its working directory and the browser opens `http://localhost:5500/index.html` showing the dashboard rather than a directory listing. Check the console/network for failed data or stylesheet loads and confirm the layout remains readable on a narrow viewport.
- No package installation or build step is expected for this static app; validate using the existing browser preview and JSON parsing tools.

## Edge cases and open questions

- Ensure JSON loading works through the HTTP server used by the launch configuration; testing by opening the HTML directly as a `file://` URL may block `fetch`.
- If the project array is empty or data fails to load, avoid leaving a confusing blank dashboard; show a clear empty or load-error state.
- Keep status and priority visually distinguishable without relying on color alone.
- The brief does not prescribe project names, status/priority vocabularies, or exact summary wording. Use a small, representative contributor-friendly sample set and apply consistent labels.
