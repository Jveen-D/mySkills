---
name: threejs-loaders
description: Three.js 资源加载：GLTF、纹理、图片、模型与异步加载模式。适用于加载 3D 模型、纹理、HDR 环境贴图或管理资源加载进度。
---

# Three.js 加载器

## Quick Start

```javascript
import * as THREE from "three";
import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";

// 加载 GLTF 模型
const loader = new GLTFLoader();
loader.load("model.glb", (gltf) => {
  scene.add(gltf.scene);
});

// 加载纹理
const textureLoader = new THREE.TextureLoader();
const texture = textureLoader.load("texture.jpg");
```

## 适用场景

当你需要处理以下内容时，应使用此 skill：
- 加载 GLTF / GLB 模型
- 加载纹理、HDR、EXR、环境贴图
- 统一管理多个资源的加载进度
- 接入 Draco、KTX2 等压缩资源工作流
- 对已加载模型进行遍历、归一化和后处理

## 核心主题

本 skill 覆盖：
- `LoadingManager`
- 纹理加载与配置
- HDR / EXR 与 `PMREMGenerator`
- GLTF / GLB 及其扩展格式支持
- OBJ / FBX / STL / PLY 等模型格式
- 异步资源加载与错误处理模式

## 说明

这里优先完成中文入口翻译，帮助你快速知道每个 loader skill 负责什么；详细 API 代码示例继续保留英文原样。
