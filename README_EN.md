[**🌐English**](README_EN.md) | [**🇨🇳中文**](README.md)

# Learn from Experience

> Let AI Agent learn from experience -- correct mistakes once, forget them never. Good methods auto-accumulate, and the more you use it, the more it understands you.

`learn-from-experience` turns corrections, preferences, and self-reflection into reusable operational memory. Instead of re-teaching your agent the same lessons every session, you let it retain what was confirmed, organize what is still tentative, and sync durable rules into the agent's global config (like `CLAUDE.md` for Claude Code).

## Why This Skill Exists

Most AI agents are stateless where it matters:

- They forget the mistakes you already corrected
- They lose your preferred workflow when the session ends
- They repeat avoidable behavior across tools and projects

This skill exists to make agent collaboration compound over time instead of resetting to zero.

## Core Capabilities

| Capability | Description |
|---|---|
| Correction logging | Capture explicit user corrections and repeated failures in a structured log |
| Self-reflection | Turn post-task evaluation into candidate lessons instead of one-off notes |
| Tiered memory | Keep high-signal rules hot, scoped rules warm, and stale rules archived |
| Cross-session sync | Compile confirmed preferences into the agent's global startup config |
| Safety boundaries | Explicitly avoid credentials, health data, third-party data, and hidden state |
| Agent-agnostic design | One memory model, multiple agent products |

## How It Works

The repository itself is the installable skill directory. After installation, the skill maintains a local memory store in `~/learn-from-experience/` and uses the repository files here as its behavioral contract.

```text
correction / reflection
        |
        v
  corrections.md
        |
 repeated pattern + user confirmation
        |
        v
   memory.md (HOT)
        |
 compile confirmed preferences
        |
        v
agent global config: ## Learnings > ### Patterns
        |
        v
new sessions start with the learned rules loaded
```

Three storage tiers keep the memory set useful and bounded:

- `HOT`: `memory.md` for the most durable, highest-signal preferences
- `WARM`: `projects/` and `domains/` for scoped patterns
- `COLD`: `archive/` for inactive history that should stay auditable

## Quick Install

Full platform-specific instructions live in [`docs/install.md`](docs/install.md). The common pattern is: place or link this repository into your agent's skills directory, then ask the agent to initialize the skill.

```bash
# Claude Code
cp -r "$(pwd)" ~/.claude/skills/learn-from-experience

# Codex CLI
ln -sf "$(pwd)" ~/.codex/skills/learn-from-experience

# OpenCode
ln -sf "$(pwd)" ~/.opencode/skills/learn-from-experience

# Gemini CLI
ln -sf "$(pwd)" ~/.gemini/skills/learn-from-experience
```

Then tell your agent:

```text
Please initialize the learn-from-experience skill.
```

## Verify Installation

Expected first-run behavior:

1. The agent creates `~/learn-from-experience/` with `memory.md`, `corrections.md`, `index.md`, and `heartbeat-state.md`
2. The agent ensures `## Learnings > ### Patterns` exists in the relevant global config
3. The agent can answer commands like `memory stats`, `show my patterns`, or `sync memory`

## Supported Platforms

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

## Repository Layout

Install-critical files stay at the repository root so the repo can be used directly as the skill directory. Explanatory material lives under `docs/`.

```text
learn-from-experience/
├── SKILL.md
├── setup.md
├── operations.md
├── learning.md
├── scaling.md
├── boundaries.md
├── heartbeat-rules.md
├── docs/
```

## Documentation

- [`docs/install.md`](docs/install.md): full installation matrix and setup notes
- [`docs/architecture.md`](docs/architecture.md): memory tiers, sync model, and runtime data flow
- [`docs/faq.md`](docs/faq.md): common questions, edge cases, and uninstall guidance

## Safety Model

This project is intentionally conservative about what it learns:

- Never store passwords, API keys, tokens, banking data, or health data
- Never infer durable preferences from silence
- Never keep hidden state that changes behavior without being inspectable
- Always keep `memory.md` as the source of truth for cross-session sync

Detailed rules live in [`boundaries.md`](boundaries.md), and repository-level disclosure guidance lives in [`SECURITY.md`](SECURITY.md).

## Community

- **GitHub Issues** — [Submit an issue](https://github.com/shibing624/TreeSearch/issues)
- **WeChat Group** — Add WeChat ID `xuming624`, note "nlp", to join the tech group

<img src="https://github.com/shibing624/TreeSearch/blob/main/docs/wechat.jpeg" width="200" />

## Contributing

Contributions are welcome, especially in three areas:

- platform-specific install/setup validation
- tighter safety and transparency rules
- better examples for real-world agent workflows

Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) before opening a pull request.

## License

MIT. See [`LICENSE`](LICENSE).
