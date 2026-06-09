# AGENTS.md

Guidance for AI agents working in this repository.

## Project overview

Static **Bryan's Command Center** dashboard (`command-center/`) plus JSON brief templates (`briefs/`). No backend, build step, or package manager.

## Cursor Cloud specific instructions

### Dependencies

There are **no installable dependencies** (no `package.json`, `requirements.txt`, or Docker). Python 3 (stdlib `http.server`) is sufficient to serve the site locally.

### Running the Command Center

Start a static HTTP server from the `command-center` directory (preferred over `file://` for consistent asset loading):

```bash
python3 -m http.server 8080
```

Run from `command-center/` so relative paths resolve correctly. Open http://localhost:8080 in a browser.

For background/long-running use, start the server in tmux rather than a one-shot shell.

### Brief JSON files

Brief templates live in `briefs/`:

- `briefs/brian-calendar-quick-questions.json` — calendar planning questionnaire
- `briefs/carb-testing-email-draft.json` — NorCal Carb email campaign draft

Validate JSON syntax:

```bash
python3 -m json.tool briefs/brian-calendar-quick-questions.json > /dev/null
python3 -m json.tool briefs/carb-testing-email-draft.json > /dev/null
```

The dashboard **Daily Brief** button currently shows an alert pointing at the calendar brief path; it does not load the JSON in-browser yet.

### Lint / test / build

This repo has **no** ESLint, Prettier, test runner, or build pipeline. Verification is manual (browser) or HTTP checks on static assets.

### External integrations (not in repo)

Silverback AI, NorCal Carb Mobile, Notion, and Squarespace are referenced in UI copy and briefs but are **not wired** in code. Dashboard data comes from mock data in `command-center/data.js`.
