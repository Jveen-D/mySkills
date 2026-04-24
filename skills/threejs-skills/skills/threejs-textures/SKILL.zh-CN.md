---
name: threejs-textures
description: Three.js 纹理：纹理类型、UV 映射、环境贴图与纹理配置。适用于处理图片、UV 坐标、立方体贴图、HDR 环境贴图或纹理优化相关任务。
---

# Three.js 纹理

## Quick Start

```javascript
import * as THREE from "three";

// 加载纹理
const loader = new THREE.TextureLoader();
const texture = loader.load("texture.jpg");

// 应用到材质
const material = new THREE.MeshStandardMaterial({
  map: texture,
});
```

## 适用场景

当你处理以下任务时，应使用此 skill：
- 给模型加载与配置纹理
- 处理 UV 映射
- 使用环境贴图、HDR 纹理或立方体贴图
- 配置纹理重复、偏移、旋转、过滤方式
- 优化纹理质量与渲染性能

## 核心主题

本 skill 主要覆盖：
- 纹理加载与 Promise 封装
- 色彩空间与过滤方式
- wrapping / repeat / offset / rotation
- 普通纹理、数据纹理、Canvas 纹理、视频纹理、压缩纹理
- 环境贴图、HDR、render target、CubeCamera
- UV 映射与贴图优化

## 说明

这里先把标题、用途与关键模块翻译成中文，详细代码示例保留英文原样，以确保 API 精确度与可复制性。
