# claude-plugins

Personal [Claude Code](https://claude.com/claude-code) plugin marketplace.

```
/plugin marketplace add lukas-weiss/claude-plugins
```

## Why a marketplace

Claude Code installs plugins only from marketplaces, so this repo is one. That
way the plugins are available right away and an update ships with a push to
`main`, without waiting for a review.

A plugin may also be submitted to Anthropic's plugin directory
(`claude-plugins-official`). If it is accepted, you can install it from there
instead; this repo stays its source.

## Plugins

| Plugin                                    | What it does                                                        |
| ----------------------------------------- | ------------------------------------------------------------------- |
| [`gha-readonly`](plugins/gha-readonly/)   | Read-only GitHub Actions access, e.g. to check CI before merging    |

## Layout

```
.claude-plugin/marketplace.json   lists the plugins below
plugins/<name>/                   one directory per plugin
  .claude-plugin/plugin.json      name, version, description
  ...                             whatever the plugin ships (.mcp.json, skills, …)
```

## Development

Validate after a change:

```
claude plugin validate .
claude plugin validate plugins/<name>
```

Try a plugin from the working tree, for one session only:

```
claude --plugin-dir plugins/<name>
```

Disable the installed copy (`/plugin`) while doing this, or its tools show up
twice.

The checkout and the published repo are the same marketplace,
`lukas-weiss-plugins`, and Claude Code keeps one source per name. Running
`/plugin marketplace add` with the other source switches it over, and
installed plugins then update from there. If `~/.claude/settings.json` pins a
source under `extraKnownMarketplaces`, switching fails with *"its source
doesn't match its extraKnownMarketplaces entry"*; change or remove that entry
first.
