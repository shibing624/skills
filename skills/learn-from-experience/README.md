[**🌐English**](README_EN.md) | [**🇨🇳中文**](README.md)

# Learn from Experience Skill

> 让 AI Agent 从经验中学习 -- 纠正过的错误不再重犯，好的方法自动沉淀，越用越懂你的一个skill。

`learn-from-experience` 会把纠正、偏好和复盘沉淀成可复用的执行经验。你不需要在每个新会话里反复重申同一套规范，Agent 会保留已确认规则、整理待确认经验，并把长期有效的规则同步到长期记忆（如 Claude Code 的 `CLAUDE.md`）中，适用于 Claude Code、OpenClaw、Codex CLI、OpenCode、Gemini CLI、Agentica、CodeBuddy、Cursor、Windsurf 等 Agent 产品。

## 为什么需要这个Skill

大多数 AI Agent 在真正关键的地方仍然是“失忆”的：

- 你纠正过的问题，下个会话还会重犯
- 你偏好的工作方式，会随着会话结束一起丢失
- 同样的坑，会跨项目、跨工具重复出现

这个仓库的目标，就是让你和 Agent 的协作质量随着使用不断累积，而不是每次重新归零。

## 核心能力

| 能力 | 说明 |
|---|---|
| 更正记录 | 把用户明确纠正和重复失败沉淀为结构化日志 |
| 自我反思 | 将任务后复盘转成候选经验，而不是一次性笔记 |
| 分层记忆 | 高频规则常驻，局部规则按需加载，陈旧规则自动归档 |
| 跨会话同步 | 把已确认偏好编译进 Agent 的全局启动配置 |
| 安全边界 | 明确禁止存储密钥、健康信息、第三方信息和隐藏状态 |
| 多 Agent 适配 | 一套记忆模型，适配多个 Agent 产品 |

## 工作方式

这个仓库本身就是可安装的 skill 目录。安装后，skill 会在 `~/learn-from-experience/` 维护本地记忆空间，并把当前仓库里的这些文件作为行为协议。

```text
纠正 / 复盘
     |
     v
corrections.md
     |
重复模式 + 用户确认
     |
     v
memory.md (HOT)
     |
编译已确认偏好
     |
     v
全局配置: ## Learnings > ### Patterns
     |
     v
新会话启动时自动加载已学习规则
```

三层结构让记忆既有用又可控：

- `HOT`：`memory.md`，存放最稳定、信号最高的规则
- `WARM`：`projects/` 与 `domains/`，存放按项目或领域生效的规则
- `COLD`：`archive/`，存放需要保留审计能力但已不常用的历史记录

## 快速安装

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

# Agentica
cp -r "$(pwd)" ~/.agentica/skills/learn-from-experience
```

然后对 Agent 说：

```text
请初始化 learn-from-experience skill。
```

## 验证安装

预期的首次运行行为：

1. Agent 创建 `~/learn-from-experience/`，包含 `memory.md`、`corrections.md`、`index.md`、`heartbeat-state.md`
2. Agent 确保对应全局配置里存在 `## Learnings > ### Patterns`
3. Agent 能正确响应 `memory stats`、`show my patterns`、`sync memory` 等命令

## 支持平台

| 产品 | 全局配置 | Skill 安装位置 |
|---|---|---|
| Claude Code | `~/.claude/CLAUDE.md` | `~/.claude/skills/learn-from-experience/` |
| OpenClaw | `~/.openclaw/AGENTS.md` | `~/.openclaw/skills/learn-from-experience/` |
| Codex CLI | `~/.codex/AGENTS.md` | 软链接到 `~/.codex/skills/learn-from-experience/` |
| OpenCode | `~/.opencode/AGENTS.md` | 软链接到 `~/.opencode/skills/learn-from-experience/` |
| Gemini CLI | `~/.gemini/AGENTS.md` | 软链接到 `~/.gemini/skills/learn-from-experience/` |
| Agentica | `~/.agentica/AGENTS.md` | `~/.agentica/skills/learn-from-experience/` |
| CodeBuddy | `~/.codebuddy/CODEBUDDY.md` | `~/.codebuddy/skills/learn-from-experience/` |
| Cursor | `.cursor/AGENTS.md` | 软链接到 `.cursor/skills/learn-from-experience/` |
| Windsurf | `.windsurf/AGENTS.md` | 软链接到 `.windsurf/skills/learn-from-experience/` |

## 仓库结构

安装所需的核心文件保留在仓库根目录，这样整个 repo 可以直接作为 skill 目录使用。解释型文档放在 `docs/`。

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

## 文档导航

- [`docs/install.md`](docs/install.md)：完整安装矩阵与初始化说明
- [`docs/architecture.md`](docs/architecture.md)：记忆分层、同步模型与运行时数据流
- [`docs/faq.md`](docs/faq.md)：常见问题、边界情况与卸载说明

## 安全模型

这个项目对“学习什么”采取了刻意保守的策略：

- 绝不存储密码、API Key、令牌、金融信息或健康信息
- 绝不从沉默中推断长期偏好
- 绝不保留会影响行为但用户无法审计的隐藏状态
- 永远以 `memory.md` 作为跨会话同步的唯一真源

更完整的边界规则见 [`boundaries.md`](boundaries.md)，仓库层面的披露规则见 [`SECURITY.md`](SECURITY.md)。

## Community

- **GitHub Issues** — [Submit an issue](https://github.com/shibing624/TreeSearch/issues)
- **WeChat Group** — Add WeChat ID `xuming624`, note "nlp", to join the tech group

<img src="https://github.com/shibing624/TreeSearch/blob/main/docs/wechat.jpeg" width="200" />


## 许可证

MIT，详见 [`LICENSE`](LICENSE)。
