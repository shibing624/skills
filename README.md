# Learn from Experience

> Durable execution memory for coding agents.  
> 为编码 Agent 提供可持续积累的执行记忆。

`learn-from-experience` turns corrections, preferences, and self-reflection into reusable operational memory. Instead of re-teaching your agent the same lessons every session, you let it retain what was confirmed, organize what is still tentative, and sync durable rules into the agent's startup config.

`learn-from-experience` 会把纠正、偏好和复盘沉淀成可复用的执行经验。你不需要在每个新会话里反复重申同一套规范，Agent 会保留已确认规则、整理待确认经验，并把长期有效的规则同步到启动配置中。

## Why It Exists / 为什么存在

Most coding agents are stateless where it matters:

- They forget the mistakes you already corrected.
- They lose your preferred workflow when the session ends.
- They repeat avoidable behavior across tools and projects.

大多数编码 Agent 在真正关键的地方仍然是“失忆”的：

- 你纠正过的问题，下个会话还会重犯。
- 你偏好的工作方式，会随着会话结束一起丢失。
- 同样的坑，会跨项目、跨工具重复出现。

This repository exists to make agent collaboration compound over time instead of resetting to zero.

这个仓库的目标，就是让你和 Agent 的协作质量随着使用不断累积，而不是每次重新归零。

## What It Does / 核心能力

| Capability | Description |
|---|---|
| Correction logging | Capture explicit user corrections and repeated failures in a structured log |
| Self-reflection | Turn post-task evaluation into candidate lessons instead of one-off notes |
| Tiered memory | Keep high-signal rules hot, scoped rules warm, and stale rules archived |
| Cross-session sync | Compile confirmed preferences into the agent's global startup config |
| Safety boundaries | Explicitly avoid credentials, health data, third-party data, and hidden state |
| Agent-agnostic design | One memory model, multiple agent products |

| 能力 | 说明 |
|---|---|
| 更正记录 | 把用户明确纠正和重复失败沉淀为结构化日志 |
| 自我反思 | 将任务后复盘转成候选经验，而不是一次性笔记 |
| 分层记忆 | 高频规则常驻，局部规则按需加载，陈旧规则自动归档 |
| 跨会话同步 | 把已确认偏好编译进 Agent 的全局启动配置 |
| 安全边界 | 明确禁止存储密钥、健康信息、第三方信息和隐藏状态 |
| 多 Agent 适配 | 一套记忆模型，适配多个 Agent 产品 |

## How It Works / 工作方式

The repository itself is the installable skill directory. After installation, the skill maintains a local memory store in `~/learn-from-experience/` and uses the repository files here as its behavioral contract.

这个仓库本身就是可安装的 skill 目录。安装后，skill 会在 `~/learn-from-experience/` 维护本地记忆空间，并把当前仓库里的这些文件作为行为协议。

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

三层结构让记忆既有用又可控：

- `HOT`：`memory.md`，存放最稳定、信号最高的规则
- `WARM`：`projects/` 与 `domains/`，存放按项目或领域生效的规则
- `COLD`：`archive/`，存放需要保留审计能力但已不常用的历史记录

## Quick Install / 快速安装

Full platform-specific instructions live in [`docs/install.md`](docs/install.md). The common pattern is: place or link this repository into your agent's skills directory, then ask the agent to initialize the skill.

完整的多平台安装说明见 [`docs/install.md`](docs/install.md)。通用思路是：把整个仓库复制或软链接到对应的 skills 目录，然后让 Agent 初始化该 skill。

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

然后对 Agent 说：

```text
Please initialize the learn-from-experience skill.
请初始化 learn-from-experience skill。
```

## Verify Installation / 验证安装

Expected first-run behavior:

预期的首次运行行为：

1. The agent creates `~/learn-from-experience/` with `memory.md`, `corrections.md`, `index.md`, and `heartbeat-state.md`.
2. The agent ensures `## Learnings > ### Patterns` exists in the relevant global config.
3. The agent can answer commands like `memory stats`, `show my patterns`, or `sync memory`.

1. Agent 创建 `~/learn-from-experience/`，包含 `memory.md`、`corrections.md`、`index.md`、`heartbeat-state.md`。
2. Agent 确保对应全局配置里存在 `## Learnings > ### Patterns`。
3. Agent 能正确响应 `memory stats`、`show my patterns`、`sync memory` 等命令。

## Supported Platforms / 支持平台

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

## Repository Layout / 仓库结构

Install-critical files stay at the repository root so the repo can be used directly as the skill directory. Explanatory material lives under `docs/`, and examples live under `examples/`.

安装所需的核心文件保留在仓库根目录，这样整个 repo 可以直接作为 skill 目录使用。解释型文档放在 `docs/`，示例放在 `examples/`。

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
├── examples/
└── .github/
```

## Documentation / 文档导航

- [`docs/install.md`](docs/install.md): full installation matrix and setup notes
- [`docs/architecture.md`](docs/architecture.md): memory tiers, sync model, and runtime data flow
- [`docs/faq.md`](docs/faq.md): common questions, edge cases, and uninstall guidance
- [`examples/quickstart.md`](examples/quickstart.md): what a first successful run looks like
- [`CONTRIBUTING.md`](CONTRIBUTING.md): contribution and repo maintenance expectations

## Safety Model / 安全模型

This project is intentionally conservative about what it learns.

这个项目对“学习什么”采取了刻意保守的策略。

- Never store passwords, API keys, tokens, banking data, or health data
- Never infer durable preferences from silence
- Never keep hidden state that changes behavior without being inspectable
- Always keep `memory.md` as the source of truth for cross-session sync

- 绝不存储密码、API Key、令牌、金融信息或健康信息
- 绝不从沉默中推断长期偏好
- 绝不保留会影响行为但用户无法审计的隐藏状态
- 永远以 `memory.md` 作为跨会话同步的唯一真源

Detailed rules live in [`boundaries.md`](boundaries.md), and repository-level disclosure guidance lives in [`SECURITY.md`](SECURITY.md).

更完整的边界规则见 [`boundaries.md`](boundaries.md)。

## Contributing / 贡献

Contributions are welcome, especially in three areas:

- platform-specific install/setup validation
- tighter safety and transparency rules
- better examples for real-world agent workflows

欢迎贡献，尤其是这三类内容：

- 多平台安装与初始化验证
- 更严格的安全和透明度规则
- 更贴近真实工作流的使用示例

Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) before opening a pull request.

提交 PR 前请先阅读 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

## License / 许可证

MIT. See [`LICENSE`](LICENSE).
