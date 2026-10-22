# gha-readonly

Read-only access to GitHub Actions for Claude Code — workflow runs, jobs and
logs — so Claude can check that CI passed before it merges a pull request.

> **Unofficial.** Not affiliated with GitHub or Anthropic. This plugin only
> points Claude Code at GitHub's own MCP server with a different toolset.

## Why

The official `github` plugin from `claude-plugins-official` connects to
GitHub's MCP server without selecting toolsets, so it only gets the defaults
(repos, issues, pull requests, users, context). **Actions is not among them.**
And with a fine-grained personal access token, the check-runs endpoint returns
`403`, because fine-grained tokens have no "Checks" permission.

This plugin adds a second connection that loads only the Actions toolset, in
read-only mode. It complements the official plugin; it does not replace it.

## What it configures

One HTTP MCP server, `actions`:

```
https://api.githubcopilot.com/mcp/x/actions/readonly
```

- `/x/actions` — only the Actions toolset
- `/readonly` — only tools that read; nothing can start, re-run or cancel a
  workflow

Its tools show up as `mcp__plugin_gha-readonly_actions__*`.

## Requirements

- The environment variable `GITHUB_PERSONAL_ACCESS_TOKEN` — the same one the
  official `github` plugin uses.
- For a fine-grained token: repository permission **Actions: Read-only**.
  Nothing else is needed — not "Workflows" (that only allows editing
  `.github/workflows/`), not "Commit statuses" (Actions reports check runs,
  not commit statuses), and no write access.

## Install

```
/plugin marketplace add lukas-weiss/claude-plugins
/plugin install gha-readonly@lukas-weiss-plugins
```

To work on the plugin itself, see [Development](../../README.md#development).

If you had added the same server by hand (`claude mcp add … github-actions`),
remove that entry so the tools don't appear twice:

```
claude mcp remove github-actions --scope user
```

## Privacy

The plugin ships no code and collects nothing. Claude Code talks directly to
GitHub's MCP server with your token, so
[GitHub's privacy statement](https://docs.github.com/site-policy/privacy-policies/github-general-privacy-statement)
applies.

## When to drop it

If the official `github` plugin starts loading the Actions toolset, or lets
you choose toolsets, this plugin is redundant — uninstall it. That change is
proposed in
[anthropics/claude-plugins-official#6859](https://github.com/anthropics/claude-plugins-official/issues/6859).
