# 知识库总编 · Knowledge Base Editor

把零散经验、想法和资料整理成可逐篇续写的中文知识库。

这是一个不限定模型的中文知识库写作 Skill，采用 Agent Skills 的 `SKILL.md` 结构：通过聊天明确读者与目标，研究资料后提出大纲，确认后逐篇写作，并维护文章之间的关联引用。适合系列教程、学习手册、经验分享和案例库。

**当前版本：1.1.0。** 包含写作指令与参考资源，无需单独启动服务。

## 兼容性与模型

能否自动加载 Skill，取决于你使用的 AI 工具是否支持 Agent Skills；写作效果还取决于其中运行的模型、上下文容量和可用工具。本 Skill 未指定模型名称，也未调用任何特定模型供应商的 API。[Agent Skills 是可跨工具复用的开放格式](https://agentskills.io/home)。

| 使用环境 | 使用方式 | 本项目的验证状态 |
| --- | --- | --- |
| Codex | 通过技能安装器或技能目录加载 | 已验证公开下载与安装；未覆盖全部模型或写作场景 |
| Claude Code | 放入 `.claude/skills/` 或个人技能目录 | 官方支持该格式；本 Skill 尚未在此平台实测 |
| Gemini CLI | 通过 `gemini skills install` 或技能目录加载 | 官方支持该格式；本 Skill 尚未在此平台实测 |
| Cursor Agent | 放入 `.cursor/skills/` 或个人技能目录 | 官方支持该格式；本 Skill 尚未在此平台实测 |
| 其他模型或聊天工具 | 有技能加载能力时按宿主规则安装；否则提供指令和参考材料作为写作上下文 | 需按具体工具与模型验证 |

因此，GPT、Claude、Gemini 等模型可通过各自支持的工具使用这套流程；对于 DeepSeek、Qwen 等其他模型，也可在合适的 Agent 环境中尝试，尚未经过本项目测试。不同模型的长文一致性、中文表达与工具调用效果需分别验证。

`agents/openai.yaml` 是 Codex 使用的界面元数据，不会限制核心写作指令的模型选择。跨工具使用时，保留完整的 `SKILL.md`、`references/` 和许可证，并按目标工具的规则加载。

## 工作流程

聊天确认需求 → 查找与核实资料 → 提出并确认大纲 → 逐篇撰写与修订 → 更新目录、引用和进度

| 阶段 | 你提供什么 | Skill 完成什么 |
| --- | --- | --- |
| 确认需求 | 主题想法、读者、已有材料；可以口语描述 | 补问关键缺口，整理简报，复用已经确认的选择 |
| 查找资料 | 自有经验、参考材料或允许研究的范围 | 阅读实际可访问内容，记录来源、证据与缺口 |
| 制定大纲 | 对范围和顺序提出意见 | 按读者任务组织篇目，说明每篇成果、前置与边界 |
| 逐篇写作 | 选择先写哪篇，或授权连续写作 | 写出正文和必要图表，检查事实、步骤与空话 |
| 持续维护 | 反馈、补充材料或新的修改要求 | 更新进度、已有文章引用和待补项，支持后续接着写 |

不要求每篇套同一模板。教程说明操作与验收，原理文解释机制与边界，比较文给出选择条件，案例区分真实事实与作者分析。

## 安装与调用

### Codex

在 Codex 中发送：

```text
使用 $skill-installer，从以下 GitHub 路径安装 knowledge-base-editor：
https://github.com/QingkaiWu/knowledge-base-editor/tree/main/skills/knowledge-base-editor
```

安装完成后，在下一轮对话调用它。若已有同名 Skill，请先让 Codex 比较版本，再决定是否更新。

也可以下载本仓库 ZIP，解压后把 `skills/knowledge-base-editor` 文件夹完整放入你的 Codex 技能目录。默认是 `~/.codex/skills/`；设置了 `CODEX_HOME` 时使用其下的 `skills/`。保留 `references/` 和 `agents/`，不要只复制 `SKILL.md`。

[下载 v1.1.0 安装包](https://github.com/QingkaiWu/knowledge-base-editor/releases/download/v1.1.0/knowledge-base-editor-1.1.0.zip)：该包直接包含 `knowledge-base-editor/` 文件夹及 MIT 许可证，可将整个文件夹放入技能目录。[查看版本说明](https://github.com/QingkaiWu/knowledge-base-editor/releases/tag/v1.1.0)。

### Claude Code

下载并解压安装包，将完整的 `knowledge-base-editor` 文件夹放入 `~/.claude/skills/`，或当前项目的 `.claude/skills/`。然后使用 `/knowledge-base-editor` 加上你的请求，也可以用自然语言说明要使用知识库总编。安装目录与调用语法依据 [Claude Code 官方说明](https://code.claude.com/docs/en/skills)，本项目尚未在该平台执行测试。

### Gemini CLI

在已安装 Gemini CLI 的终端运行：

```bash
gemini skills install https://github.com/QingkaiWu/knowledge-base-editor.git --path skills/knowledge-base-editor
```

也可以把完整技能文件夹放入 `~/.gemini/skills/`。已有会话中使用 `/skills reload` 刷新，再通过自然语言请求使用知识库总编。命令与目录依据 [Gemini CLI 官方说明](https://geminicli.com/docs/cli/skills/)，本项目尚未在该平台执行测试。

### Cursor Agent

下载并解压安装包，将完整的 `knowledge-base-editor` 文件夹放入当前项目的 `.cursor/skills/`，或个人目录 `~/.cursor/skills/`。在 Agent 中使用 `/knowledge-base-editor`，或提出与该 Skill 匹配的请求。目录与调用方式依据 [Cursor 官方说明](https://cursor.com/docs/skills)，本项目尚未在该平台执行测试。

### 只有聊天界面时

如果工具没有 Skill 安装入口，可以提供 `SKILL.md` 及当前阶段需要的 `references/` 文件，让模型按其中的流程协作；工具无法读取文件时，粘贴相关文本。自动发现技能、跨会话读取项目记录、联网研究和飞书写入，需要所在工具提供相应能力。使用提示词不能自动开通这些功能。

## 开始使用

### 主题还没想清楚

```text
使用知识库总编（knowledge-base-editor）。我想把自己的经验整理成知识库，主题还比较模糊。先和我聊清楚读者、读后成果和材料范围，再找资料、出大纲。
```

### 已有明确简报

```text
使用知识库总编（knowledge-base-editor）。我要做一套面向职场新人的工作笔记教程，读完能把零散记录整理成以后找得到、用得上的资料。文风专业、好懂、少空话。请阅读我提供的材料，补充研究后提出大纲，确认后再写正文。
```

### 继续已有知识库

```text
使用知识库总编（knowledge-base-editor），继续当前知识库的下一篇。先读取现有简报、目录和相关正文，沿用确认过的读者与文风，在有帮助的位置引用已有文章，完成后更新进度。
```

查看[首次使用示例](examples/first-run.md)，了解从模糊想法到可审阅大纲的过程。示例为教学构造，不是实际用户运行记录。

## 产出与续写

AI 按实际需要维护简报、目录、来源、正文与图表。已有项目可保留原来的文件名和组织方式。

每篇使用稳定 ID；改标题时检查受影响的引用。引用前阅读目标正文，未写文章记为计划中，不能编造链接。新会话提供知识库项目位置后，先读已有记录再继续。

默认以飞书可编辑文档为主要交付目标，也可按你的要求输出 Markdown 或其他文档格式。**安装本 Skill 不会自动连接飞书。** 研究、绘图和文档写入依赖所在 AI 工具当前可用的能力与权限；无法完成线上写入时，交付本地正文和可导入稿，并说明剩余步骤。

## 文件结构

```text
knowledge-base-editor/
├── README.md
├── LICENSE
├── examples/
│   └── first-run.md
└── skills/
    └── knowledge-base-editor/
        ├── SKILL.md
        ├── LICENSE
        ├── agents/openai.yaml
        └── references/
            ├── interview-and-approval.md
            ├── research-and-outline.md
            ├── writing-patterns.md
            ├── project-records.md
            └── review-and-state.md
```

[查看 Skill 主入口](skills/knowledge-base-editor/SKILL.md)。安装所需文件位于 `skills/knowledge-base-editor/`。

## 验证范围

1.1.0 已完成基础格式校验、内部资源链接检查和本地跨篇引用演练。它们不能证明任意主题的写作质量或飞书交付稳定性。不同材料质量、模型与工具条件会影响结果。

## 反馈

遇到问题可在本仓库 Issues 描述：你的请求、预期结果、实际结果、使用环境和 Skill 版本。贴出必要片段即可；请先去除私人资料和访问凭据。

## 许可证

采用 [MIT License](LICENSE)，允许使用、修改、分发和商业使用，并要求保留版权与许可声明。安装目录中也包含许可证，便于单独分发 Skill 时保留。
