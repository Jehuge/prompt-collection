# 柑橘果冻切割器 Citrus Jelly Cutters

- **类型**：交互网页 / 可切割软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · SDF 布尔切割
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `切割` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109687505679171955) · [提示词帖](https://x.com/vib3coded/status/2109687855123497136) · 2026-10-13（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来测试 AI 模型的提示词（帖子展示的是 Claude Opus 5.5 的结果）。这是在 [citrus-jelly](citrus-jelly.md) 基础上的升级版（作者让 Claude Opus 5.5 在原作上继续加功能），但提示词本身是完整独立的。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "Citrus Jelly Cutters"（柑橘果冻切割器）——一个单文件自包含 HTML（内联 JS/CSS，无第三方库）：一块实时 WebGPU 软体软糖橙子切片，你可以用手拉伸，用直刀或波浪形皱纹刀切开，还能用饼干模具压出形状。每一块都会变成独立的果冻体。

### 标本

- 一块厚实、圆润的半月形柑橘切片：
  - 外果皮、白色内皮（pith）、五瓣果肉配细细的乳白色隔膜、一个白色果芯、汁胞和几个气泡；
  - 圆角，以及倒角的上下边缘。
- 品种：Orange、Blood Orange、Lemon。

### 碎块（核心思路）

- 把每一块存为切片原始静止平面上的有向距离网格（0.01 分辨率）。所有碎块共享同一个静止坐标系，因此果皮、白皮、果瓣和隔膜都保持在它们原本在果实中的位置。
- 切割和压模是对该网格的布尔运算：
  - 用形态学闭运算再开运算（精确欧氏距离变换）把新转角倒圆，只作用在新切口附近，使旧特征得以保留；
  - 拆分为连通部分并丢弃碎屑。
- 每个部分获得一个新的四面体网格：
  - 对轮廓做 Delaunay 三角剖分（marching squares，重采样、平滑、投影回零等值面），加上内部晶格，挤出成棱柱 → 四面体；
  - 渲染网格包括圆润的侧壁、两个端面、内部的隔膜面，以及其中的气泡。
- 每个轮廓采样点的上下倒角受局部内切半径限制，使细长碎片和皱纹刀的凸棱保持干净。
- 每次切割后，新世界通过重心插值继承旧世界的位置和速度。碎块之间做粒子对粒子的排斥，所以它们永远不会互相穿透。

### 物理（XPBD）

- 每个四面体的共旋转形状匹配（热启动四元数）加体积约束，因此被拉伸的果冻会"缩颈"。
- 果皮和白皮更硬；边速度阻尼；带库仑摩擦的地面接触。
- 柔性的区域抓取，拉伸距离有上限。滚轮或第二根手指可以扭转被抓住的区域。
- 固定 60 Hz 步长，10 个子步。

### 工具（2×2 网格：Hand、Knife、Wavy knife、Cutter；快捷键 H、K、W、C，1–4 选择模具形状）

- Hand：抓住任意碎块拉动。
- Knife（菜切刀 nakiri，胡桃木刀柄）：
  - 在切片上画一道划痕；
  - 这道划痕在表面上读取，确定一个竖直的刀刃平面，并通过每个被穿过碎块的最佳拟合旋转带入其静止坐标系，于是变成一条线；
  - 松手时就预先构建好各碎块；
  - 动画：刀对准，压出一道凹槽（果冻被压扁），切穿（新碎块替换进来），一边向前切一边把切面楔开，然后抬起。
- Wavy knife（皱纹切刀，鼠尾草绿聚合物刀柄）：
  - 刀板按 A·sin(2π(x − xr)/λ) 起伏，A = 0.036，λ = 0.28；
  - 切割面 n·(X − o) = A·sin(2π d·(X − o)/λ) 被带入静止空间成为一条波浪线，倒圆半径很小（0.026）；
  - 刀刃竖直向下压（不滑动），其楔形跟随起伏；
  - 两个方向各切一次，就得到皱纹切丁。
- Cutter：Star（星）、Heart（心）、Flower（花）和 Round（圆）马口铁模具环，带卷边。
  - 点击一块平的碎块，把模具压穿。它把碎块分成内外两部分，侧壁被楔开，形状弹起以便取出。
- 最多 14 块。一个小提示解释没切中的情况（"Missed — draw the blade across the slice."）。

### 渲染（WebGPU / WGSL）

- 带柔光箱的程序化摄影棚无缝背景。柔和的 PCSS 主光阴影带果冻色调，另加由俯视高度图得到的接触 AO。
- 果冻：按视线方向厚度（背面深度通道）折射场景，Beer–Lambert 吸收，白皮中的乳白散射，薄边缘的背光辉光，菲涅尔摄影棚反射和 GGX 高光。
- 果皮、白皮、果瓣和汁胞根据静止空间坐标着色，所以新切开的面会显示真实的内部。
- 工具绘制在果冻表面后方，因此埋入的钢刃会以折射形式被看到：
  - 拉丝钢，带缎面刃口倒角和抛光刀枕；
  - 带铆钉的胡桃木刀柄；
  - 颗粒纹聚合物刀柄；
  - 马口铁模具环。
- 后处理：曝光、Khronos PBR Neutral 色调映射、sRGB、抖动。

### UI（编辑风格 "Material Studies / No. 010"，英文）

- 斜体衬线标题 "Citrus / Jelly."，说明文字 "Sunshine in segments. Soft enough to slice. Sweet enough to share."
- 状态胶囊 "WEBGPU · LIVE"。
- 面板 "The Specimen"：
  - 工具网格和模具形状；
  - 品种色板；
  - Firmness 和 Internal damping 滑块；
  - Give it a nudge、Reset、Pause；¼ speed 和 Show mesh。
- 读数：工具提示、Mass (g)、Volume（静止体积的百分比）、Kinetic (µJ)、Pieces（块数）。
- 可折叠的 "Inside the experiment"，说明四面体、切割、波浪刀、饼干模具、随动表面以及光在果冻中的传播。
- 降级页面 "This slice needs WebGPU."。移动端为堆叠布局，无横向滚动。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Citrus Jelly Cutters" — a single self-contained HTML file (inline JS/CSS, no libraries): a real-time WebGPU soft-body gummy orange slice you can stretch by hand, cut with a straight knife or a wavy crinkle knife, and stamp with cookie cutters. Every piece becomes its own jelly body.

Specimen
- A thick, rounded half-moon citrus slice:
  - zest rind, white pith, five segments with thin milky membranes, a pithy core, juice vesicles and a few air bubbles;
  - rounded corners and bevelled top/bottom edges.
- Varieties: Orange, Blood Orange, Lemon.

Pieces (the core idea)
- Store every piece as a signed-distance grid (0.01 resolution) over the slice's original rest plane. All pieces share one rest frame, so zest, pith, segments and membranes stay where they were in the fruit.
- Cuts and stamps are boolean operations on that grid:
  - round the new corners with a morphological closing then opening (exact Euclidean distance transform), applied only near the new cut so older features survive;
  - split into connected parts and drop crumbs.
- Each part gets a fresh tetrahedral mesh:
  - Delaunay of the outline (marching squares, resampled, smoothed, projected back onto the zero set) plus an interior lattice, extruded into prisms → tets;
  - a render mesh of rounded walls, two caps, the membrane spans inside it, and the bubbles inside it.
- The top/bottom bevel of each outline sample is limited by the local inscribed radius, so thin slivers and crinkle ridges stay clean.
- After each cut, the new world takes over positions and velocities from the old one by barycentric interpolation. Pieces repel each other particle-to-particle, so they never pass through one another.

Physics (XPBD)
- Co-rotational per-tet shape matching (warm-started quaternion) plus volume constraints, so stretched jelly necks in.
- Stiffer rind and pith; edge-velocity damping; floor contact with Coulomb friction.
- Soft patch grab with bounded reach. Scroll or a second finger twists the held patch.
- Fixed 60 Hz step with 10 substeps.

Tools (2×2 grid: Hand, Knife, Wavy knife, Cutter; keys H, K, W, C, and 1–4 for cutter shapes)
- Hand: grab any piece and pull.
- Knife (nakiri, walnut handle):
  - draw a stroke across the slice;
  - the stroke, read on the surface, fixes a vertical blade plane, carried into each crossed piece's rest frame via its best-fit rotation, so it becomes a line;
  - the pieces are prebuilt on release;
  - animation: the knife lines up, presses a groove (the jelly squashes), breaks through (the new pieces swap in), wedges the faces apart while slicing forward, then lifts.
- Wavy knife (crinkle cutter, sage-green polymer handle):
  - the blade plate is corrugated by A·sin(2π(x − xr)/λ), A = 0.036, λ = 0.28;
  - the cut surface n·(X − o) = A·sin(2π d·(X − o)/λ) is carried into rest space as a wavy line, with tight rounding (0.026);
  - the blade presses straight down (no slide) and its wedge follows the corrugation;
  - cutting both ways makes crinkle-cut cubes.
- Cutter: Star, Heart, Flower and Round tin-plate rings with rolled rims.
  - Click a flat piece to press the ring through. It splits the piece into inside and outside, the walls are wedged apart, and the shape pops up to lift out.
- Up to 14 pieces. A small toast explains misses ("Missed — draw the blade across the slice.").

Rendering (WebGPU / WGSL)
- Procedural photo-studio cyclorama with softboxes. Soft PCSS key shadows tinted by the jelly, plus contact AO from a top-down height map.
- Jelly: refraction of the scene by view-ray thickness (back-face depth pass), Beer–Lambert absorption, milky scattering in the pith, back-lit glow at thin edges, Fresnel studio reflections and GGX highlights.
- The zest, pith, segments and vesicles are shaded from rest-space coordinates, so fresh cut faces show the real inside.
- Tools are drawn behind the jelly surface, so buried steel is seen refracted:
  - brushed steel with a satin edge bevel and polished bolster;
  - walnut handle with rivets;
  - pebbled polymer handle;
  - tin-plate cutter rings.
- Post: exposure, Khronos PBR Neutral tone mapping, sRGB, dither.

UI (editorial "Material Studies / No. 010", English)
- Italic serif title "Citrus / Jelly." with the caption "Sunshine in segments. Soft enough to slice. Sweet enough to share."
- Status pill "WEBGPU · LIVE".
- Panel "The Specimen":
  - tool grid and cutter shapes;
  - variety swatches;
  - Firmness and Internal damping sliders;
  - Give it a nudge, Reset, Pause; ¼ speed and Show mesh.
- Readouts: tool hint, Mass (g), Volume (% of rest), Kinetic (µJ), Pieces.
- A collapsible "Inside the experiment" with notes on tetrahedra, cutting, the wavy knife, cookie cutters, the riding surface, and light through jelly.
- Fallback "This slice needs WebGPU." Stacked mobile layout with no horizontal scroll.
```

</details>
