# 菠萝果冻 Pineapple Jelly

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110744617918304744) · [提示词帖](https://x.com/vib3coded/status/2110744893295386702) · 2026-10-15（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![菠萝果冻 Pineapple Jelly](../assets/pineapple-jelly.jpg)

## 提示词（英文原文）

```text
Build "Pineapple Jelly" — a single self-contained HTML file (inline JS/CSS, no libraries): a real-time WebGPU soft-body gummy pineapple ring with a real hole. The user can grab its outer or inner edge, stretch it, flip it over and let it wobble.

Object
- A thick canned-pineapple ring: outer radius 1.36, hole radius 0.5, thickness 0.5.
- Every edge rounded (bevel 0.12); 14 shallow scallops around the outer edge.
- Zones from rest-space coordinates, so they deform with the body. Both faces carry the same detail.
- A paler, denser core ring around the hole and a slightly deeper rim.
- Radial fibres: long thin streaks from core to rim, plus finer threads.
- The fibrous "eyes" band just inside the rim, where the flesh is most textured.
- Embedded juice cells (elongated pale sacs lying along the radius) and a few air bubbles that ride with the flesh.
- Tints: Golden, Amber, Rosé. Only the colour changes; scattering, gloss and fibres stay the same.

Physics (XPBD tetrahedral soft body)
- Mesh: 2D Delaunay of the scalloped annulus (outline samples plus a hex lattice; holes skipped), extruded into prisms → tets.
- Co-rotational per-tet shape matching (warm-started quaternion), so inverted tets recover; tet volume constraints for near-incompressibility; hard edge strain limits.
- Relative-velocity damping along edges; floor contact with Coulomb friction.
- Grab:
  - a soft patch attachment with bounded reach that never crushes the held patch into the floor;
  - the ray-pick knows when it passes through the empty hole;
  - scroll or a second finger twists the held patch.
- "Turn it over" tosses the ring with a spin about the screen's horizontal axis, so it flips and lands on its other face.
- Fixed 60 Hz step, small substeps (1 iteration each), gentle settling.
- The frame loop reuses every array (no per-frame allocation).

Rendering (WebGPU / WGSL)
- Passes: key-light shadow map; top-down height map for contact AO; scene (floor, juice cells, bubbles; MSAA); jelly back-face depth; jelly (refraction and absorption; MSAA) plus an optional mesh overlay; tone map.
- Procedural photo-studio cyclorama with softboxes. Soft PCSS key shadow tinted by the jelly.
- Jelly:
  - refraction of the scene by view-ray thickness;
  - per-tap Beer–Lambert absorption, denser and milkier in the core and fibres;
  - back-lit glow at thin edges, Fresnel studio reflections and GGX highlights.
- Post: exposure, Khronos PBR Neutral tone mapping, sRGB, dither.

UI (editorial "Material Studies / No. 012", English)
- Italic serif title "Pineapple / Jelly." and hint "Grab either edge. Pull. Let go."
- Panel "The Specimen": Tint swatches (tiny pineapple-ring icons); Firmness and Internal damping sliders; Give it a nudge, Turn it over, Reset, Pause; Show mesh and ¼ speed.
- Keys: Space to pause, N to nudge, T to turn it over, R to reset.
- Readouts: Mass (g, 1 unit ≈ 3 cm at 1.3 g/cm³), Volume (% of rest), Kinetic.
- Fallback screen when WebGPU is missing. Responsive stacked layout on mobile with no horizontal scroll.
```

---

## 提示词（中文）

构建 "Pineapple Jelly"（菠萝果冻）——一个单文件自包含 HTML（内联 JS/CSS，无第三方库）：一个带真实中孔的实时 WebGPU 软体软糖菠萝圈。用户可以抓住它的外缘或内缘，拉伸它，把它翻面，让它晃动。

### 物体

- 一个厚厚的罐头菠萝圈：外半径 1.36，孔半径 0.5，厚度 0.5。
- 所有边都倒圆（倒角 0.12）；外缘一圈 14 个浅扇贝形起伏。
- 各区域由静止空间坐标决定，所以会随物体一起变形。两面带有相同的细节。
- 孔周围一圈颜色更浅、更致密的芯环，以及一圈颜色稍深的外缘。
- 放射状纤维：从芯到外缘的细长条纹，外加更细的丝。
- 紧贴外缘内侧的纤维状"果眼"带，这里的果肉纹理最丰富。
- 嵌入的汁胞（沿半径方向躺着的细长浅色小囊）和几个随果肉移动的气泡。
- 色调：Golden（金黄）、Amber（琥珀）、Rosé（玫瑰）。只改变颜色；散射、光泽和纤维保持不变。

### 物理（XPBD 四面体软体）

- 网格：对扇贝形圆环做二维 Delaunay 剖分（轮廓采样点 + 六边形晶格；跳过孔），挤出成棱柱 → 四面体。
- 每个四面体的共旋转形状匹配（热启动四元数），使翻转的四面体能够恢复；四面体体积约束实现近似不可压缩；硬性的边应变限制。
- 沿边的相对速度阻尼；带库仑摩擦的地面接触。
- 抓取：
  - 柔性区域附着，拉伸距离有上限，绝不把被抓住的区域压进地面；
  - 射线拾取能识别何时穿过了中间的空孔；
  - 滚轮或第二根手指扭转被抓住的区域。
- "Turn it over"（翻面）把圆环绕屏幕水平轴旋转着抛起，让它翻过来以另一面落地。
- 固定 60 Hz 步长，小子步（每步 1 次迭代），温和的稳定处理。
- 帧循环复用所有数组（不做逐帧内存分配）。

### 渲染（WebGPU / WGSL）

- 渲染通道：主光阴影贴图；用于接触 AO 的俯视高度图；场景（地面、汁胞、气泡；MSAA）；果冻背面深度；果冻（折射和吸收；MSAA）加可选的网格叠加；色调映射。
- 带柔光箱的程序化摄影棚无缝背景。柔和的 PCSS 主光阴影带果冻色调。
- 果冻：
  - 按视线方向厚度折射场景；
  - 每次采样做 Beer–Lambert 吸收，在芯和纤维处更致密、更乳白；
  - 薄边缘的背光辉光、菲涅尔摄影棚反射和 GGX 高光。
- 后处理：曝光、Khronos PBR Neutral 色调映射、sRGB、抖动。

### UI（编辑风格 "Material Studies / No. 012"，英文）

- 斜体衬线标题 "Pineapple / Jelly."，提示 "Grab either edge. Pull. Let go."
- 面板 "The Specimen"：色调色板（小菠萝圈图标）；Firmness 和 Internal damping 滑块；Give it a nudge、Turn it over、Reset、Pause；Show mesh 和 ¼ speed。
- 按键：空格暂停，N 推一下，T 翻面，R 重置。
- 读数：Mass（g，1 单位 ≈ 3 cm，密度 1.3 g/cm³）、Volume（静止体积的百分比）、Kinetic。
- 缺少 WebGPU 时显示降级页面。移动端为响应式堆叠布局，无横向滚动。
