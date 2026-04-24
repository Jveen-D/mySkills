# translate-skill-descriptions

一个用于 **批量本地化 Skill 元数据与说明文档** 的 CodeBuddy skill。

它会扫描当前工作区内的所有 `SKILL.md`，完成两件核心事情：

- 将真实生效的 `SKILL.md` 中 `description` 翻译成中文
- 在同目录创建或更新 `SKILL.zh-CN.md`，作为中文阅读副本

## 适用场景

适合以下情况：

- 你维护的是一个包含多个 skill 的仓库
- 你希望在 skill 选择面板中直接显示中文描述
- 你希望保留英文原文，同时提供完整中文副本
- 你需要统一 `SKILL.md` / `SKILL.zh-CN.md` 的目录与命名规范
- 你需要批量处理，而不是手工逐个修改

## 它会做什么

### 1. 扫描全部真实 Skill

递归查找工作区中的所有 `SKILL.md`，并排除 `SKILL.zh-CN.md` 这类翻译副本。

### 2. 修改真实生效的描述

仅修改 frontmatter 中的 `description` 字段：

- 单行 `description` 保持单行结构
- 多行 `description: |` 保持 YAML 块格式
- 不改动 `name`、`metadata`、`license`、`allowed-tools` 等其他字段

这样 skill 选择界面读取到的说明会直接变成中文。

### 3. 生成中文副本

在每个 `SKILL.md` 同目录创建或更新 `SKILL.zh-CN.md`：

- 保留英文原文文件不删除
- 同步中文 `description`
- 翻译标题与主要说明内容
- 必要时继续扩展为全文翻译版本

### 4. 检查多份副本与缓存问题

如果同一个 skill 同时存在于 `.agents`、`.codebuddy` 或其他镜像目录中，这个 skill 的工作流会继续排查并提示你同步更新，避免出现“文件已改中文，但 UI 仍显示英文”的问题。

## 推荐用法

当你想让整个 skill 仓库统一中文化时，直接让代理执行：

- 处理当前所有的 skill
- 将所有 `SKILL.md` 的 `description` 翻译成中文
- 为每个 skill 建立 `SKILL.zh-CN.md` 中文副本

## 输出结果

执行完成后，理想结果应当是：

- 所有真实 `SKILL.md` 的 `description` 都已经是中文
- 所有 skill 都存在 `SKILL.zh-CN.md`
- 英文原文件仍被保留
- 中文副本与真实生效文件语义一致

## 说明

这个 skill 主要面向 **skill 仓库维护者**、**中文本地化场景** 和 **需要统一元数据展示语言** 的团队。
