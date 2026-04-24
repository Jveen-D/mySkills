---
name: threejs-shaders
description: Three.js 着色器：GLSL、ShaderMaterial、uniform 与自定义效果。适用于创建自定义视觉效果、修改顶点、编写片元着色器或扩展内置材质。
---

# Three.js 着色器

## Quick Start

```javascript
import * as THREE from "three";

const material = new THREE.ShaderMaterial({
  uniforms: {
    time: { value: 0 },
    color: { value: new THREE.Color(0xff0000) },
  },
  vertexShader: `
    void main() {
      gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
    }
  `,
  fragmentShader: `
    uniform vec3 color;

    void main() {
      gl_FragColor = vec4(color, 1.0);
    }
  `,
});

material.uniforms.time.value = clock.getElapsedTime();
```

## 适用场景

当你需要以下能力时，应使用此 skill：
- 编写自定义 GLSL 效果
- 修改顶点位置或表面外观
- 使用 `uniform`、`varying`、纹理采样等概念
- 扩展内置材质能力
- 实现菲涅尔、噪声、渐变、边缘光等视觉效果

## 核心主题

本 skill 主要覆盖：
- `ShaderMaterial` 与 `RawShaderMaterial` 的区别
- `uniform` 类型与传值方式
- `varying` 数据传递
- 常见着色器模式
- 顶点位移、纹理采样、噪声、渐变、边缘光等效果

## 说明

这里先完成中文入口说明，确保每个 shader 相关 skill 都能直接被中文用户理解；详细 GLSL 代码保留原文，方便复制与验证。
