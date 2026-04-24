# Three.js Skills for Claude Code

这是一个精心整理的 Three.js skill 文件集合，为 Claude Code 提供创建 3D 元素与交互体验所需的基础知识。

## 目的

在处理 Three.js 相关任务时，Claude Code 虽然具备通用编程知识，但通常缺少具体的 Three.js API 细节、最佳实践以及常见模式。这些 skill 文件用于补齐这部分能力，提供：

- 准确的 API 参考与构造函数签名
- 常见场景下可运行的代码示例
- 性能优化建议
- 不同 Three.js 子系统之间的集成模式

## 安装

将此仓库克隆到你的项目中，或复制 `.claude/skills` 目录：

```bash
git clone https://github.com/pinkforest/threejs-playground.git
```

或者添加为子模块：

```bash
git submodule add https://github.com/pinkforest/threejs-playground.git
```

## 包含的技能

| Skill                      | 说明 |
| -------------------------- | ---- |
| **threejs-fundamentals**   | 场景搭建、相机、渲染器、`Object3D` 层级、坐标系统 |
| **threejs-geometry**       | 内置几何体、`BufferGeometry`、自定义几何体、实例化 |
| **threejs-materials**      | PBR 材质、基础/Phong/Standard 材质、着色器材质 |
| **threejs-lighting**       | 灯光类型、阴影、环境光照、灯光辅助对象 |
| **threejs-textures**       | 纹理类型、UV 映射、环境贴图、渲染目标 |
| **threejs-animation**      | 关键帧动画、骨骼动画、变形目标、动画混合 |
| **threejs-loaders**        | GLTF/GLB 加载、纹理加载、异步模式、缓存 |
| **threejs-shaders**        | GLSL 基础、`ShaderMaterial`、uniform、自定义效果 |
| **threejs-postprocessing** | `EffectComposer`、泛光、景深、屏幕后处理、自定义 Pass |
| **threejs-interaction**    | 射线投射、相机控制、鼠标/触摸输入、物体选择 |

## 工作方式

当你的请求与上下文匹配时，Claude Code 会自动从 `.claude/skills` 目录加载相应的 skill 文件。例如当你要求 Claude Code：

- 创建一个 3D 场景 → 会加载 `threejs-fundamentals`
- 添加灯光和阴影 → 会加载 `threejs-lighting`
- 加载一个 GLTF 模型 → 会加载 `threejs-loaders`
- 创建自定义视觉效果 → 会加载 `threejs-shaders` 和 `threejs-postprocessing`

## 使用示例

### 基础场景搭建

你可以这样问 Claude Code：

> “创建一个带旋转立方体的基础 Three.js 场景”

Claude Code 会使用 `threejs-fundamentals` 生成准确的样板代码，包括正确的渲染器初始化、动画循环和窗口尺寸变化处理。

### 加载 3D 模型

你可以这样问 Claude Code：

> “加载一个带 Draco 压缩的 GLTF 模型并播放它的动画”

Claude Code 会使用 `threejs-loaders` 和 `threejs-animation` 生成代码，并正确配置加载器、动画混合器以及错误处理逻辑。

### 自定义着色器

你可以这样问 Claude Code：

> “创建一个带菲涅尔效果的自定义 shader material”

Claude Code 会使用 `threejs-shaders` 生成可运行的 GLSL 代码，并正确处理 uniform 声明与坐标空间。

## Skill 文件结构

每个 skill 文件都遵循统一格式：

```markdown
---
name: skill-name
description: 该 skill 应在什么场景下激活
---

# Skill 标题

## Quick Start

[最小可运行示例]

## Core Concepts

[带示例的详细 API 说明]

## Common Patterns

[真实场景中的常用模式]

## Performance Tips

[性能优化建议]

## See Also

[相关 skill]
```

## 校验说明

这些 skill 已根据官方 Three.js 文档（r160+）进行审查，确保以下内容准确：

- 正确的类名与构造函数签名
- 有效的属性名与方法签名
- 准确的导入路径（`three/addons/` 格式）
- 可运行的代码示例
- 当前推荐的最佳实践

## 贡献指南

如果你发现错误，或者想为更多 Three.js 特性补充文档：

1. Fork 此仓库
2. 编辑或新增 `.claude/skills/` 中的 skill 文件
3. 对照 [Three.js documentation](https://threejs.org/docs/) 进行核验
4. 提交 Pull Request

### Skill 文件编写建议

- 使用准确且经过验证的代码示例
- 同时包含简单模式与进阶模式
- 说明性能影响
- 为相关 skill 添加交叉引用
- 示例保持简洁但完整

## 许可证

MIT License - 可自由使用、修改与分发。

## 鸣谢

- [Three.js](https://threejs.org/) - 本技能文档所围绕的 3D 库
