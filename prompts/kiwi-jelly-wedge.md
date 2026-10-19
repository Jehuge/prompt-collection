# 猕猴桃果冻楔块 Kiwi Jelly Wedge

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs Claude Fable 5.1
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109932661204517203) · [提示词帖](https://x.com/vib3coded/status/2109932845774897347) · 2026-10-13（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs Claude Fable 5.1）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "Kiwi Jelly Wedge"（猕猴桃果冻楔块）——一个单文件自包含 HTML（内联 JS/CSS，无第三方库）：一块实时 WebGPU 软体软糖猕猴桃楔块，你可以抓住、拉伸、抬起和扭转它。

### 物体

厚猕猴桃切片的六分之一：一块扇形楔块，半角 30°，半径 ≈ 1.8，厚度 0.56。圆角（iq 的精确扇形 SDF 减去倒圆半径），上下边缘倒角。

各区域，在静止空间中从尖端起算：
- 尖端处奶油色的果芯，边缘略呈分瓣状；
- 每隔 2π/56 从果芯放射出的细细浅色射线，每条亮度和长度各自随机；
- 围绕籽的一圈颜色更深、更像玻璃的环（在 Ruby 品种中泛红）；
- 明亮多汁的外层果肉，带放射状细胞纹理，紧贴果皮下方有一条更浅的带；
- 圆弧外壁上一层薄薄的棕色绒毛果皮。

籽：
- 小而扁的黑色泪滴，尖端朝向果芯，在射线之间成放射状排列，分布在四个深度；
- 表面那层会像真籽一样破开切面；其余的漂浮在内部，透过果冻可见；
- 湿润有光泽的着色。

外层果肉中有几个小气泡。

品种：Green（绿心）、Gold（黄心）、Ruby（红心）。

### 物理（XPBD 四面体软体）

- 网格：对圆角轮廓做二维 Delaunay 剖分，加上六边形晶格，挤出成棱柱 → 四面体。
- 每个四面体的共旋转形状匹配（热启动四元数）加体积约束。
- 果皮和果芯的四面体更硬；边速度阻尼；带库仑摩擦的地面接触。
- 柔性区域抓取，拉伸距离有上限；滚轮或第二根手指扭转被抓住的区域。
- 固定 60 Hz 步长，10 个子步；温和的稳定处理。
- 籽和气泡是独立的网格，用重心权重嵌入四面体，因此随果肉一起移动。

### 渲染（WebGPU / WGSL）

- 带柔光箱的程序化摄影棚无缝背景。柔和的 PCSS 主光阴影带绿色调，另加由俯视高度图得到的接触 AO。
- 籽和气泡在场景通道中绘制。背面通道给出视线方向厚度。
- 果冻：
  - 场景折射，每次采样按材质（果肉、玻璃质籽环、乳白果芯和射线、不透明果皮）做 Beer–Lambert 吸收；
  - 散射、薄边缘的背光辉光、菲涅尔摄影棚反射和 GGX 高光；
  - 绒毛果皮上的天鹅绒光泽；
  - 果肉中稀疏的糖晶闪光。
- 后处理：曝光、Khronos PBR Neutral 色调映射、sRGB、抖动。

### UI（编辑风格 "Material Studies / No. 028"，英文）

- 斜体衬线标题 "Kiwi / Jelly."，说明文字 "An emerald wedge. A halo of seeds. A gentle wobble."
- 状态胶囊 "WEBGPU · LIVE"。
- 面板 "The Specimen"：品种选择块（果皮 / 果芯 / 果肉色带）；Firmness（"trembling → set"）和 Internal damping（"lively → syrupy"）滑块；Give it a nudge、Reset、Pause；¼ speed 和 Show mesh。
- 读数：Mass（g，1 单位 ≈ 1.6 cm，密度 1.3 g/cm³）、Volume（静止体积的百分比）、Kinetic（µJ）。
- 可折叠的 "Inside the experiment"，说明所用方法。
- 降级页面 "This kiwi needs WebGPU."。移动端为堆叠布局，无横向滚动。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Kiwi Jelly Wedge" — a single self-contained HTML file (inline JS/CSS, no libraries): a real-time WebGPU soft-body gummy kiwi wedge you can grab, stretch, lift and twist.
Object
One sixth of a thick kiwi slice: a pie-shaped wedge with 30° half-angle, radius ≈ 1.8 and thickness 0.56. Rounded corners (iq's exact pie SDF minus a rounding radius) and bevelled top/bottom edges.
Regions, measured from the tip in rest space:a cream core at the tip with a slightly lobed edge;
thin pale rays fanning out of the core every 2π/56, each with its own random brightness and length;
a darker, glassier ring around the seeds (blushes red in the Ruby variety);
bright juicy outer flesh with radial cell grain and a lighter band just under the skin;
a thin brown fuzzy skin on the arc wall.

Seeds:small flattened black teardrops, pointed end toward the core, in radial rows between the rays, at four depths;
the face layers break the cut surfaces like real seeds; the others float inside and show through the jelly;
wet glossy shading.

A few small air bubbles in the outer flesh.
Varieties: Green, Gold, Ruby.
Physics (XPBD tetrahedral soft body)
Mesh: 2D Delaunay of the rounded outline plus a hex lattice, extruded into prisms → tets.
Co-rotational per-tet shape matching (warm-started quaternion) plus volume constraints.
Stiffer skin and core tets; edge-velocity damping; floor contact with Coulomb friction.
Soft patch grab with bounded reach; scroll or a second finger twists the held patch.
Fixed 60 Hz step with 10 substeps; gentle settling.
Seeds and bubbles are separate meshes embedded in the tets by barycentric weights, so they ride with the flesh.
Rendering (WebGPU / WGSL)
Procedural photo-studio cyclorama with softboxes. Soft PCSS key shadow tinted green, plus contact AO from a top-down height map.
Seeds and bubbles are drawn in the scene pass. A back-face pass gives the view-ray thickness.
Jelly:refraction of the scene, with per-tap Beer–Lambert absorption by material (flesh, glassy seed ring, milky core and rays, opaque skin);
scattering, back-lit glow at thin edges, Fresnel studio reflections and GGX highlights;
a velvet sheen on the fuzzy skin;
sparse sugar glints in the flesh.

Post: exposure, Khronos PBR Neutral tone mapping, sRGB, dither.
UI (editorial "Material Studies / No. 028", English)
Italic serif title "Kiwi / Jelly." with the caption "An emerald wedge. A halo of seeds. A gentle wobble."
Status pill "WEBGPU · LIVE".
Panel "The Specimen": variety chips (skin / core / flesh bands); Firmness ("trembling → set") and Internal damping ("lively → syrupy") sliders; Give it a nudge, Reset, Pause; ¼ speed and Show mesh.
Readouts: Mass (g, 1 unit ≈ 1.6 cm at 1.3 g/cm³), Volume (% of rest), Kinetic (µJ).
A collapsible "Inside the experiment" with notes on the method.
Fallback "This kiwi needs WebGPU." Stacked mobile layout with no horizontal scroll.
```

</details>
