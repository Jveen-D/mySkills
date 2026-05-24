---
name: git-commit-chinese
description: 使用 Conventional Commits 生成和校验中文 Git 提交信息。适用于 Codex 需要创建、建议、审核、暂存或执行 git commit，编写提交信息，总结 Git 变更，或选择 feat、fix、style、refactor、docs、test、chore、build、ci、perf、revert、security、release 等提交类型的场景。
---

# Git Commit Chinese

## Workflow

When creating or suggesting a commit message:

1. Inspect the actual diff before deciding the message.
2. Identify the dominant intent of the change, not just the files touched.
3. Use the format `<type>: <中文摘要>`.
4. Keep the subject concise, specific, and in Simplified Chinese.
5. Do not end the subject with punctuation.
6. Use an optional body only when the change needs extra context, migration notes, or risk notes.

When the user asks Codex to run `git commit`, commit with the selected Chinese message after normal staging and verification steps for the task.

## Commit Types

Use these types:

- `feat`: Add a new user-facing or developer-facing capability.
- `fix`: Fix a bug, incorrect behavior, crash, regression, or broken edge case.
- `style`: Change only visual/UI style, formatting, whitespace, CSS presentation, copy layout, or non-behavioral appearance.
- `refactor`: Restructure code without changing behavior.
- `perf`: Improve runtime performance, memory usage, bundle size, query efficiency, or rendering speed.
- `docs`: Change documentation, comments intended as documentation, README files, guides, examples, or generated docs.
- `test`: Add, update, or fix tests, fixtures, mocks, snapshots, or test infrastructure only.
- `chore`: Change maintenance tasks that do not affect app behavior, such as repository housekeeping, config cleanup, metadata, editor settings, or routine scripts.
- `build`: Change build system, packaging, bundling, lockfiles, dependency versions, or generated build artifacts.
- `ci`: Change CI/CD workflows, automation, release pipelines, or repository checks.
- `security`: Fix or harden security behavior, permissions, validation, secrets handling, dependency vulnerabilities, or auth-sensitive flows.
- `revert`: Revert a previous commit.
- `release`: Version bumps, changelog updates, release metadata, or publish preparation.

## Selection Rules

Prefer the type that explains the user-visible or system-visible result:

- New feature plus tests: use `feat`.
- Bug fix plus tests: use `fix`.
- Behavior-preserving code cleanup plus tests: use `refactor`.
- CSS or visual-only component changes: use `style`.
- Dependency updates that fix a security issue: use `security` if the security intent is explicit; otherwise use `build`.
- Lockfile-only or package manager metadata changes: use `build`.
- Config changes for tooling only: use `chore`, unless the tool is CI/CD (`ci`) or build/package output (`build`).
- Documentation plus code changes: use the code-change type unless documentation is the primary change.
- Multiple unrelated changes: prefer splitting into separate commits; if not possible, choose the dominant intent.

## Message Style

Write the summary in Chinese after the colon:

- `feat: 添加用户导出入口`
- `fix: 修复登录过期后的跳转错误`
- `style: 调整仪表盘卡片间距`
- `refactor: 简化订单状态计算逻辑`
- `perf: 减少列表重复渲染`
- `docs: 更新部署说明`
- `test: 补充支付失败用例`
- `chore: 清理无用开发配置`
- `build: 升级前端依赖版本`
- `ci: 调整发布工作流触发条件`
- `security: 加强回调地址校验`
- `revert: 回退订单导出改动`
- `release: 准备 1.4.0 发布`

Avoid vague summaries such as:

- `fix: 修复问题`
- `feat: 更新功能`
- `chore: 修改代码`

## Optional Scope

Use an optional scope only when it makes history easier to scan:

- `feat(auth): 添加短信验证码登录`
- `fix(api): 修复分页参数解析`
- `style(button): 调整禁用态颜色`

Keep scopes lowercase ASCII when they refer to packages, modules, or folders.

## Commit Body

Add a body when needed:

```text
fix: 修复批量导入失败后的状态回滚

导入过程中任一行校验失败时，现在会回滚已写入的临时记录，并保留失败原因供前端展示。
```

For breaking changes, include a footer:

```text
feat: 调整任务同步接口参数

BREAKING CHANGE: /api/tasks/sync 现在要求传入 workspaceId。
```
