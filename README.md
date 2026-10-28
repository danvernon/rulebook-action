# Rulebook action

Tests whether coding agents (Claude Code, Codex) follow your repo's written rules (`AGENTS.md`, `CLAUDE.md`, `.cursor/rules`), using the [`rulebook-ai`](https://www.npmjs.com/package/rulebook-ai) CLI. Dashboard: https://rulebookai.vercel.app

The easiest setup is `npx rulebook-ai init-ci` in your repo, which writes the workflow for you. Or add it by hand:

```yaml
- uses: actions/checkout@v4
- uses: danvernon/rulebook-action@v1
  with:
    agents: claude-code
    runs: "2"
    token: ${{ secrets.RULEBOOK_TOKEN }}   # optional: upload to the dashboard
    fail-on-regression: "true"             # optional, needs .rulebook/baseline.json
  env:
    ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
```

It writes the report to the job summary, saves `.rulebook/runs` as an artifact, uploads the report if a token is set, and checks drift if a baseline is committed. It never commits or pushes. Your code stays on the runner; with a token, only the report JSON is uploaded.
