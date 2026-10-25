# 柑橘果冻 Citrus Jelly

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109424502237016076) · [提示词帖](https://x.com/vib3coded/status/2109424651340284152) · 2026-10-12（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![柑橘果冻 Citrus Jelly](../assets/citrus-jelly.jpg)

## 提示词（英文原文）

```text
Build "Citrus Jelly" — a single self-contained HTML file (inline JS/CSS, no libraries) with a real-time WebGPU soft-body jelly shaped like a half-moon citrus slice that the user can grab, stretch and let go.

Object
- A rounded half-moon slice: half-disk profile extruded into a thick slab with softly rounded edges; flat cut edge on the bottom, arc on top.
- Three material zones by radius: translucent fruit flesh inside, a pale pith band, and a thin glossy rind along the arc (the cut edge is all flesh).
- Inside the jelly: thin milky radial membranes between the segments (inset from both faces), a few seeds, small air bubbles with a faint rim and a pin-point highlight, and tiny sub-surface glints like sugar crystals.

Physics (XPBD tetrahedral soft body)
- Mesh: 2D Bowyer–Watson Delaunay of the profile, extruded into prisms and split into tets. Render mesh embedded in sim tets with barycentric coordinates.
- Constraints:
  - co-rotational per-tet shape matching (warm-started quaternion, Müller 2016), which recovers inverted tets;
  - tet volume constraints for near-incompressibility;
  - hard edge strain limits (max 1.8×, min 0.35× rest length).
- Fixed timestep, "small steps" XPBD (many substeps, 1 iteration each).
- Damping: relative-velocity damping along edges, light air drag, and settling that bleeds off residual jitter.
- Floor contact with Coulomb-style positional friction (static and kinetic). Never crush the held patch into the floor; lift the patch instead.
- Grab and pull:
  - pick a surface point with the mouse or touch;
  - the patch around it is attached softly;
  - reach is bounded, so stretching is strong but never unbounded;
  - on release the slice wobbles back.
- Safety: reset gently if any value becomes NaN.

Rendering (WebGPU / WGSL)
- Procedural photo studio: pale cyclorama paper sweep, overhead softbox, back-left strip light, front-right fill card.
- Jelly material:
  - refraction of the scene through the slice;
  - view-ray thickness from a back-face depth pass, used for Beer–Lambert absorption;
  - Fresnel studio reflections and a key highlight.
- Soft PCSS-style floor shadows, tinted by the jelly color.
- Post: exposure, Khronos PBR Neutral tone mapping, sRGB, dither. Optional mesh-overlay debug view.

UI (minimal editorial style, English)
- Corner label "Material Studies / No. 010", big title "Citrus / Jelly.", hint "Grab. Stretch. Let go."
- Variety swatches: Orange, Blood Orange, Lemon. Each changes the flesh, pith and rind colors.
- Sliders: Firmness (log-mapped edge compliance) and Internal damping.
- Buttons:
  - "Give it a nudge": a small hop with a twist;
  - Reset;
  - Pause.
- Keys: Space to pause, N to nudge, R to reset.
- Fallback screen "This slice needs WebGPU." when the browser has no WebGPU.
- Responsive: works on mobile with touch and no horizontal scroll.
```

---

## 提示词（中文）

构建 "Citrus Jelly"（柑橘果冻）——一个单文件自包含 HTML（内联 JS/CSS，无第三方库），包含一个实时 WebGPU 软体果冻，形状像半月形柑橘切片，用户可以抓住、拉伸再松开。

### 物体

- 一块圆润的半月形切片：半圆轮廓挤出成厚板，边缘柔和圆润；底部是平直的切边，顶部是圆弧。
- 按半径分三个材质区：内部是半透明果肉，中间一条浅色白皮（pith）带，沿圆弧是一层薄而有光泽的果皮（切边处全是果肉）。
- 果冻内部：瓣与瓣之间有细细的乳白色放射状隔膜（距两个表面都有内缩），几粒籽，带淡淡边缘和针尖高光的小气泡，以及像糖晶一样的细小次表面闪光。

### 物理（XPBD 四面体软体）

- 网格：对轮廓做二维 Bowyer–Watson Delaunay 三角剖分，挤出成棱柱并切分为四面体。渲染网格用重心坐标嵌入模拟四面体中。
- 约束：
  - 每个四面体的共旋转（co-rotational）形状匹配（热启动四元数，Müller 2016），可以恢复翻转的四面体；
  - 四面体体积约束，实现近似不可压缩；
  - 硬性的边应变限制（最大 1.8×，最小 0.35× 静止长度）。
- 固定时间步长，"small steps" XPBD（多子步，每步 1 次迭代）。
- 阻尼：沿边的相对速度阻尼、轻微空气阻力，以及消除残余抖动的稳定处理。
- 地面接触，带库仑式位置摩擦（静摩擦和动摩擦）。绝不要把被抓住的区域压进地面；而是把该区域抬起来。
- 抓取和拉动：
  - 用鼠标或触摸选中表面上的一点；
  - 其周围的一块区域被柔性附着；
  - 拉伸距离有上限，所以拉伸很强但不会无限；
  - 松手后切片晃动着恢复。
- 安全：任何数值变成 NaN 时温和地重置。

### 渲染（WebGPU / WGSL）

- 程序化摄影棚：浅色无缝纸背景（cyclorama），顶部柔光箱，左后方灯条，右前方补光板。
- 果冻材质：
  - 场景透过切片的折射；
  - 由背面深度通道得到的视线方向厚度，用于 Beer–Lambert 吸收；
  - 菲涅尔摄影棚反射和主光高光。
- 柔和的 PCSS 风格地面阴影，带果冻颜色的色调。
- 后处理：曝光、Khronos PBR Neutral 色调映射、sRGB、抖动。可选的网格叠加调试视图。

### UI（极简编辑风格，英文）

- 角落标签 "Material Studies / No. 010"，大标题 "Citrus / Jelly."，提示 "Grab. Stretch. Let go."
- 品种色板：Orange（橙）、Blood Orange（血橙）、Lemon（柠檬）。每个都改变果肉、白皮和果皮的颜色。
- 滑块：Firmness（对数映射的边柔度）和 Internal damping（内部阻尼）。
- 按钮：
  - "Give it a nudge"：带扭转的小跳；
  - Reset；
  - Pause。
- 按键：空格暂停，N 推一下，R 重置。
- 浏览器没有 WebGPU 时显示降级页面 "This slice needs WebGPU."。
- 响应式：在移动端支持触摸，无横向滚动。
