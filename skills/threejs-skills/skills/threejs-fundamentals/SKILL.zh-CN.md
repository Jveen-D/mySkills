---
name: threejs-fundamentals
description: Three.js 基础：场景搭建、相机、渲染器、Object3D 层级与坐标系统。适用于搭建 3D 场景、创建相机、配置渲染器、管理对象层级或处理变换相关任务。
---

# Three.js 基础

## Quick Start

```javascript
import * as THREE from "three";

// 创建场景、相机、渲染器
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000,
);
const renderer = new THREE.WebGLRenderer({ antialias: true });

renderer.setSize(window.innerWidth, window.innerHeight);
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
document.body.appendChild(renderer.domElement);

// 添加网格
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshStandardMaterial({ color: 0x00ff00 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);

// 添加光源
scene.add(new THREE.AmbientLight(0xffffff, 0.5));
const dirLight = new THREE.DirectionalLight(0xffffff, 1);
dirLight.position.set(5, 5, 5);
scene.add(dirLight);

camera.position.z = 5;

// 动画循环
function animate() {
  requestAnimationFrame(animate);
  cube.rotation.x += 0.01;
  cube.rotation.y += 0.01;
  renderer.render(scene, camera);
}
animate();

// 处理窗口尺寸变化
window.addEventListener("resize", () => {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
});
```

## 核心类

### Scene

所有 3D 对象、灯光和相机的容器。

### Cameras

- **PerspectiveCamera**：最常用，模拟人眼透视。
- **OrthographicCamera**：无透视形变，适合 2D / 等距视角。
- **ArrayCamera**：多个子相机对应多个视口。
- **CubeCamera**：用于反射和环境贴图渲染。

### WebGLRenderer

用于将场景渲染到画布，常见关注点包括：
- 抗锯齿、透明背景、性能偏好
- `setSize()` 与 `setPixelRatio()`
- 色调映射与输出色彩空间
- 阴影开关与阴影类型

### Object3D

所有 3D 对象的基类，核心概念包括：
- 位置、旋转、缩放
- 本地坐标与世界坐标
- 父子层级管理
- `visible`、`layers`、`traverse()`
- 矩阵自动更新与手动更新

### Group

空容器，用于组织多个对象并整体变换。

### Mesh

几何体与材质的组合，是最常见的可渲染对象。

## 坐标系统

Three.js 使用 **右手坐标系**：

- **+X** 向右
- **+Y** 向上
- **+Z** 朝向观察者（屏幕外）

## 使用建议

当你在以下场景工作时，应优先使用本 skill：
- 创建 Three.js 基础场景
- 配置相机和渲染器
- 组织 `Object3D` 层级
- 处理坐标、变换与动画循环

## 说明

此 skill 原文包含大量 API 示例代码。为了先完成仓库中文化，这里优先将标题、用途与关键概念翻译为中文，并保留可运行示例代码不变。
