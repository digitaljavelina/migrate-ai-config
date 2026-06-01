# ai-config-tools — Claude Code plugin marketplace

A small marketplace hosting the **`migrate-ai-config`** plugin: an interactive helper that migrates **Claude Code** and **OpenAI Codex** configuration (skills, hooks, plugins, commands, agents, MCP servers, prompts, settings) between **macOS, Windows, and Linux**.

It interviews you for source OS, target OS, and which tools to move, then emits a single-use migration playbook containing only the steps your specific OS pair needs — no manual file copying or guesswork.

## Install

Add this repo as a marketplace, then install the plugin:

```
/plugin marketplace add <git-url-or-local-path>
/plugin install migrate-ai-config@ai-config-tools
```

- **From GitHub:** `/plugin marketplace add your-org/migrate-ai-config`
- **From a local clone:** `/plugin marketplace add /path/to/migrate-ai-config`

Restart Claude Code (or reload) so the new skill is discovered.

## Use

In any session:

```
/migrate-ai-config
```

Answer the four prompts (source OS, target OS, tools, deliverable). The plugin generates the tailored playbook and either writes it to a Markdown file or prints it inline.

## What it does and doesn't touch

- **Migrates** portable config only: settings, skills, hooks, commands, agents, prompts, plugin registry, and your MCP server definitions.
- **Never copies** credentials — it always re-authenticates (`claude` sign-in / `codex login`), because auth is machine-bound (macOS Keychain) or token-based.
- **Reinstalls** plugins rather than copying their platform-specific binaries.
- **Handles cross-OS gotchas** automatically: line-ending conversion (Windows→Unix), the executable bit, `python3`↔`python`, bash-hook interpreters on Windows, and path rewrites.

## Repository layout

```
migrate-ai-config/                       # marketplace repo root
├── .claude-plugin/
│   └── marketplace.json                 # lists the plugin
├── plugins/
│   └── migrate-ai-config/               # the plugin
│       ├── .claude-plugin/
│       │   └── plugin.json              # plugin manifest
│       └── skills/
│           └── migrate-ai-config/
│               └── SKILL.md             # the interactive skill
└── README.md
```

## Before publishing

Edit the `TODO:` author/owner fields in `.claude-plugin/marketplace.json` and `plugins/migrate-ai-config/.claude-plugin/plugin.json`, then push to a git host your team can reach.

## License

MIT
