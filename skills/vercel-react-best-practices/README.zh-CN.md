# React 最佳实践

一个结构化的仓库，用于创建和维护面向智能体与大语言模型优化的 React 最佳实践。

## 目录结构

- `rules/` - 单条规则文件目录（每条规则一个文件）
  - `_sections.md` - 分区元数据（标题、影响级别、说明）
  - `_template.md` - 新建规则时使用的模板
  - `area-description.md` - 单条规则文件示例
- `src/` - 构建脚本与工具函数
- `metadata.json` - 文档元数据（版本、组织、摘要）
- __`AGENTS.md`__ - 编译产物（自动生成）
- __`test-cases.json`__ - 用于 LLM 评测的测试用例（自动生成）

## 快速开始

1. 安装依赖：
   ```bash
   pnpm install
   ```

2. 根据规则构建 `AGENTS.md`：
   ```bash
   pnpm build
   ```

3. 校验规则文件：
   ```bash
   pnpm validate
   ```

4. 提取测试用例：
   ```bash
   pnpm extract-tests
   ```

## 新建一条规则

1. 复制 `rules/_template.md` 到 `rules/area-description.md`
2. 选择合适的领域前缀：
   - `async-`：消除瀑布式等待（第 1 节）
   - `bundle-`：包体积优化（第 2 节）
   - `server-`：服务端性能（第 3 节）
   - `client-`：客户端数据获取（第 4 节）
   - `rerender-`：重渲染优化（第 5 节）
   - `rendering-`：渲染性能（第 6 节）
   - `js-`：JavaScript 性能（第 7 节）
   - `advanced-`：高级模式（第 8 节）
3. 填写 frontmatter 和正文内容
4. 确保提供清晰、带解释的示例
5. 运行 `pnpm build` 重新生成 `AGENTS.md` 和 `test-cases.json`

## 规则文件结构

每条规则文件都应遵循以下结构：

```markdown
---
title: 在此填写规则标题
impact: MEDIUM
impactDescription: 可选的影响说明
tags: tag1, tag2, tag3
---

## 在此填写规则标题

简要说明这条规则以及它为何重要。

**错误示例（说明哪里有问题）：**

```typescript
// 错误代码示例
```

**正确示例（说明为什么这样是对的）：**

```typescript
// 正确代码示例
```

示例后的可选补充说明。

参考资料：[链接](https://example.com)
```

## 文件命名约定

- 以 `_` 开头的文件属于特殊文件（不会参与构建）
- 规则文件命名格式：`area-description.md`（例如：`async-parallel.md`）
- 所属分区会根据文件名前缀自动推断
- 每个分区内的规则会按照标题字母顺序排序
- ID（例如 `1.1`、`1.2`）会在构建时自动生成

## 影响级别

- `CRITICAL` - 最高优先级，带来显著性能收益
- `HIGH` - 明显的性能提升
- `MEDIUM-HIGH` - 中高程度收益
- `MEDIUM` - 中等性能提升
- `LOW-MEDIUM` - 中低程度收益
- `LOW` - 渐进式优化

## 脚本

- `pnpm build` - 将规则编译为 `AGENTS.md`
- `pnpm validate` - 校验所有规则文件
- `pnpm extract-tests` - 提取用于 LLM 评估的测试用例
- `pnpm dev` - 执行构建并校验

## 贡献指南

当你新增或修改规则时：

1. 使用与你所在分区匹配的文件名前缀
2. 遵循 `_template.md` 的结构
3. 提供清晰的错误/正确示例，并附上解释
4. 添加合适的标签
5. 运行 `pnpm build` 重新生成 `AGENTS.md` 和 `test-cases.json`
6. 规则会按标题自动排序 —— 不需要手动维护编号

## 鸣谢

最初由 [@shuding](https://x.com/shuding) 在 [Vercel](https://vercel.com) 创建。
