---
name: threejs-interaction
description: Three.js 交互：射线投射、控制器、鼠标/触摸输入与对象选择。适用于处理用户输入、实现点击检测、添加相机控制或构建交互式 3D 体验。
---

# Three.js 交互

## Quick Start

```javascript
import * as THREE from "three";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";

// 相机控制
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;

// 用射线检测点击
const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();

function onClick(event) {
  mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
  mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

  raycaster.setFromCamera(mouse, camera);
  const intersects = raycaster.intersectObjects(scene.children);

  if (intersects.length > 0) {
    console.log("Clicked:", intersects[0].object);
  }
}

window.addEventListener("click", onClick);
```

## 适用场景

当你需要以下能力时，应使用此 skill：
- 鼠标或触摸交互
- 物体点击、悬停、选择
- 射线投射与拾取
- 相机控制器接入
- 可编辑或可拖拽的 3D 交互体验

## 核心主题

此 skill 覆盖：
- `Raycaster` 的基础用法与优化方式
- 鼠标 / 触摸坐标转换
- `OrbitControls`、`FlyControls`、`PointerLockControls` 等常见控制器
- `TransformControls` 与 `DragControls`
- 场景中的拾取、拖拽与交互响应

## 说明

为优先完成中文入口层，这里先翻译标题、用途与关键模块说明；详细代码示例保留英文原样，确保和 Three.js API 一致。
