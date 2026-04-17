# LLM Wiki Skill

> 把零散资料沉淀为可持续维护、可交叉引用、可持续扩展的 Markdown 知识库。

`llm-wiki` 是一个面向 Agent 的知识库工作流 skill，灵感来自 Andrej Karpathy 的 LLM Wiki 模式。它不是传统的“每次查询都重新检索一次”的 RAG，而是把信息整理成长期存在的 wiki：资料先被摄取，再被归纳、交叉链接、持续更新，后续查询直接基于已经编译好的知识网络完成。

## 适用场景

当你希望 Agent 帮你做下面这些事情时，这个 skill 很适合：

- 建一个长期维护的研究型知识库
- 把网页、论文、访谈、会议纪要等资料沉淀进 wiki
- 在已有 wiki 上持续补充、更新和交叉引用内容
- 对 wiki 做一致性检查、结构审计和健康检查
- 在研究过程中把一次性问答沉淀成可复用页面

## 核心思路

普通 RAG 更像“每次临时找资料”；`llm-wiki` 更像“持续建设一套自己的知识体系”。

它强调三件事：

- **原始资料保留**：源材料单独保存，不被反复覆盖
- **知识页面沉淀**：把实体、概念、对比、查询结果整理成独立页面
- **结构化维护**：通过 `SCHEMA.md`、`index.md`、`log.md` 约束组织方式和更新流程

## 默认目录结构

默认 wiki 路径是 `~/wiki`，典型结构如下：

```text
wiki/
├── SCHEMA.md
├── index.md
├── log.md
├── raw/
│   ├── articles/
│   ├── papers/
│   ├── transcripts/
│   └── assets/
├── entities/
├── concepts/
├── comparisons/
└── queries/
```

其中：

- `raw/`：原始资料层，只读保存
- `entities/`、`concepts/`、`comparisons/`、`queries/`：知识层，由 Agent 创建和维护
- `SCHEMA.md`：约定命名、标签体系、页面阈值和更新规则
- `index.md`：内容总索引
- `log.md`：操作日志

## 工作流程

### 初始化新 Wiki

当用户要求“创建 wiki”时，Agent 应该：

1. 确定 wiki 路径，默认使用 `~/wiki`
2. 创建目录结构
3. 根据具体领域写 `SCHEMA.md`
4. 创建初始 `index.md`
5. 创建初始 `log.md`
6. 准备好后，引导用户导入第一批资料

### 接手已有 Wiki

每次进入一个已有 wiki，会话开始时应先做定向检查：

1. 读取 `SCHEMA.md`
2. 读取 `index.md`
3. 查看 `log.md` 最近的更新记录

这样可以避免：

- 创建重复页面
- 漏掉已有交叉引用
- 违背既有命名或标签规范
- 重复做已经做过的整理工作

### 摄取资料

当用户提供 URL、PDF 或一段文本时，推荐流程是：

1. 把原始资料保存到 `raw/`
2. 识别涉及的实体和概念
3. 检查这些页面是否已经存在
4. 创建新页面或更新已有页面
5. 补充 `[[wikilinks]]` 交叉引用
6. 更新 `index.md` 和 `log.md`

## 使用建议

- 页面文件名保持小写、用连字符连接，例如 `transformer-architecture.md`
- 新页面尽量至少链接到 2 个已有页面，避免形成孤岛
- 标签应统一由 `SCHEMA.md` 维护，不要自由扩散
- 原始资料放进 `raw/` 后尽量保持不可变
- 如果某个回答有长期价值，可以把它沉淀到 `queries/` 或 `comparisons/`

## Obsidian 配合使用

这个 wiki 本质上就是一组 Markdown 文件，因此可以直接用 Obsidian、VS Code 等工具打开。若使用 Obsidian：

- `[[wikilinks]]` 可以直接点击跳转
- Graph View 可视化知识网络
- YAML frontmatter 可配合 Dataview 做查询
- `raw/assets/` 可以存放图片与图表素材

## 目录内容

当前 skill 目录包含：

```text
llm-wiki/
├── SKILL.md
└── README.md
```

其中：

- `SKILL.md`：供 Agent 加载和执行的核心协议
- `README.md`：面向仓库浏览者的人类可读说明

## 参考

- Andrej Karpathy 的 LLM Wiki 思路：`https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f`

如果你希望这个 skill 继续完善，可以下一步补上：

- 更具体的中文使用示例
- 一个可直接复制的 `SCHEMA.md` 模板
- 一个最小可运行的示例 wiki 目录
