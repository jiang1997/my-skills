# My Skills — Claude Code Plugins

A collection of Claude Code plugins.

## Plugins

| Plugin | Description |
|--------|-------------|
| `jules-cli` | Delegate coding tasks to Google Jules CLI and review results |

## Installation

### Via Marketplace

```bash
/plugin marketplace add <OWNER>/<REPO>
/plugin install jules-cli@my-skills
```

> Replace `<OWNER>/<REPO>` with your actual GitHub owner and repository name.

### Local Development

```bash
claude --plugin-dir ./jules-cli
```

Then invoke with:

```
/jules-cli:jules-cli
```

## Plugin Structure

```
.
├── .claude-plugin/
│   └── marketplace.json      # Marketplace catalog
├── jules-cli/                # Plugin: jules-cli
│   ├── .claude-plugin/
│   │   └── plugin.json       # Plugin manifest
│   └── skills/
│       └── jules-cli/
│           └── SKILL.md      # Skill definition
└── README.md
```
