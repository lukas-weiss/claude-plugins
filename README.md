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

Validate after a change:

```
claude plugin validate .
claude plugin validate plugins/<name>
```
