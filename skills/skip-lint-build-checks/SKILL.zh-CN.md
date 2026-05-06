---
name: skip-lint-build-checks
description: 通过跳过 lint 错误清理以及打包、构建或 bundle 校验来保持任务完成范围收敛。适用于用户说明不需要处理 lint 错误、不需要打包或构建验证，或任务完成时应避免追查无关 lint/build 失败，除非用户明确要求。
---

# 跳过 Lint 与打包校验

## 规则

完成用户请求的任务，不要把范围扩大到 lint 修复或打包验证。

## 应用此边界

- 不要运行 `lint`、`eslint`、`biome check`、`stylelint` 或等价的纯 lint 命令，除非用户明确要求。
- 不要修复工作过程中发现的无关 lint 错误。
- 不要运行 `build`、`package`、`pack`、`bundle` 或发布打包类命令，除非用户明确要求。
- 当现有 lint 失败或 build/package 失败位于请求任务范围之外时，不要把它们视为完成任务的阻塞项。
- 优先使用与本次改动直接匹配的目标验证，例如聚焦的单元测试、冒烟检查、类型检查或语法检查。
- 如果通常会预期执行 lint 或 build 检查但本次跳过了，请在最终回复中说明这是因为此 skill 生效而有意跳过。

## 覆盖规则

如果用户明确要求修复 lint 错误、运行 lint、build、package、bundle 或验证生产输出，请遵循该更新的请求。
