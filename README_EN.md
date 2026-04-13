[**🌐English**](README_EN.md) | [**🇨🇳中文**](README.md)

# Skills

> Composable skills for AI Agents -- install a skill, and the agent gains that expertise.

This repository contains a collection of independent, installable Agent skills. Each skill is a self-contained directory that you drop into your agent's skills folder.

## Included Skills

| Skill | Description |
|---|---|
| [learn-from-experience](skills/learn-from-experience/) | Let agents learn from experience -- mistakes corrected once are never repeated, good methods auto-accumulate, confirmed preferences sync across sessions |
| [llm-wiki](skills/llm-wiki/) | Build and maintain a persistent, interlinked markdown knowledge base based on Karpathy's LLM Wiki pattern |

## Quick Install

Copy or symlink the skill directory you need into your agent's skills folder:

```bash
# Install learn-from-experience
cp -r skills/learn-from-experience ~/.claude/skills/learn-from-experience

# Install llm-wiki
cp -r skills/llm-wiki ~/.claude/skills/llm-wiki
```

The example above uses Claude Code. For other agents, replace the path accordingly:

| Product | Skills Install Path |
|---|---|
| Claude Code | `~/.claude/skills/` |
| OpenClaw | `~/.openclaw/skills/` |
| Codex CLI | `~/.codex/skills/` |
| OpenCode | `~/.opencode/skills/` |
| Gemini CLI | `~/.gemini/skills/` |
| Agentica | `~/.agentica/skills/` |
| CodeBuddy | `~/.codebuddy/skills/` |
| Cursor | `.cursor/skills/` |
| Windsurf | `.windsurf/skills/` |

After installation, tell your agent:

```text
Please initialize the learn-from-experience skill.
```

Or:

```text
Please initialize the llm-wiki skill.
```

## Repository Layout

```text
skills/
├── learn-from-experience/   # Experience learning skill
│   ├── SKILL.md             # Skill entry point
│   ├── setup.md
│   ├── operations.md
│   ├── memory.md
│   ├── boundaries.md
│   └── ...
└── llm-wiki/                # LLM Wiki skill
    └── SKILL.md             # Skill entry point
```

Each skill uses `SKILL.md` as its entry point -- the agent reads it first when loading the skill.

## Community

- **GitHub Issues** — [Submit an issue](https://github.com/shibing624/skills/issues)
- **WeChat Group** — Add WeChat ID `xuming624`, note "nlp", to join the tech group

<img src="https://github.com/shibing624/TreeSearch/blob/main/docs/wechat.jpeg" width="200" />

## License

MIT. See [`LICENSE`](LICENSE).
