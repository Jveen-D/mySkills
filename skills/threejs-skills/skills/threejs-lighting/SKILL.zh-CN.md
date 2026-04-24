---
name: threejs-lighting
description: Three.js 灯光：灯光类型、阴影与环境光照。适用于添加灯光、配置阴影、搭建 IBL 环境光照或优化灯光性能。
---

# Three.js 灯光

## Quick Start

```javascript
import * as THREE from "three";

// 基础灯光配置
const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
scene.add(ambientLight);

const directionalLight = new THREE.DirectionalLight(0xffffff, 1);
directionalLight.position.set(5, 5, 5);
scene.add(directionalLight);
```

## 适用场景

当你在以下场景工作时，应使用此 skill：
- 为场景添加灯光
- 配置阴影质量与范围
- 搭建环境光照 / IBL
- 调整灯光性能与视觉质量的平衡

## 核心主题

本 skill 主要覆盖：
- 各类灯光：`AmbientLight`、`HemisphereLight`、`DirectionalLight`、`PointLight`、`SpotLight`、`RectAreaLight`
- 阴影启用方式与优化策略
- 灯光辅助对象（helpers）
- HDR 环境贴图与基于图像的光照（IBL）
- 更高级的光照探针与调试手段

## 说明

这里先完成标题、适用范围和主要内容的中文翻译，详细 API 示例与参数说明仍保留原文代码，便于直接使用。
