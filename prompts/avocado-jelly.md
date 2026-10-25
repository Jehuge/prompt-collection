# 牛油果果冻 Avocado Jelly

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 刚体果核
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `刚体` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2112128541022114137) · [提示词帖](https://x.com/vib3coded/status/2112128796505624621) · 2026-10-19（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![牛油果果冻 Avocado Jelly](../assets/avocado-jelly.jpg)

## 提示词（英文原文）

```text
Build a single-file WebGPU page "Avocado Jelly" in the style of a "Material Studies" specimen sheet (light studio backdrop #E2DFDA, italic serif title, a specimen control panel on the right, live readouts bottom-left, collapsible "Inside the experiment" notes; fully responsive with a stacked phone layout and a no-WebGPU fallback card).

Subject: half an avocado made of translucent jelly, lying skin-down on a table, cut face up, with its pit seated in the hollow.

Geometry: define the fruit as a signed distance field — a smooth pear of revolution along x (round body + narrower neck, smooth-min blended, cross-section slightly flattened, belly gently flattened on the floor), cut at the axis plane, minus an egg-shaped hollow for the pit (two half-ellipsoids, a little longer toward the neck). Build the simulation mesh as a hex lattice (5 tets per cell, ~800 particles / ~2400 tets) with node layers exactly on the floor and the cut face, boundary nodes snapped onto the surface (back off where tets would invert, force nodes out of the pit). Render surface via surface nets (~0.03 spacing), embedded in the tets with barycentric weights.

Physics (CPU, XPBD, 60 Hz, 10 substeps): per-tet co-rotational shape matching + volume constraints, stiffer leathery skin, edge-relative damping, floor contact with friction, soft pointer grab with twist (wheel / second finger). The pit is a true rigid body (position, quaternion, ellipsoid inertia): frictional contact with every particle, floor contact through ~70 sampled surface points so it rolls and stops. The hollow's lining nodes are held to the pit by soft adhesion bonds. Release them by a sustained net pull (fatigue on the lining's net force, measured in the half's best-fit rigid frame), peeling from the floor of the hollow up to the lip, so the flesh clings, stretches, then lets go and snaps back; brief knocks and wobbles must not release it. A loose pit that settles near its hollow is drawn home and re-bonded with a short soft grace period. Grabbing the pit moves it as a whole (no pivoting); it can be thrown. Buttons: "Give it a nudge", "Reset", "Pop the pit" (tosses it onto the table toward the viewer) / "Put the pit back" (carries it along an arc and drops it in), Pause, ¼ speed, Show mesh, sliders for firmness and internal damping. Readouts: mass, volume % of rest, grip % (share of bonds holding).

Rendering (WGSL): shadow map + top-down height map for contact AO; a scene pass (floor, pit, a few bubbles) whose alpha stores linear depth; a back-face pass for view-ray thickness; jelly front faces that refract the scene by that thickness with Beer–Lambert absorption and scattering. Flesh regions from rest-space SDFs: dark pebbled skin (derivative bump mapping, anti-aliased), an emerald band under the skin, vivid green fading to a milky butter-yellow heart around the pit, faint strands, glints, back-lit edge glow, Fresnel studio reflections and GGX highlights. The pit: tan core under a papery brown coat with fibres and a faint seam, soft key shadows, a moist sheen. Three varieties: Hass, Fuerte, Reed. UI text in English.
```

---

## 提示词（中文）

构建一个单文件 WebGPU 页面 "Avocado Jelly"（牛油果果冻），采用 "Material Studies" 标本页的风格（浅色摄影棚背景 #E2DFDA，斜体衬线标题，右侧标本控制面板，左下实时读数，可折叠的 "Inside the experiment" 说明；完全响应式，手机上为堆叠布局，没有 WebGPU 时显示降级卡片）。

### 主体

由半透明果冻做成的半个牛油果，果皮朝下躺在桌上，切面朝上，果核嵌在凹窝里。

### 几何

把果实定义为一个有向距离场——沿 x 轴的光滑梨形旋转体（圆润的主体 + 较窄的颈部，用 smooth-min 混合，横截面略扁，腹部轻轻压平贴在地面上），在轴平面处切开，再减去一个容纳果核的蛋形凹窝（两个半椭球，朝颈部方向稍长一些）。把模拟网格构建为六面体晶格（每个单元 5 个四面体，约 800 个粒子 / 约 2400 个四面体），并让节点层恰好位于地面和切面上，边界节点吸附到表面（在四面体会翻转的地方退回，强制节点离开果核区域）。渲染表面用 surface nets（间距约 0.03），通过重心权重嵌入四面体中。

### 物理（CPU，XPBD，60 Hz，10 个子步）

- 每个四面体的共旋转形状匹配 + 体积约束，果皮更硬、有皮革感，基于边的相对阻尼，带摩擦的地面接触，柔性指针抓取并支持扭转（滚轮 / 第二根手指）。
- 果核是真正的刚体（位置、四元数、椭球惯量）：与每个粒子都有带摩擦的接触，通过约 70 个采样表面点与地面接触，所以它会滚动并停下。
- 凹窝内衬的节点通过柔性黏附键与果核相连。只有持续的净拉力才能使其脱开（对内衬所受净力做"疲劳"累积，在这半个牛油果的最佳拟合刚体坐标系中测量），从凹窝底部一直剥离到边缘，于是果肉会粘着、拉伸，然后松开并弹回；短暂的磕碰和晃动不得使其脱开。
- 一颗松开的果核如果停在凹窝附近，会被吸回原位，并在一个短暂的柔性宽限期后重新黏合。
- 抓住果核会整体移动它（不绕支点转动）；它可以被扔出去。
- 按钮："Give it a nudge"、"Reset"、"Pop the pit"（把果核朝观众方向抛到桌上）/ "Put the pit back"（沿弧线带回来放进凹窝）、Pause、¼ speed、Show mesh，以及硬度和内部阻尼滑块。
- 读数：质量、相对静止状态的体积百分比、grip %（仍在起作用的黏附键比例）。

### 渲染（WGSL）

- 阴影贴图 + 用于接触 AO 的俯视高度图；一个场景通道（地面、果核、几个气泡），其 alpha 存储线性深度；一个用于视线方向厚度的背面通道；果冻正面按该厚度折射场景，带 Beer–Lambert 吸收和散射。
- 果肉区域由静止空间的 SDF 决定：深色、带颗粒疙瘩的果皮（导数凹凸贴图，抗锯齿），果皮下方一条祖母绿色带，鲜绿色逐渐过渡到果核周围乳白的黄油色果心，淡淡的纤维丝，闪光，背光边缘辉光，菲涅尔摄影棚反射和 GGX 高光。
- 果核：棕褐色内核，外面包着一层纸质的棕色种皮，带纤维和一条淡淡的接缝，柔和的主光阴影，湿润的光泽。
- 三个品种：Hass、Fuerte、Reed。界面文字为英文。
