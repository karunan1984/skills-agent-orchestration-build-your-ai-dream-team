# Project Pulse implementation plan

## Goal and constraints

Build a static HTML/CSS/JSON project dashboard titled **Project Pulse**. Do not add a framework, build system, or dependency. Keep the implementation within these four paths:

- `app/index.html`
- `app/styles.css`
- `app/project-data.json`
- `.vscode/launch.json`

## Ownership and implementation

Before parallel work begins, Designer and Coder agree on the data schema, markup structure, and CSS/markup hooks. At minimum, the shared hooks are `.dashboard` for the dashboard container and `.project-card` for each project card.

After that agreement, work can proceed in parallel:

- **Designer** owns `app/styles.css` and implements visual hierarchy, visual treatments, accessibility, and responsive layout against the agreed markup and hooks.
- **Coder** owns `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`. The HTML loads the JSON and renders the dashboard; use safe text rendering (such as `textContent`, not interpolated HTML) for project values.

Use a top-level `projects` array in the JSON. Each project has `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`. Include multiple entries. Use clearly labeled placeholder projects if real Mona project data is unavailable; do not present placeholders as real project data.

Configure the VS Code launch entry with the name **Run Project Pulse Dashboard**. It runs `python3 -m http.server 5500` with cwd `${workspaceFolder}/app` and opens `/index.html` in a browser.

## Dependency sequence and integration

1. Review available project guidance and determine whether real Mona project data is available; record any placeholders clearly.
2. Agree on the JSON schema, markup structure, empty/error states, and `.dashboard` / `.project-card` hooks. This is a prerequisite for parallel implementation.
3. Implement Designer and Coder work in parallel within their assigned files.
4. Integrate sequentially: check that the markup uses the agreed hooks and the stylesheet covers them; verify JSON fields and loading/error/empty behavior; resolve mismatches before testing.
5. Run validation and the browser smoke tests below, addressing failures before completion.

The data contract and hooks are shared dependencies; Designer and Coder must not independently redefine them during parallel work.

## Validation expectations

- Strictly parse `app/project-data.json` and `.vscode/launch.json` as JSON; keep the launch configuration free of JSONC comments and trailing commas.
- Check that all four expected paths exist and contain the expected content, including the page title, required schema fields, CSS hooks, and launch command/cwd/browser URL.
- Run **Run Project Pulse Dashboard** from VS Code and smoke-test the page in a browser with multiple cards.
- Exercise empty-data and JSON load/error cases and confirm each has a clear, usable message rather than a blank or broken dashboard.
- Check responsive behavior, accessible semantic structure and labels, and browser console/network output for errors or failed requests.
- Run existing exercise validation if available.

## Edge cases to cover

- Empty or missing `projects` array.
- Malformed JSON, failed fetch, or unavailable data file.
- Missing or empty field values; render safely and avoid exposing markup from data as HTML.
- Long names, summaries, or activity text, including narrow viewports and multiple cards.
- Placeholder data must remain clearly identified.

## Open questions

- Is real Mona project data available, and what source is authoritative? If not, which clearly labeled placeholders should be used?
- What status and priority values or conventions should the data use?
- Should empty and load-error states share presentation, or have distinct messages?
