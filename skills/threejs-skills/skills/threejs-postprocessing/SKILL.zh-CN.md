---
name: threejs-postprocessing
description: Three.js post-processing - EffectComposer, bloom, DOF, screen effects. Use when adding visual effects, color grading, blur, glow, or creating custom screen-space shaders.
---

# Three.js 后处理

## Quick Start

```javascript
import * as THREE from "three";
import { EffectComposer } from "three/addons/postprocessing/EffectComposer.js";
import { RenderPass } from "three/addons/postprocessing/RenderPass.js";
import { UnrealBloomPass } from "three/addons/postprocessing/UnrealBloomPass.js";

// 配置 composer
const composer = new EffectComposer(renderer);

// 渲染场景
const renderPass = new RenderPass(scene, camera);
composer.addPass(renderPass);

// 添加 bloom
const bloomPass = new UnrealBloomPass(
  new THREE.Vector2(window.innerWidth, window.innerHeight),
  1.5,
  0.4,
  0.85,
);
composer.addPass(bloomPass);

function animate() {
  requestAnimationFrame(animate);
  composer.render();
}
```

## 适用场景

当你需要以下效果时，应使用此 skill：
- Bloom / Glow
- 景深（DOF）
- 抗锯齿、暗角、颗粒、故障风格等屏幕特效
- 颜色校正与风格化渲染
- 自定义屏幕后处理着色器

## 核心主题

本 skill 主要覆盖：
- `EffectComposer` 与基础 Pass 组织方式
- 常见效果：Bloom、FXAA、SMAA、SSAO、DOF、Film、Vignette、Outline 等
- 自定义 `ShaderPass`
- 尺寸变化处理与渲染链顺序
- 性能与画质之间的平衡

## 说明

为优先完成整体中文化，这里先翻译标题、用途和模块概览；详细的 API 示例代码仍保留英文原文。
