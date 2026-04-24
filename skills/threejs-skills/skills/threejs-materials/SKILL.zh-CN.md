---
name: threejs-materials
description: Three.js 材质：PBR、基础材质、Phong 材质、着色器材质与材质属性。适用于设置网格外观、处理纹理、编写自定义着色器或优化材质性能。
---

# Three.js 材质

## Quick Start

```javascript
import * as THREE from "three";

// PBR 材质（推荐用于真实感渲染）
const material = new THREE.MeshStandardMaterial({
  color: 0x00ff00,
  roughness: 0.5,
  metalness: 0.5,
});

const mesh = new THREE.Mesh(geometry, material);
```

## 适用场景

当你需要以下能力时，应使用此 skill：
- 为模型设置不同材质外观
- 使用颜色贴图、法线贴图、粗糙度贴图等纹理
- 在 PBR 与非 PBR 材质之间做选择
- 编写自定义 `ShaderMaterial`
- 优化材质质量与性能

## 核心主题

本 skill 涵盖：
- `MeshBasicMaterial`、`MeshLambertMaterial`、`MeshPhongMaterial`
- `MeshStandardMaterial` 与 `MeshPhysicalMaterial`
- Toon、Normal、Depth、Points、Line 等特殊材质
- `ShaderMaterial` 与 `RawShaderMaterial`
- 材质常见属性、透明度、双面渲染、环境反射等

## 说明

当前先完成中文标题、用途和模块说明，保留详细英文示例代码，以保证术语和 API 可直接使用。
