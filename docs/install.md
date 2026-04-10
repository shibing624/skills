# Installation Guide

This repository is designed so that the repository itself can be used as the installed skill directory.

## General Pattern

1. Clone this repository somewhere on your machine
2. Copy or symlink the repository into the correct skills directory for your agent product
3. Start a new agent session
4. Ask the agent to initialize `learn-from-experience`

## Platform Matrix

| Product | Global Config | Skill Installation |
|---|---|---|
| Claude Code | `~/.claude/CLAUDE.md` | `~/.claude/skills/learn-from-experience/` |
| OpenClaw | `~/.openclaw/AGENTS.md` | `~/.openclaw/skills/learn-from-experience/` |
| Codex CLI | `~/.codex/AGENTS.md` | symlink to `~/.codex/skills/learn-from-experience/` |
| OpenCode | `~/.opencode/AGENTS.md` | symlink to `~/.opencode/skills/learn-from-experience/` |
| Gemini CLI | `~/.gemini/AGENTS.md` | symlink to `~/.gemini/skills/learn-from-experience/` |
| CodeBuddy | `~/.codebuddy/CODEBUDDY.md` | `~/.codebuddy/skills/learn-from-experience/` |
| Cursor | `.cursor/AGENTS.md` | symlink to `.cursor/skills/learn-from-experience/` |
| Windsurf | `.windsurf/AGENTS.md` | symlink to `.windsurf/skills/learn-from-experience/` |

## Example Commands

Replace the path source with the absolute path to your local clone. If you are currently in the repository root, `$(pwd)` is fine.

### Claude Code

```bash
cp -r "$(pwd)" ~/.claude/skills/learn-from-experience
```

### OpenClaw

```bash
cp -r "$(pwd)" ~/.openclaw/skills/learn-from-experience
```

### Codex CLI

```bash
ln -sf "$(pwd)" ~/.codex/skills/learn-from-experience
```

### OpenCode

```bash
ln -sf "$(pwd)" ~/.opencode/skills/learn-from-experience
```

### Gemini CLI

```bash
ln -sf "$(pwd)" ~/.gemini/skills/learn-from-experience
```

### CodeBuddy

```bash
cp -r "$(pwd)" ~/.codebuddy/skills/learn-from-experience
```

### Cursor

```bash
ln -sf "/absolute/path/to/learn-from-experience" "/path/to/workspace/.cursor/skills/learn-from-experience"
```

### Windsurf

```bash
ln -sf "/absolute/path/to/learn-from-experience" "/path/to/workspace/.windsurf/skills/learn-from-experience"
```

## First Initialization Prompt

Use either language:

```text
Please initialize the learn-from-experience skill.
请初始化 learn-from-experience skill。
```

## Expected Initialization Effects

- Create `~/learn-from-experience/`
- Create `memory.md`, `index.md`, `corrections.md`, and `heartbeat-state.md`
- Ensure `## Learnings > ### Patterns` exists in the relevant global config
- Optionally add workspace integration snippets such as `HEARTBEAT.md`

## Optional Installation Route

If your environment supports ClawHub:

```bash
clawhub install learn-from-experience
```

Use the repository install flow when you want a transparent local copy you can inspect and modify.
