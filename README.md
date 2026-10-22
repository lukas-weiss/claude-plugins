# claude-plugins

Personal [Claude Code](https://claude.com/claude-code) plugin marketplace.

```
/plugin marketplace add lukas-weiss/claude-plugins
```

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

Don't add the checkout as a marketplace (`/plugin marketplace add .`) if you
also use the published one. Both are named `lukas-weiss-plugins`, and Claude
Code allows only one source per marketplace name: adding the second fails with
*"its source doesn't match its extraKnownMarketplaces entry"*. To switch, edit
or remove the `lukas-weiss-plugins` entry under `extraKnownMarketplaces` in
`~/.claude/settings.json`.
