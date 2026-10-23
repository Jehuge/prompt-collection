# 桃子果冻 Peach Jelly

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 刚体果核 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `刚体` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2112240323560645092) · [提示词帖](https://x.com/vib3coded/status/2112240438635868328) · 2026-10-19（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![桃子果冻 Peach Jelly](../assets/peach-jelly.jpg)

## 提示词（中文）

构建一个单文件 WebGPU 页面 "Peach Jelly"（桃子果冻），采用 "Material Studies" 标本页的风格（浅色摄影棚背景 #E2DFDA，斜体衬线标题，右侧标本控制面板，左下实时读数，可折叠的 "Inside the experiment" 说明；响应式，手机上为堆叠布局，没有 WebGPU 时显示降级卡片）。

### 主体

半个桃子，由半透明果冻做成，沿缝合线切开。果皮朝下躺着，切面朝上，果核坐在凹窝里。

### 几何

果实是一个有向距离场：一个球体，从果柄到花端略微拉长，果柄处有一个凹窝，花端有一个淡淡的尖，一侧边缘有缝合线的折痕，腹部在地面上轻轻压平。在赤道处切开，再减去一个给果核留的杏仁形凹窝（压扁的，两个宽面与切面平行，朝果柄那一端比较钝）。

模拟网格是吸附对齐过的六面体晶格，每个单元 5 个四面体（大约 700 个粒子 / 大约 2500 个四面体）。节点层正好落在地面和切面上。节点被强制推到果核外面。渲染表面用 surface nets，用重心权重嵌进四面体里。每一帧做一次法线平滑，这样反射不会把四面体的折痕勾出来。

果核有自己的高分辨率网格：深深的、像虫子爬过的沟，大多沿纵向，还有用位移刻出来的小坑；边缘一圈低矮的棱；花端一个小尖。沟有多深，写在顶点的材质 id 里，给着色用。

### 物理（CPU，XPBD，60 Hz，10 个子步）

每个四面体做共旋转形状匹配，加上体积约束。果皮更硬。阻尼是沿边的相对速度。地面有摩擦。指针可以抓住，也可以扭转。

果核是刚体（位置、四元数、椭球惯量）。它和每一个粒子都有带摩擦的接触，和地面之间是采样出来的接触点。凹窝里贴着的那些节点用柔性黏附键拉住果核。只有持续的净拉力才会把它们剥开，这个拉力在这半个桃子的最佳拟合刚体坐标系里量（凹窝底部先剥，唇缘最后）。短暂的磕碰不行。一颗已经松开、但还停在凹窝里的果核，会被吸回原来的位置，经过一段柔和的宽限期后再重新粘上。抓住果核是把它整个移动，也可以把它扔出去。

按钮：nudge、reset、"Pop the stone" / "Put the stone back"、pause、¼ speed、show mesh。滑块是硬度和阻尼。读数：mass、volume %、grip %。

### 渲染（WGSL）

阴影贴图，加上一张俯视的接触 AO 图。场景通道画地面、果核和气泡，alpha 里放线性深度。再一个背面通道算厚度。果冻按这个厚度折射，带 Beer–Lambert 吸收和散射。

区域由静止空间的 SDF 决定：金色的果肉；紧贴果核的一圈红宝石色，不规则地断开，细的红纤维向外延伸；果皮的红晕向果肉渗进一点点。果皮是黄的，带着一块一块的红晕和浅色斑点，掠射角有丝绒一样的光泽（Nectarine 这个品种是光滑、有光泽的）。果核是木质的红棕色，深色沟里挂着红色纤维的碎屑，主光的阴影很柔，光泽很低。

品种：Yellow、White、Nectarine。界面文字为英文。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file WebGPU page "Peach Jelly" in the style of a "Material Studies" specimen sheet (light studio backdrop #E2DFDA, italic serif title, a specimen control panel on the right, live readouts bottom-left, collapsible "Inside the experiment" notes; responsive with a stacked phone layout and a no-WebGPU fallback card).

Subject: half a peach made of translucent jelly, cut along its suture, lying skin-down with the cut face up and its stone seated in the hollow.

Geometry: a signed distance field for the fruit — a sphere slightly longer from stem to blossom end, with a stem dimple, a faint point at the blossom tip and the suture crease along one side of the rim, belly gently flattened on the floor — cut at the equator, minus an almond-shaped hollow for the stone (flattened, broad faces parallel to the cut, blunt toward the stem). Simulation mesh: a snapped hex lattice, 5 tets per cell (~700 particles / ~2500 tets), node layers exactly on the floor and the cut face, nodes forced out of the stone. Render surface by surface nets, embedded in the tets by barycentric weights, with one normal-smoothing pass per frame so reflections don't pick out tet kinks. The stone gets its own high-resolution mesh: deep wormy furrows (mostly lengthwise) and little pits carved by displacement, a low keel round its edge, a small point at the blossom end; groove depth rides in the vertex material id for shading.

Physics (CPU, XPBD, 60 Hz, 10 substeps): per-tet co-rotational shape matching + volume constraints, stiffer skin, edge-relative damping, floor friction, pointer grab with twist. The stone is a rigid body (position, quaternion, ellipsoid inertia) with frictional contact against every particle and sampled floor contacts. Nodes lining the hollow are held by soft adhesion bonds that peel (floor of the hollow first, lip last) under a sustained net pull measured in the half's best-fit rigid frame — never from brief knocks; a loose stone resting in the hollow is drawn home and re-bonded with a soft grace period. Grabbing the stone moves it as a whole and it can be thrown. Buttons: nudge, reset, "Pop the stone" / "Put the stone back", pause, ¼ speed, show mesh; sliders for firmness and damping; readouts mass, volume %, grip %.

Rendering (WGSL): shadow map + top-down contact-AO map, scene pass (floor, stone, bubbles) with linear depth in alpha, back-face thickness pass, refracting jelly with Beer–Lambert absorption and scattering. Regions from rest-space SDFs: golden flesh; a ruby ring hugging the stone, broken up irregularly, with fine red fibres streaking out; the skin's blush bleeding a little way into the flesh. Skin: yellow with patchy red blush and pale flecks, a velvet sheen at grazing angles (nectarine: smooth and glossy). Stone: woody reddish-brown, dark furrows with shreds of red fibre, soft key shadows, low sheen. Varieties: Yellow, White, Nectarine. UI text in English.
```

</details>
