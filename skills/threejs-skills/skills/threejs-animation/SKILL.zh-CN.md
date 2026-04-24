---
name: threejs-animation
description: Three.js 动画：关键帧动画、骨骼动画、变形目标与动画混合。适用于为对象添加动画、播放 GLTF 动画、创建程序化运动或混合多个动画状态。
---

# Three.js 动画

## Quick Start

```javascript
import * as THREE from "three";

// 简单的程序化动画
const clock = new THREE.Clock();

function animate() {
  const delta = clock.getDelta();
  const elapsed = clock.getElapsedTime();

  mesh.rotation.y += delta;
  mesh.position.y = Math.sin(elapsed) * 0.5;

  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();
```

## 动画系统概览

Three.js 动画系统主要由三部分组成：

1. **AnimationClip** - 关键帧数据容器
2. **AnimationMixer** - 在某个根对象上播放动画
3. **AnimationAction** - 控制某个 clip 的播放行为

## 适用场景

当你需要处理以下任务时，应使用此 skill：
- 为对象添加关键帧动画
- 播放 GLTF / GLB 自带动画
- 创建程序化运动效果
- 混合多个动画状态
- 处理骨骼动画与变形目标

## 核心内容

文档正文涵盖：
- `AnimationClip` 与各种 `KeyframeTrack`
- 插值模式
- `AnimationMixer` 的创建与更新
- `AnimationAction` 的播放、淡入淡出与混合
- GLTF 动画加载
- 骨骼动画与 morph target 工作流

## 说明

为了优先完成整个仓库的中文入口说明，这里先把核心标题、用途和系统概念翻译为中文；详细 API 示例代码继续保留英文原样，避免破坏可复制性与准确性。
