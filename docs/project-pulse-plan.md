# Project Pulse Implementation Plan

## Summary

Build a lightweight static dashboard that helps contributors scan project names, owners, status, recent activity, priority or risk, and a short summary. Use the existing agent workflow: Designer sets the experience direction, Coder implements the assigned files, and Orchestrator coordinates and verifies the integrated result.

## File Ownership

| File | Owner | Assignment |
| --- | --- | --- |
| `app/index.html` | Coder | Semantic dashboard page titled "Project Pulse"; reference the stylesheet and JSON data; render a `.project-card` for each project with its required fields and summary. Include loading, empty, and data-load error states. |
| `app/styles.css` | Designer | Responsive, accessible visual design with clear hierarchy, readable spacing, status and priority treatments, and `.dashboard` and `.project-card` selectors. Include `border-radius` and `box-shadow` styling as expected by the exercise. |
| `app/project-data.json` | Coder | Strict JSON with a top-level `projects` array. Each entry includes `name`, `owner`, `status`, `recentActivity`, and `priority`; include a short summary for the contributor-friendly dashboard copy. |
| `.vscode/launch.json` | Coder | Strict JSON with a "Run Project Pulse Dashboard" configuration. Set `cwd` to `${workspaceFolder}/app`, run `python3 -m http.server 5500`, and use `serverReadyAction` to open `http://localhost:%s/index.html` rather than the directory root. |

## Ordered Phases

1. **Agree on the UI and data contract**
   - **Owner:** Orchestrator, with Designer and Coder input.
   - **Files:** No implementation files.
   - Confirm the project-card fields, loading/empty/error states, and shared CSS hooks before parallel work. Treat sample project records as illustrative unless Mona provides real project data.
   - **Dependency:** This contract unblocks both styling and implementation.

2. **Create independent foundations in parallel**
   - **Designer:** Implement `app/styles.css` against the agreed hooks, including `.dashboard` and `.project-card`; check responsive layout, readable contrast, and keyboard-visible focus treatment.
   - **Coder:** Create `app/project-data.json` and `.vscode/launch.json` within their separate file scopes. Keep both files valid JSON; configure the launch task to serve the `app` directory and open `/index.html` when the server is ready.
   - **Parallel decision:** These assignments can proceed concurrently after Phase 1 because they do not edit the same files. The HTML integration depends on the data shape and CSS hooks being settled.

3. **Implement the dashboard page**
   - **Owner:** Coder.
   - **File:** `app/index.html`.
   - Reference `styles.css` and `project-data.json`, load the data, and render each record with its name, owner, status, `recentActivity`, priority, and summary. Keep markup semantic and handle loading, empty, and failed data loads.
   - **Dependency:** Requires Phase 1's contract and Phase 2's data fields and CSS hooks; keep this phase sequential after those interfaces are stable.

4. **Integrate and validate**
   - **Owner:** Orchestrator, with Designer and Coder addressing findings in their assigned files.
   - **Files:** All four deliverables, respecting the ownership table.
   - Check the static app, launch configuration, accessibility, and visual behavior together. Resolve integration issues before handoff.
   - **Dependency:** Runs after Phases 2 and 3.

## Dependencies and Parallel Work

The design/data contract must come first. After that, Designer can work on `app/styles.css` while Coder creates `app/project-data.json` and `.vscode/launch.json`; these three separate-file assignments can run in parallel. Coder should complete `app/index.html` only once the data schema and class hooks are fixed. Runtime and visual integration checks are sequential and happen after all deliverables exist. Keep file ownership separate; route any cross-file changes through the Orchestrator.

## Edge Cases

- No projects in the `projects` array: show a useful empty state.
- JSON fetch failure or malformed data: show a clear error instead of a blank dashboard.
- Unexpected status or priority values: keep the content readable and avoid relying on color alone.
- Long project names, activity text, or summaries: ensure cards remain readable at narrow widths.
- Launch opens the directory listing instead of the dashboard: verify the URL ends in `/index.html` and the server working directory is `app/`.
- No real project records are specified in the brief: use clearly illustrative sample content or confirm the source data with Mona.

## Validation Expectations

Run the exercise repository check and syntax checks from the repository root:

```bash
bash scripts/validate-exercise.sh
python3 -m json.tool app/project-data.json >/dev/null
python3 -m json.tool .vscode/launch.json >/dev/null
```

Confirm the plan names Project Pulse, Designer, Coder, all four file assignments, dependencies, parallel work decisions, and validation. The Step 2 workflow checks these plan phrases. The Step 3 workflow checks implementation file presence, required keyphrases, and JSON syntax; neither workflow runs the app.

For a runtime smoke test, start the server with `python3 -m http.server 5500 --directory app` and confirm `http://localhost:5500/index.html` serves the dashboard page. Then run **Run Project Pulse Dashboard** from VS Code and verify that project cards populate. Manually check a narrow viewport, keyboard navigation, visible focus, and the empty/error states. `bash scripts/validate-exercise.sh` checks exercise-repository conventions, not dashboard runtime behavior.

## Open Questions

- Should the dashboard use real Mona team projects, or are representative sample records acceptable?
- Is there a preferred visual style or project-status vocabulary beyond the brief?