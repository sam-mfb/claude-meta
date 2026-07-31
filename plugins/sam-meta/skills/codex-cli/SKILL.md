---
name: codex-cli
description: Use OpenAI's Codex CLI to invoke GPT models from the command line. Use when you need a second AI opinion, want to verify your work, or need OpenAI-specific capabilities.
argument-hint: [prompt]
allowed-tools: Bash, Read
---

# Codex CLI

Use the `codex` command to invoke OpenAI's Codex AI from the command line.

## Prerequisites

The user must have already:
1. Installed Codex CLI: `npm install -g @openai/codex`
2. Logged in: run `codex login`

## Basic Command

Use `exec` for non-interactive mode with the latest model:

```bash
codex exec -m gpt-5.2-codex "Your prompt here"
```

## Models

| Model | Use Case |
|-------|----------|
| `gpt-5.2-codex` | Latest, most capable |
| `gpt-5.1-codex-max` | Long-horizon tasks |
| `gpt-5.1-codex-mini` | Faster, cost-effective |

## File References

Use `@` in prompts to include files:

```bash
codex exec -m gpt-5.2-codex "Review @src/main.js"
```

## Piped Input

```bash
cat file.txt | codex exec -m gpt-5.2-codex "Summarize this"
git diff | codex exec -m gpt-5.2-codex "Write a commit message"
echo "your prompt" | codex exec -m gpt-5.2-codex -
```

## JSON Output

For programmatic parsing:

```bash
codex exec -m gpt-5.2-codex --json "Query" | jq
```

## File Output

Write result to file:

```bash
codex exec -m gpt-5.2-codex -o output.md "Generate docs"
```

## Key Flags

| Flag | Description |
|------|-------------|
| `-m model` | Specify model |
| `--json` | Output JSON event stream |
| `-o file` | Write final message to file |
| `--sandbox` | `read-only`, `workspace-write`, or `danger-full-access` |
| `--full-auto` | Auto-approve with workspace-write sandbox |
| `--yolo` | No approvals or sandbox (use carefully) |
| `-i image` | Attach image files |
| `-C path` | Set working directory |

## Sandbox Modes

```bash
# Safe analysis only
codex exec --sandbox read-only -m gpt-5.2-codex "review code"

# Allow file edits
codex exec --sandbox workspace-write -m gpt-5.2-codex "fix linting errors"
```

## Session Resume

Continue a previous conversation:

```bash
codex exec resume --last "follow up question"
```

## Exit Codes

Standard exit codes - 0 for success, non-zero for errors.

## When Using This Skill

If `$ARGUMENTS` is provided, construct and run the appropriate codex command for that prompt.

Otherwise, use Codex CLI when you need to:
- Get a second opinion on code or analysis
- Verify your own output
- Leverage OpenAI's specific strengths
