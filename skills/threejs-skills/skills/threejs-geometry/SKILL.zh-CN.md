---
name: threejs-geometry
description: Three.js 几何体：内置形状、BufferGeometry、自定义几何体与实例化渲染。适用于创建 3D 形状、处理顶点数据、构建自定义网格或通过实例化优化性能。
---

# Three.js 几何体

## Quick Start

```javascript
import * as THREE from "three";

// 内置几何体
const box = new THREE.BoxGeometry(1, 1, 1);
const sphere = new THREE.SphereGeometry(0.5, 32, 32);
const plane = new THREE.PlaneGeometry(10, 10);

// 创建网格
const material = new THREE.MeshStandardMaterial({ color: 0x00ff00 });
const mesh = new THREE.Mesh(box, material);
scene.add(mesh);
```

## 适用场景

当你需要处理以下内容时，请使用此 skill：
- 创建基础或复杂 3D 形状
- 操作顶点、法线、UV 与索引
- 编写自定义 `BufferGeometry`
- 使用实例化渲染优化大量重复网格

## 核心主题

本 skill 主要覆盖：
- 内置几何体（立方体、球体、平面、圆柱、圆环等）
- 路径类几何体（Lathe、Extrude、Tube）
- 文本几何体
- `BufferGeometry` 与 `BufferAttribute`
- 点、线、线框与边缘几何体
- 自定义几何体与高性能布局

## 说明

为保证仓库先完成整体中文化，这里优先翻译标题、用途和核心说明；下方详细 API 代码示例保持英文原文，方便直接复制使用。
