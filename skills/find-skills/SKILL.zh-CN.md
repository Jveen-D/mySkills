---
name: find-skills
description: Helps users discover and install agent skills when they ask questions like "how do I do X", "find a skill for X", "is there a skill that can...", or express interest in extending capabilities. This skill should be used when the user is looking for functionality that might exist as an installable skill.
---

# 查找 Skills

这个 skill 用于帮助你从开放的 agent skills 生态中发现并安装合适的 skill。

## 何时使用这个 Skill

当用户出现以下需求时，应使用这个 skill：

- 询问“我该怎么做 X”，而 X 很可能是已有 skill 能覆盖的常见任务
- 直接说“帮我找一个做 X 的 skill”或“有没有适合 X 的 skill”
- 询问“你能做 X 吗”，而 X 属于某种专门能力
- 表达出想扩展 agent 能力的意图
- 想搜索工具、模板或工作流
- 提到自己希望在某个具体领域（如设计、测试、部署等）得到帮助

## 什么是 Skills CLI？

Skills CLI（`npx skills`）是开放 agent skills 生态的包管理工具。Skill 是模块化能力包，用来通过专门知识、工作流和工具扩展 agent 的能力。

**常用命令：**

- `npx skills find [query]` - 交互式或按关键词搜索 skill
- `npx skills add <package>` - 从 GitHub 或其他来源安装 skill
- `npx skills check` - 检查 skill 更新
- `npx skills update` - 更新所有已安装的 skill

**浏览 skills：** `https://skills.sh/`

## 如何帮助用户查找 Skill

### 第一步：理解用户真正需要什么

当用户提出某项需求时，先识别：

1. 所属领域（例如 React、测试、设计、部署）
2. 具体任务（例如写测试、制作动画、评审 PR）
3. 这是否是一个足够常见、很可能已有现成 skill 的任务

### 第二步：先查看排行榜

在运行 CLI 搜索之前，先查看 [skills.sh 排行榜](https://skills.sh/)，确认该领域是否已有知名 skill。排行榜会按照总安装量排序，优先展示最流行、经过验证的选择。

例如，Web 开发领域常见的高排名 skill 有：
- `vercel-labs/agent-skills` — React、Next.js、Web 设计（每项 100K+ 安装）
- `anthropics/skills` — 前端设计、文档处理（100K+ 安装）

### 第三步：搜索 Skill

如果排行榜不能覆盖用户需求，再运行查找命令：

```bash
npx skills find [query]
```

例如：

- 用户问“怎么让我的 React 应用更快？” → `npx skills find react performance`
- 用户问“你能帮我做 PR review 吗？” → `npx skills find pr review`
- 用户说“我需要生成 changelog” → `npx skills find changelog`

### 第四步：推荐前先验证质量

**不要只根据搜索结果就直接推荐 skill。** 推荐前务必检查：

1. **安装量** —— 优先选择安装量在 1K 以上的 skill；低于 100 的需要谨慎。
2. **来源信誉** —— 来自 `vercel-labs`、`anthropics`、`microsoft` 等官方或知名来源更可靠。
3. **GitHub Star 数** —— 检查源仓库；如果仓库 Star 少于 100，应谨慎看待。

### 第五步：把选项展示给用户

找到相关 skill 后，应向用户说明：

1. skill 名称及作用
2. 安装量和来源
3. 可直接执行的安装命令
4. 在 `skills.sh` 查看详情的链接

示例回复：

```
我找到一个可能适合你的 skill！“react-best-practices” 提供了
来自 Vercel Engineering 的 React 和 Next.js 性能优化指南。
（185K installs）

安装命令：
npx skills add vercel-labs/agent-skills@react-best-practices

了解更多：https://skills.sh/vercel-labs/agent-skills/react-best-practices
```

### 第六步：主动提出帮用户安装

如果用户想继续，你可以直接替他们安装：

```bash
npx skills add <owner/repo@skill> -g -y
```

其中 `-g` 表示全局安装（用户级），`-y` 用于跳过确认提示。

## 常见 Skill 分类

搜索时可以从以下常见分类切入：

| 分类 | 示例查询 |
| ---- | -------- |
| Web 开发 | react, nextjs, typescript, css, tailwind |
| 测试 | testing, jest, playwright, e2e |
| DevOps | deploy, docker, kubernetes, ci-cd |
| 文档 | docs, readme, changelog, api-docs |
| 代码质量 | review, lint, refactor, best-practices |
| 设计 | ui, ux, design-system, accessibility |
| 生产力 | workflow, automation, git |

## 提高搜索效果的小技巧

1. **使用更具体的关键词**：例如 “react testing” 比单独搜 “testing” 更好
2. **尝试同义表达**：如果 “deploy” 没结果，就试试 “deployment” 或 “ci-cd”
3. **优先看热门来源**：很多 skill 来自 `vercel-labs/agent-skills` 或 `ComposioHQ/awesome-claude-skills`

## 当没有找到 Skill 时

如果没有合适的 skill：

1. 明确告诉用户目前没找到现成 skill
2. 表示你仍然可以用通用能力直接帮助完成任务
3. 建议用户如果这是高频需求，也可以自己创建 skill，例如使用 `npx skills init`

示例：

```
我搜索了与 “xyz” 相关的 skill，但暂时没有找到匹配项。
不过我仍然可以直接帮你完成这项任务！如果你愿意，我现在就可以继续。

如果这是你经常要做的事情，也可以考虑自己创建一个 skill：
npx skills init my-xyz-skill
```
