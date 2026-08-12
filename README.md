# claude-meta

Personal Claude Code marketplace and global configs.

## Layout

```
.claude-plugin/marketplace.json   # marketplace manifest (this repo is a marketplace)
plugins/sam-meta/                 # the plugin: skills + agents
  .claude-plugin/plugin.json
  skills/                         # model-invoked skills (also usable as /slash commands)
  agents/                         # custom subagents
general/settings.json             # user-level ~/.claude/settings.json
```

## Installation

Skills and agents install as a plugin:

```bash
claude plugin marketplace add sam-mfb/claude-meta
claude plugin install sam-meta@claude-meta
```

Restart Claude Code to load it. To update later:

```bash
claude plugin marketplace update claude-meta
claude plugin update sam-meta
```

Global settings are not something a plugin can write, so they are copied
separately. `update-claude-meta.sh` in the `docker-dev` repo does both steps,
and runs during the Docker build.

## Working on the plugin

```bash
claude plugin validate .                    # marketplace manifest
claude plugin validate plugins/sam-meta     # plugin manifest
claude plugin details sam-meta              # component inventory + token cost
```

The plugin `version` must go up whenever plugin contents change, or
`claude plugin update` has nothing to move to. A git hook does this
automatically. Turn it on once per clone:

```bash
git config core.hooksPath .githooks
```

Any commit that touches `plugins/<name>/` bumps that plugin's patch version and
stages the change. If you edit the version yourself in the same commit, the hook
leaves it alone, so minor and major bumps still work. Commits that touch only
the README, the marketplace manifest, or `general/` do not bump anything.

**Note:** `general/settings.json` is copied over `~/.claude/settings.json`
wholesale, so it must hold the complete desired set of user settings — anything
missing here gets removed on the next run.
