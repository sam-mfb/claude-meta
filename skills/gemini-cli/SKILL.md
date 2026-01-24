---
name: gemini-cli
description: Use the Gemini CLI to invoke Google's Gemini AI from the command line. Use when you need a second AI opinion, want to verify your work, or need Gemini-specific capabilities.
argument-hint: [prompt]
allowed-tools: Bash, Read
---

# Gemini CLI

Use the `gemini` command to invoke Google's Gemini AI from the command line.

## Prerequisites

The user must have already:
1. Installed Gemini CLI: `npm install -g @google/gemini-cli`
2. Logged in via Google account: run `gemini` and select "Login with Google"
3. Enabled preview features: run `gemini`, then `/settings`, toggle "Preview Features" to true

## Basic Command

Always use the latest preview model with `-m` and non-interactive mode with `-p`:

```bash
gemini -m gemini-3-flash-preview -p "Your prompt here"
```

## Models

| Model | Use Case |
|-------|----------|
| `gemini-3-flash-preview` | Fast, general purpose |
| `gemini-3-pro-preview` | Complex reasoning tasks |

## File References

Use `@` syntax to include files in prompts:

```bash
gemini -m gemini-3-flash-preview -p "Review @./src/main.js"
gemini -m gemini-3-flash-preview -p "Compare @./a.txt and @./b.txt"
```

## Piped Input

```bash
cat file.txt | gemini -m gemini-3-flash-preview -p "Summarize this"
git diff | gemini -m gemini-3-flash-preview -p "Write a commit message"
```

## JSON Output

For programmatic parsing:

```bash
gemini -m gemini-3-flash-preview -p "Query" --output-format json | jq -r '.response'
```

## Key Flags

| Flag | Description |
|------|-------------|
| `-p "prompt"` | Non-interactive mode (required for scripting) |
| `-m model` | Specify model |
| `--output-format json` | Structured JSON output |
| `--yolo` | Auto-approve tool executions (use carefully) |
| `--sandbox` | Run in sandboxed environment |

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 41 | Authentication error |
| 42 | Invalid input |

## When Using This Skill

If `$ARGUMENTS` is provided, construct and run the appropriate gemini command for that prompt.

Otherwise, use Gemini CLI when you need to:
- Get a second opinion on code or analysis
- Verify your own output
- Leverage Gemini's specific strengths
