# 南瓜果冻 Pumpkin Jelly

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `万圣节` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110438822085312714) · [提示词帖](https://x.com/vib3coded/status/2110438942466302433) · 2026-10-15（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![南瓜果冻 Pumpkin Jelly](../assets/pumpkin-jelly.jpg)

## 提示词（英文原文）

```text
Build "Pumpkin Jelly" — a single self-contained HTML file (inline JS/CSS, no libraries): a Halloween real-time WebGPU soft-body gummy pumpkin wedge lit by a flickering candle, which you can grab, stretch, lift and twist.
Object
A rounded pie-shaped wedge: 32° half-angle, radius ≈ 1.8, thickness 0.58, rounded corners (exact pie SDF minus a rounding radius) and bevelled top/bottom edges.
Ribbed rind on the outer arc:broad lobes with darker grooves running pole to pole, fine speckle and a waxy finish;
the normal is tilted across the ribs so they read as real bumps.

A lighter inner-rind band, then dense orange flesh with grain.
At the tip, the seed pulp:glassy yellow-orange pulp with clumped fibrous strings (domain-warped noise strands);
about 24 flat creamy pumpkin seeds (oval with one pointed end, raised rim, thin middle) hanging at random angles and depths. Some lie flat just under the cut faces.

A few small air bubbles in the flesh.
Varieties: Jack (orange), Cinderella (red-orange), Ghost (white).
Physics (XPBD tetrahedral soft body)
Mesh: 2D Delaunay of the rounded outline plus a hex lattice, extruded into prisms → tets.
Co-rotational per-tet shape matching (warm-started quaternion) plus volume constraints.
Stiffer rind; edge-velocity damping; floor contact with Coulomb friction.
Soft patch grab with bounded reach; scroll or a second finger twists the held patch.
Fixed 60 Hz step with 10 substeps.
Seeds and bubbles are embedded in the tets by barycentric weights, so they ride with the flesh.
Rendering (WebGPU / WGSL)
Dusk-violet studio cyclorama with softboxes. Soft PCSS key shadow tinted by the jelly, plus contact AO from a top-down height map.
A candle just out of frame (front-left, low) with a multi-sine flicker:wraps warm light into the jelly;
glows through thin parts;
adds its own GGX glint;
pools orange light on the table.

Jelly:refraction of the scene by view-ray thickness (back-face pass);
per-tap Beer–Lambert absorption by material (flesh, glassy pulp with strings, milky inner rind, opaque rind) with matching scattering;
back-lit glow at thin edges, Fresnel studio reflections and GGX highlights.

Seeds are shaded creamy and matte with a darker rim and a wet sheen, also lit by the candle.
Post: exposure, Khronos PBR Neutral tone mapping, sRGB, dither.
UI (dark editorial theme, English)
"Material Studies / No. 031", italic serif title "Pumpkin / Jelly." with the caption "Cut by candlelight. Seeds in the strings. A spooky little wobble."
Status pill "WEBGPU · LIVE".
Panel "The Specimen": variety chips (rind / inner band / flesh); Firmness and Internal damping sliders; Give it a nudge, Reset, Pause; ¼ speed and Show mesh.
Readouts: Mass (g, 1 unit ≈ 4 cm at 1.3 g/cm³), Volume (% of rest), Kinetic (µJ).
A collapsible "Inside the experiment" with notes on the method.
Fallback "This pumpkin needs WebGPU." Stacked mobile layout with no horizontal scroll.
```

---

## 提示词（中文）

构建 "Pumpkin Jelly"（南瓜果冻）——一个单文件自包含 HTML（内联 JS/CSS，无第三方库）：一块万圣节主题的实时 WebGPU 软体软糖南瓜楔块，由一支摇曳的蜡烛照亮，你可以抓住、拉伸、抬起和扭转它。

### 物体

一块圆润的扇形楔块：半角 32°，半径 ≈ 1.8，厚度 0.58，圆角（精确扇形 SDF 减去倒圆半径），上下边缘倒角。

外弧上带棱的南瓜皮：
- 宽阔的瓣，瓣间是从一极延伸到另一极的深色沟槽，细小斑点和蜡质光泽；
- 法线沿棱横向倾斜，让它们看起来是真实的凸起。

一条颜色更浅的内皮带，然后是带纹理的致密橙色果肉。

尖端处是籽瓤：
- 玻璃质感的黄橙色瓤，夹着成团的纤维丝（用域扭曲噪声生成的丝缕）；
- 约 24 粒扁平的奶油色南瓜子（一端尖的椭圆形、凸起的边缘、薄薄的中部），以随机角度和深度悬挂其中。有些平躺在切面正下方。

果肉中有几个小气泡。

品种：Jack（橙色）、Cinderella（红橙色）、Ghost（白色）。

### 物理（XPBD 四面体软体）

- 网格：对圆角轮廓做二维 Delaunay 剖分，加上六边形晶格，挤出成棱柱 → 四面体。
- 每个四面体的共旋转形状匹配（热启动四元数）加体积约束。
- 瓜皮更硬；边速度阻尼；带库仑摩擦的地面接触。
- 柔性区域抓取，拉伸距离有上限；滚轮或第二根手指扭转被抓住的区域。
- 固定 60 Hz 步长，10 个子步。
- 籽和气泡通过重心权重嵌入四面体，因此随果肉一起移动。

### 渲染（WebGPU / WGSL）

- 带柔光箱的黄昏紫色摄影棚无缝背景。柔和的 PCSS 主光阴影带果冻色调，另加由俯视高度图得到的接触 AO。
- 画面外（左前方、低位）一支蜡烛，用多正弦叠加做闪烁：
  - 把暖光包裹进果冻；
  - 透过薄的部分发光；
  - 加上它自己的 GGX 闪光；
  - 在桌面上投下一汪橙色的光。
- 果冻：
  - 按视线方向厚度（背面通道）折射场景；
  - 每次采样按材质（果肉、带丝的玻璃质瓤、乳白内皮、不透明瓜皮）做 Beer–Lambert 吸收，并配相应的散射；
  - 薄边缘的背光辉光、菲涅尔摄影棚反射和 GGX 高光。
- 南瓜子着色为奶油色哑光，边缘更深，带湿润光泽，同样被烛光照亮。
- 后处理：曝光、Khronos PBR Neutral 色调映射、sRGB、抖动。

### UI（深色编辑风格主题，英文）

- "Material Studies / No. 031"，斜体衬线标题 "Pumpkin / Jelly."，说明文字 "Cut by candlelight. Seeds in the strings. A spooky little wobble."
- 状态胶囊 "WEBGPU · LIVE"。
- 面板 "The Specimen"：品种选择块（瓜皮 / 内皮带 / 果肉）；Firmness 和 Internal damping 滑块；Give it a nudge、Reset、Pause；¼ speed 和 Show mesh。
- 读数：Mass（g，1 单位 ≈ 4 cm，密度 1.3 g/cm³）、Volume（静止体积的百分比）、Kinetic（µJ）。
- 可折叠的 "Inside the experiment"，说明所用方法。
- 降级页面 "This pumpkin needs WebGPU."。移动端为堆叠布局，无横向滚动。
