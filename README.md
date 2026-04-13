[**🌐English**](README_EN.md) | [**🇨🇳中文**](README.md)

# Skills

> AI Agent 的可组合技能集合 -- 安装一个 skill，Agent 就获得对应的专业能力。

这个仓库包含一组独立的、可安装的 Agent skill。每个 skill 是一个自包含的目录，放入你的 Agent 的 skills 文件夹即可使用。

## 包含的 Skills

| Skill | 说明 |
|---|---|
| [learn-from-experience](skills/learn-from-experience/) | 让 Agent 从经验中学习 -- 纠正过的错误不再重犯，好的方法自动沉淀，跨会话同步已确认偏好 |
| [llm-wiki](skills/llm-wiki/) | 基于 Karpathy 的 LLM Wiki 模式，构建和维护持久化、互链的 markdown 知识库 |

## 快速安装

把你需要的 skill 目录复制或软链接到 Agent 的 skills 目录下：

```bash
# 安装 learn-from-experience
cp -r skills/learn-from-experience ~/.claude/skills/learn-from-experience

# 安装 llm-wiki
cp -r skills/llm-wiki ~/.claude/skills/llm-wiki
```

上面以 Claude Code 为例，其他 Agent 替换对应路径即可：

| 产品 | Skills 安装位置 |
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

安装后对 Agent 说：

```text
请初始化 learn-from-experience skill。
```

或：

```text
请初始化 llm-wiki skill。
```

## 仓库结构

```text
skills/
├── learn-from-experience/   # 经验学习 skill
│   ├── SKILL.md             # skill 入口
│   ├── setup.md
│   ├── operations.md
│   ├── memory.md
│   ├── boundaries.md
│   └── ...
└── llm-wiki/                # LLM Wiki skill
    └── SKILL.md             # skill 入口
```

每个 skill 以 `SKILL.md` 作为入口文件，Agent 加载 skill 时首先读取它。

## Community

- **GitHub Issues** — [Submit an issue](https://github.com/shibing624/skills/issues)
- **WeChat Group** — Add WeChat ID `xuming624`, note "nlp", to join the tech group

<img src="https://github.com/shibing624/skills/blob/main/docs/wechat.jpeg" width="200" />

## 许可证

MIT，详见 [`LICENSE`](LICENSE)。
