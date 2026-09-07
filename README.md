# 知识库总编 · Knowledge Base Editor

把零散经验、想法和资料整理成可逐篇续写的中文知识库。

这是一个面向 Codex 的 Skill：通过聊天明确读者与目标，研究资料后提出大纲，确认后逐篇写作，并维护文章之间的关联引用。适合系列教程、学习手册、经验分享和案例库。

**当前版本：1.1.0。** 包含写作指令与参考资源，无需单独启动服务。

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

## 安装到 Codex

在 Codex 中发送：

```text
使用 $skill-installer，从以下 GitHub 路径安装 knowledge-base-editor：
https://github.com/QingkaiWu/knowledge-base-editor/tree/main/skills/knowledge-base-editor
```

安装完成后，在下一轮对话调用它。若已有同名 Skill，请先让 Codex 比较版本，再决定是否更新。

也可以下载本仓库 ZIP，解压后把 `skills/knowledge-base-editor` 文件夹完整放入你的 Codex 技能目录。默认是 `~/.codex/skills/`；设置了 `CODEX_HOME` 时使用其下的 `skills/`。保留 `references/` 和 `agents/`，不要只复制 `SKILL.md`。

[下载 v1.1.0 安装包](https://github.com/QingkaiWu/knowledge-base-editor/releases/download/v1.1.0/knowledge-base-editor-1.1.0.zip)：该包直接包含 `knowledge-base-editor/` 文件夹及 MIT 许可证，可将整个文件夹放入技能目录。[查看版本说明](https://github.com/QingkaiWu/knowledge-base-editor/releases/tag/v1.1.0)。

## 开始使用

### 主题还没想清楚

```text
使用 $knowledge-base-editor。我想把自己的经验整理成知识库，主题还比较模糊。先和我聊清楚读者、读后成果和材料范围，再找资料、出大纲。
```

### 已有明确简报

```text
使用 $knowledge-base-editor。我要做一套面向职场新人的工作笔记教程，读完能把零散记录整理成以后找得到、用得上的资料。文风专业、好懂、少空话。请阅读我提供的材料，补充研究后提出大纲，确认后再写正文。
```

### 继续已有知识库

```text
使用 $knowledge-base-editor，继续当前知识库的下一篇。先读取现有简报、目录和相关正文，沿用确认过的读者与文风，在有帮助的位置引用已有文章，完成后更新进度。
```

查看[首次使用示例](examples/first-run.md)，了解从模糊想法到可审阅大纲的过程。示例为教学构造，不是实际用户运行记录。

## 产出与续写

AI 按实际需要维护简报、目录、来源、正文与图表。已有项目可保留原来的文件名和组织方式。

每篇使用稳定 ID；改标题时检查受影响的引用。引用前阅读目标正文，未写文章记为计划中，不能编造链接。新会话提供知识库项目位置后，先读已有记录再继续。

默认以飞书可编辑文档为主要交付目标，也可按你的要求输出 Markdown 或其他文档格式。**安装本 Skill 不会自动连接飞书。** 研究、绘图和文档写入依赖 Codex 当前可用的工具及权限；无法完成线上写入时，交付本地正文和可导入稿，并说明剩余步骤。

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
