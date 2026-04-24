---
name: vercel-react-best-practices
description: 来自 Vercel Engineering 的 React 与 Next.js 性能优化指南。适用于编写、评审或重构 React/Next.js 代码时，确保采用更优的性能模式；当任务涉及 React 组件、Next.js 页面、数据获取、包体积优化或性能改进时应使用此 skill。
license: MIT
metadata:
  author: vercel
  version: "1.0.0"
---

# Vercel React 最佳实践

这是由 Vercel 维护的 React 与 Next.js 应用性能优化指南。内容包含 8 个类别、70 条规则，并按影响程度排序，可用于指导自动化重构与代码生成。

## 适用场景

在以下情况下应参考这些指南：
- 编写新的 React 组件或 Next.js 页面
- 实现数据获取逻辑（客户端或服务端）
- 评审存在性能问题的代码
- 重构现有 React / Next.js 代码
- 优化包体积或加载速度

## 按优先级划分的规则类别

| 优先级 | 类别 | 影响级别 | 前缀 |
|----------|----------|--------|--------|
| 1 | 消除瀑布式等待 | CRITICAL | `async-` |
| 2 | 包体积优化 | CRITICAL | `bundle-` |
| 3 | 服务端性能 | HIGH | `server-` |
| 4 | 客户端数据获取 | MEDIUM-HIGH | `client-` |
| 5 | 重渲染优化 | MEDIUM | `rerender-` |
| 6 | 渲染性能 | MEDIUM | `rendering-` |
| 7 | JavaScript 性能 | LOW-MEDIUM | `js-` |
| 8 | 高级模式 | LOW | `advanced-` |

## 快速参考

### 1. 消除瀑布式等待（CRITICAL）

- `async-cheap-condition-before-await` - 在等待远程值或 flag 前先判断廉价同步条件
- `async-defer-await` - 仅在真正需要的分支中再执行 `await`
- `async-parallel` - 对互不依赖的操作使用 `Promise.all()`
- `async-dependencies` - 对部分依赖关系使用更合理的并发组织方式
- `async-api-routes` - 在 API 路由中尽早启动 Promise，尽晚等待结果
- `async-suspense-boundaries` - 使用 `Suspense` 流式输出内容

### 2. 包体积优化（CRITICAL）

- `bundle-barrel-imports` - 直接导入，避免 barrel 文件
- `bundle-analyzable-paths` - 优先使用静态可分析的 import 与文件路径，避免产生过宽的打包范围与 trace
- `bundle-dynamic-imports` - 对重量级组件使用 `next/dynamic`
- `bundle-defer-third-party` - 在 hydration 后再加载分析/日志类第三方库
- `bundle-conditional` - 仅在功能启用时再加载对应模块
- `bundle-preload` - 在 hover/focus 时预加载，提升感知速度

### 3. 服务端性能（HIGH）

- `server-auth-actions` - 像保护 API 路由一样保护 server actions
- `server-cache-react` - 使用 `React.cache()` 做单请求去重
- `server-cache-lru` - 使用 LRU 缓存跨请求数据
- `server-dedup-props` - 避免在 RSC props 中重复序列化
- `server-hoist-static-io` - 将静态 I/O（字体、logo）提升到模块级
- `server-no-shared-module-state` - 避免在 RSC/SSR 中使用模块级可变请求状态
- `server-serialization` - 最小化传给客户端组件的数据量
- `server-parallel-fetching` - 重构组件以并行获取数据
- `server-parallel-nested-fetching` - 对嵌套数据获取使用 `Promise.all` 按项并行
- `server-after-nonblocking` - 使用 `after()` 处理非阻塞操作

### 4. 客户端数据获取（MEDIUM-HIGH）

- `client-swr-dedup` - 使用 SWR 自动去重请求
- `client-event-listeners` - 去重全局事件监听器
- `client-passive-event-listeners` - 对滚动监听使用 passive listener
- `client-localstorage-schema` - 为 `localStorage` 做版本管理并减少存储数据量

### 5. 重渲染优化（MEDIUM）

- `rerender-defer-reads` - 仅在回调中使用的状态不要提前订阅
- `rerender-memo` - 将昂贵计算提取到记忆化组件中
- `rerender-memo-with-default-value` - 将默认的非原始类型 props 提升到外部
- `rerender-dependencies` - 在 effect 中优先使用原始类型依赖
- `rerender-derived-state` - 订阅派生布尔值，而不是原始值
- `rerender-derived-state-no-effect` - 在 render 阶段派生状态，而不是在 effect 中派生
- `rerender-functional-setstate` - 使用函数式 `setState` 获得稳定回调
- `rerender-lazy-state-init` - 对昂贵初始值传函数给 `useState`
- `rerender-simple-expression-in-memo` - 简单原始值不要滥用 `memo`
- `rerender-split-combined-hooks` - 将依赖独立的 hook 拆开
- `rerender-move-effect-to-event` - 交互逻辑放进事件处理器，而不是 effect
- `rerender-transitions` - 对非紧急更新使用 `startTransition`
- `rerender-use-deferred-value` - 延迟昂贵渲染，保持输入响应性
- `rerender-use-ref-transient-values` - 高频临时值使用 `ref`
- `rerender-no-inline-components` - 不要在组件内部定义组件

### 6. 渲染性能（MEDIUM）

- `rendering-animate-svg-wrapper` - 给包裹层 `div` 做动画，而不是直接给 SVG 元素做动画
- `rendering-content-visibility` - 长列表使用 `content-visibility`
- `rendering-hoist-jsx` - 将静态 JSX 提出组件外部
- `rendering-svg-precision` - 降低 SVG 坐标精度
- `rendering-hydration-no-flicker` - 对仅客户端数据使用内联脚本避免闪烁
- `rendering-hydration-suppress-warning` - 对可预期的不一致使用 suppress warning
- `rendering-activity` - 用 `Activity` 组件处理显示/隐藏
- `rendering-conditional-render` - 条件渲染优先三元表达式，不要滥用 `&&`
- `rendering-usetransition-loading` - 加载状态优先考虑 `useTransition`
- `rendering-resource-hints` - 使用 React DOM resource hints 进行预加载
- `rendering-script-defer-async` - script 标签使用 `defer` 或 `async`

### 7. JavaScript 性能（LOW-MEDIUM）

- `js-batch-dom-css` - 通过 class 或 `cssText` 批量更新 CSS
- `js-index-maps` - 重复查找时先构建 `Map`
- `js-cache-property-access` - 在循环中缓存对象属性访问
- `js-cache-function-results` - 用模块级 `Map` 缓存函数结果
- `js-cache-storage` - 缓存 `localStorage` / `sessionStorage` 读取结果
- `js-combine-iterations` - 多次 `filter` / `map` 合并成一次循环
- `js-length-check-first` - 先检查数组长度，再做昂贵比较
- `js-early-exit` - 函数中尽早返回
- `js-hoist-regexp` - 将 `RegExp` 创建提升出循环
- `js-min-max-loop` - 求最值时用循环，不要先排序
- `js-set-map-lookups` - 用 `Set` / `Map` 实现 O(1) 查找
- `js-tosorted-immutable` - 使用 `toSorted()` 保持不可变性
- `js-flatmap-filter` - 用 `flatMap` 一次完成映射与过滤
- `js-request-idle-callback` - 将非关键任务延后到浏览器空闲时执行

### 8. 高级模式（LOW）

- `advanced-effect-event-deps` - 不要把 `useEffectEvent` 的结果放进 effect 依赖中
- `advanced-event-handler-refs` - 将事件处理函数存入 `ref`
- `advanced-init-once` - 应用初始化应在一次应用加载期间只执行一次
- `advanced-use-latest` - 使用 `useLatest` 维护稳定回调引用

## 使用方式

阅读单独的规则文件，查看详细说明与代码示例：

```
rules/async-parallel.md
rules/bundle-barrel-imports.md
```

每个规则文件通常包含：
- 为什么这条规则重要的简要说明
- 带解释的错误代码示例
- 带解释的正确代码示例
- 补充背景与参考资料

## 完整编译文档

如需查看所有规则展开后的完整指南，请阅读：`AGENTS.md`
