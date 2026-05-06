---
name: skip-lint-build-checks
description: 通过跳过 lint 错误清理以及打包、构建或 bundle 校验来保持任务完成范围收敛。适用于用户说明不需要处理 lint 错误、不需要打包或构建验证，或任务完成时应避免追查无关 lint/build 失败，除非用户明确要求。
---

# Skip Lint Build Checks

## Rule

Complete the requested task without expanding the scope to lint fixes or packaging validation.

## Apply This Boundary

- Do not run lint commands such as `lint`, `eslint`, `biome check`, `stylelint`, or equivalent lint-only scripts unless the user explicitly asks for them.
- Do not fix unrelated lint errors discovered while working.
- Do not run packaging, bundling, or production build checks such as `build`, `package`, `pack`, `bundle`, or release packaging commands unless the user explicitly asks for them.
- Do not treat existing lint failures or build/package failures as blockers for completion when they are outside the requested task.
- Prefer targeted verification that directly matches the change, such as a focused unit test, smoke check, type check, or syntax check when appropriate.
- If a skipped lint or build check would normally be expected, mention in the final response that it was intentionally skipped because this skill applies.

## Override

If the user explicitly asks to fix lint errors, run lint, build, package, bundle, or validate production output, follow that newer request.
