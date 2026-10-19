# 整颗橙子果冻 Whole Orange Jelly

- **类型**：交互网页 / 可切割软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 软体 · SDF 切割 · 体积渲染
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `切割` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110665495221268915) · [提示词帖](https://x.com/vib3coded/status/2110665641665454342) · 2026-10-15（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来测试 AI 模型的提示词（帖子展示的是 Claude Opus 5.5 的结果）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "Whole Orange Jelly"（整颗橙子果冻）——一个单文件自包含 HTML（内联 JS/CSS，无第三方库）：一颗由果冻做成的实时 WebGPU 软体完整橙子。用户可以抓住并拉伸它，还能用刀把它切成圆片、楔块和小块。每一块都是独立晃动的物体。

### 形状与碎块

- 橙子是一个有向距离场：一个略扁的椭球（沿 x 的极向半长 1.27，赤道半径 1.36）侧躺着，与地面接触处有一个柔和压平的"座面"。
- 每块碎块都是这个场被产生它的那些切割半空间 n·X ≤ c 裁切后的结果，新切边做倒圆（smooth max，k ≈ 0.085）。所有碎块共享橙子原始的静止坐标系，因此内部结构保持在它生长时的位置。
- 每块碎块：
  - 一层投影到场上的 surface-nets 渲染外皮（0.042 网格）；
  - 一个在碎块自身主轴坐标系中用于模拟的六面体晶格，边界节点吸附到表面；
  - 把渲染顶点用重心坐标嵌入晶格四面体中。
- 最多 30 块；拒绝过细的碎片。

### 解剖结构（全部在静止空间中，因此每一刀都会把它显示在真实位置）

- 外果皮（0.07 深），带油胞孔、斑驳的色调，一端是绿色果蒂，另一端是小小的脐。
- 白色内皮（pith，深至 0.19）。
- 围绕果蒂轴的 11 瓣果肉，瓣间是细细的乳白色隔膜（略带扰动、弯曲，并沿轴向游走），沿轴是一根白色果芯。
- 汁胞：每瓣内从果芯呈扇形散开的泪滴形小囊。
- 果芯附近 16 粒浅色柑橘籽，尖端朝内；果肉中有几个小气泡。
- 被切到的籽归属于包含其中心的那一侧，并被轻轻移到新切面正下方。

### 物理（XPBD）

- 每块碎块：六面体单元，做共旋转形状匹配，并对其五个四面体施加体积约束。
- 外果皮和白皮比果肉更硬。
- 边阻尼和形变阻尼；带库仑摩擦和一点滚动阻力的地面接触。
- 碎块之间的接触，在最佳拟合坐标系中对照彼此精确的静止形状判断。
- 静止的碎块进入休眠，被触碰时唤醒；固定 60 Hz 步长，小子步。

### 刀

- 一把菜切刀（nakiri）风格的刀：在橙子上画一道划痕。
- 这道划痕在其穿过物体的顶部读取，确定一个竖直刀刃平面，通过每个被穿过碎块的最佳拟合旋转带入其静止坐标系，并作为一个半空间加入。
- 在刀对准、压出凹槽、竖直切下的过程中，新碎块被增量构建。它们继承原来那块果冻的位置和速度，刀刃把切面楔开。

### 渲染（WebGPU / WGSL）

- 程序化摄影棚。柔和的 PCSS 主光阴影带果冻色调，另加由高度图得到的接触 AO。
- 背面厚度；折射场景，每次采样按自身路径长度变暗。
- 在静止空间中对果冻做体积步进（volumetric march），使用逐顶点的逆形变梯度：
  - 外果皮、白皮、隔膜/果芯和果肉各以自己的颜色吸收（Beer–Lambert）；
  - 散射是灰色的（只有吸收带颜色），所以从橙色果肉中散射出来的光仍然是橙色。
- 白皮、星形隔膜和果芯在切面上清晰可辨。
- 薄边缘的背光辉光、菲涅尔摄影棚反射、GGX 高光、糖晶闪光。
- 后处理：Khronos PBR Neutral 色调映射、sRGB、抖动。

### UI（编辑风格 "Material Studies / No. 032"，英文）

- 斜体衬线标题 "Whole / Orange."，说明文字 "Eleven segments, set in jelly. Zest, pith and juice. Cut it as small as you like."
- 状态胶囊 "WEBGPU · LIVE"。
- 工具：Hand / Knife。品种：Navel（脐橙）、Blood（血橙）、Cara Cara（红肉脐橙）。
- Firmness 和 Internal damping 滑块；Give it a nudge、Reset、Pause；¼ speed 和 Show mesh。
- 读数：Mass（g，1 单位 ≈ 3 cm，密度 1.3 g/cm³）、Volume（静止体积的百分比）、Kinetic（mJ）、Pieces。
- 可折叠的 "Inside the experiment"，说明所用方法。
- 没有 WebGPU 时降级。移动端为堆叠布局，无横向滚动。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Whole Orange Jelly" — a single self-contained HTML file (inline JS/CSS, no libraries): a real-time WebGPU soft-body whole orange made of jelly. The user can grab and stretch it, and cut it with a knife into wheels, wedges and small pieces. Every piece is its own wobbling body.

Shape and pieces
- The orange is a signed distance field: a gently oblate ellipsoid (polar half-length 1.27 along x, equatorial radius 1.36) lying on its side, with a softly flattened seat on the floor.
- Every piece is that field clipped by the half-spaces n·X ≤ c of the cuts that made it, with the fresh edges rounded (smooth max, k ≈ 0.085). All pieces share the orange's original rest frame, so the anatomy stays where it grew.
- Per piece:
  - a surface-nets render skin (0.042 grid) projected onto the field;
  - a hex lattice for the simulation in the piece's own principal frame, with boundary nodes snapped to the surface;
  - barycentric embedding of render vertices into the lattice tets.
- Up to 30 pieces; slivers are rejected.

Anatomy (all in rest space, so every cut shows it where it really is)
- Zest (0.07 deep) with oil-gland pores, a mottled tone, a green stem button at one end and a small navel at the other.
- White pith (to 0.19 deep).
- 11 segments around the stem axis, with thin milky membrane walls (slightly jittered, bowed and wandering along the axis) and a pithy core along the axis.
- Juice vesicles: teardrop sacs fanning out from the core within each segment.
- 16 pale citrus pips near the core, pointed end inward; a few small bubbles in the flesh.
- A pip that a cut goes through is kept by the side holding its centre and eased just under the new face.

Physics (XPBD)
- Per piece: hex cells with co-rotational shape matching plus volume constraints on their five tets.
- Zest and pith firmer than the flesh.
- Edge and deformation damping; floor contact with Coulomb friction and a little rolling resistance.
- Piece–piece contact against each other's exact rest shape in a best-fit frame.
- Sleeping pieces that wake on touch; fixed 60 Hz step with small substeps.

Knife
- A nakiri-style knife: draw a stroke across the orange.
- The stroke, read on the top of what it crosses, fixes a vertical blade plane, carried into each crossed piece's rest frame by its best-fit rotation and added as a half-space.
- The new pieces are built incrementally while the knife lines up, presses a groove and cuts straight down. They take over the position and speed of the jelly they came from, and the blade wedges the faces apart.

Rendering (WebGPU / WGSL)
- Procedural photo studio. Soft PCSS key shadow tinted by the jelly, plus contact AO from a height map.
- Back-face thickness; refraction of the scene, with each tap dimmed by its own path length.
- A volumetric march through the jelly in rest space, using a per-vertex inverse deformation gradient:
  - zest, pith, membranes/core and flesh each absorb with their own colour (Beer–Lambert);
  - scattering is grey (only absorption is coloured), so light scattered out of orange flesh stays orange.
- The white pith, the membrane star and the core read crisply on cut faces.
- Back-lit glow at thin edges, Fresnel studio reflections, GGX highlights, sugar-crystal glints.
- Post: Khronos PBR Neutral tone mapping, sRGB, dither.

UI (editorial "Material Studies / No. 032", English)
- Italic serif title "Whole / Orange." with the caption "Eleven segments, set in jelly. Zest, pith and juice. Cut it as small as you like."
- Status pill "WEBGPU · LIVE".
- Tools: Hand / Knife. Varieties: Navel, Blood, Cara Cara.
- Firmness and Internal damping sliders; Give it a nudge, Reset, Pause; ¼ speed and Show mesh.
- Readouts: Mass (g, 1 unit ≈ 3 cm at 1.3 g/cm³), Volume (% of rest), Kinetic (mJ), Pieces.
- A collapsible "Inside the experiment" with notes on the method.
- Fallback without WebGPU. Stacked mobile layout with no horizontal scroll.
```

</details>
