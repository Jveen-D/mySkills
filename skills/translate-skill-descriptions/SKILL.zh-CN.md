---
name: translate-skill-descriptions
description: 用于批量本地化当前工作区内所有 `SKILL.md` 的元数据与说明文档：将真实生效文件中的 `description` 翻译为中文，并在同目录创建或更新 `SKILL.zh-CN.md` 中文副本。适用于维护 skills 仓库、统一技能选择面板展示语言、保留英文原文同时提供中文版本等场景。
---

# 翻译 Skill 描述

## 概述

扫描当前工作区内所有技能目录，识别真实生效的 `SKILL.md` 文件，完成两项任务：

1. 将 YAML frontmatter 中的 `description` 翻译为中文，使技能选择界面直接显示中文说明。
2. 在每个 `SKILL.md` 同目录创建或更新 `SKILL.zh-CN.md`，保留英文原文件不删除，并提供中文阅读副本。

## 何时使用

在以下场景触发此 skill：

- 维护一个包含多个技能的 skill 仓库
- 需要让技能选择器直接显示中文描述
- 需要为每个 skill 建立中文副本文件
- 需要统一 `SKILL.md` 与 `SKILL.zh-CN.md` 的命名和目录结构
- 需要批量翻译 skill 元数据而不是逐个手工编辑

## 工作流程

### 1. 发现所有 Skill

递归搜索当前工作区内所有 `SKILL.md` 文件。

执行时遵循以下规则：
- 排除 `SKILL.zh-CN.md`，只把真实生效的 `SKILL.md` 当作源文件
- 若仓库存在多份 skill 存储位置（例如 `.agents` 与 `.codebuddy`），分别检查并确认哪一份实际被系统读取
- 记录所有 skill 路径，确保翻译范围完整

### 2. 更新生效中的元数据

优先修改真实生效的 `SKILL.md`。

操作要求：
- 只改 frontmatter 中的 `description`
- 保留 `name`、`license`、`metadata`、`allowed-tools` 等其他字段不变
- 若 `description` 是单行，替换为中文单行
- 若 `description` 是 YAML 多行块（`description: |`），保留原格式并翻译其内容
- 目标是让技能选择界面直接显示中文

### 3. 创建或刷新中文副本

为每个 `SKILL.md` 在同目录创建或更新 `SKILL.zh-CN.md`。

约束如下：
- 不覆盖或删除英文原始 `SKILL.md`
- 文件命名固定为 `SKILL.zh-CN.md`
- 中文副本至少要同步：
  - frontmatter
  - 中文 `description`
  - 标题
  - 使用说明
- 若全文翻译成本过高，可优先翻译入口层内容，并保留代码示例原样
- 若用户明确要求全文翻译，则继续翻译正文各章节

### 4. 保持两边一致

完成后检查以下一致性：
- 每个 `SKILL.md` 都有对应的 `SKILL.zh-CN.md`
- 每个真实 `SKILL.md` 的 `description` 都已中文化
- 每个 `SKILL.zh-CN.md` 的 `description` 与真实生效文件含义一致
- 若同一 skill 在多个目录出现副本，避免一处中文、一处英文的状态不一致

### 5. 用数量验证

验证时至少执行：
- 统计 `SKILL.md` 数量
- 统计 `SKILL.zh-CN.md` 数量
- 抽查每个 `SKILL.md` 的前几行，确认 `description` 已是中文
- 若用户反馈界面仍显示英文，继续排查缓存、锁文件或镜像目录

## 故障排查

### UI 仍显示英文

若文件已改成中文但界面仍显示英文，优先排查：
- 是否存在第二份 skill 仓库副本（例如 `.codebuddy`、`.agents`）
- 是否存在锁文件或安装索引（例如 `.skill-lock.json`）
- 是否命中了缓存而非最新本地文件
- 是否只改了中文副本而未改真实生效的 `SKILL.md`

### 重复的 Skill 来源

如果同一个 skill 同时存在于多个目录：
- 先确认哪个目录被技能系统实际读取
- 再把另一份同步更新，避免再次出现显示不一致

## 输出预期

完成任务后应能明确给出：
- 一共有多少个真实 `SKILL.md`
- 一共有多少个 `SKILL.zh-CN.md`
- 是否所有真实 skill 都已中文化 description
- 是否所有 skill 都已有中文副本
- 若仍有未生效项，指出具体缓存或路径原因
