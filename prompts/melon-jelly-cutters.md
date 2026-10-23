# 西瓜果冻切割 Melon Jelly Cutters

- **类型**：交互网页 / 可切割软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 刀具切割
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `切割` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2112638127483343162) · [提示词帖](https://x.com/vib3coded/status/2112638899965001772) · 2026-10-20（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![西瓜果冻切割 Melon Jelly Cutters](../assets/melon-jelly-cutters.jpg)

## 提示词（中文）

构建一个实时 WebGPU 软体 "jelly" 研究：一块可以用钢刀切开的西瓜楔。页面是编辑式的 "Material Studies" 风格（衬线标题 "Melon Jelly."，低饱和的纸质背景，侧栏，英文界面，适配手机）。

### 几何与模拟

几何：一块厚的三角形西瓜楔。圆润的绿色果皮，一层浅白，半透明的红色果肉，里面有深色的籽和几个气泡。

模拟：四面体网格上的 CPU XPBD，步长固定 60 Hz，10 个子步。每个四面体用一条有限柔度的共旋转形状匹配约束，这条约束也会把已经翻转的单元翻回来；再加上一条近乎不可压缩的体积约束，所以被拉长的切片会向中间缩颈。果皮大约比果肉硬 3 倍。阻尼只作用在沿边的相对速度上。地面接触用库仑摩擦。抓取是对一小片粒子的柔性附着，距离有上限；滚轮或第二根手指可以扭转。

### 两种工具：Hand 和 Knife

- Knife：用户在切片上画一笔。在表面上读到这一笔之后，它定义一个竖直的刀平面。每一块都存成切片静止平面里的一条圆角凸轮廓。对刀平面切过的每一块，用一个最佳旋转去拟合这块现在的姿态，把平面带回静止空间，变成一条直线，再沿着这条线把轮廓切开。
- 这一刀：松开的时候，把两半预先做成全新的四面体网格。一把会动的钢刀对准这一笔落下来，先在果冻上压出一道沟。切穿的那一刻，换成新的两块。它们继承自己切出来的那块果肉的位置和速度。刀刃在落到案板的路上，把两个切面楔开。刀刃要画在果冻表面的后面，这样埋进去的那一段看起来是被折射过的。
- 碎块：每一块都是自己的软体，可以再被抓住、拉长、切开。块和块之间会撞上，而不是穿过去。

### 渲染

一张平滑的表面网格，加上籽和气泡。每个顶点用重心权重嵌进一个四面体，所以会跟着晃。WGSL 通道：

- 先画地面、籽和气泡；
- 再画背面，得到每一条视线穿过的厚度；
- 正面按这个厚度折射，Beer–Lambert 吸收，浅色层里的乳白散射，薄边缘上被从后面照亮的辉光，程序化摄影棚的菲涅尔反射，以及 GGX 高光；
- 地面上有一块被果冻染色的柔和主光阴影，再加上来自俯视高度图的接触 AO。

### 品种与控制

品种：Crimson、Golden、Rosé。控制：Hand / Knife 工具切换，firmness 和 internal damping 滑块，"Give it a nudge"、Reset、Pause、¼ speed、Show mesh，以及质量、体积、动能读数。一个 "Inside the experiment" 说明抽屉，解释物理、切割和渲染。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a real-time WebGPU soft-body "jelly" study of a watermelon wedge that you can cut with a steel knife, in an editorial "Material Studies" page style (serif title "Melon Jelly.", muted paper backdrop, side panel, English UI, mobile-friendly). Geometry: a thick triangular watermelon wedge with a rounded green rind, a pale white layer, and translucent red flesh with dark seeds and a few air bubbles. Sim: CPU XPBD on a tetrahedral mesh, fixed 60 Hz step with 10 substeps. Each tet uses a co-rotational shape-matching constraint with finite compliance, which also flips inverted elements back out, plus a near-incompressible volume constraint so a stretched slice necks in. The rind is about 3× stiffer than the flesh. Damping acts only on relative velocity along edges. Floor contact uses Coulomb friction. Grabbing is a soft, reach-limited attachment to a patch of particles, and scroll or a second finger twists it.

Two tools, Hand and Knife:
- Knife: the user draws a stroke across the slice. Read on the surface, that stroke defines a vertical blade plane. Every piece is stored as a rounded convex outline in the slice's rest plane. For each piece the plane crosses, fit the piece's current pose with a best rotation, carry the plane back to rest space as a straight line, and split the outline along it.
- The cut: prebuild both halves as fresh tet meshes on release. An animated steel knife lines up over the stroke, comes down, and first presses a groove into the jelly. When it breaks through, swap in the new pieces, which inherit the position and velocity of the flesh they came from, and the blade wedges the faces apart on its way to the board. Draw the blade behind the jelly surface so the buried part is seen refracted.
- Pieces: every piece is its own soft body that can be grabbed, stretched and cut again, and pieces collide with each other instead of passing through.

Render: a smooth surface mesh plus the seeds and bubbles, each vertex embedded in a tet by barycentric weights so they ride the wobble. WGSL passes:
- floor, seeds and bubbles first;
- back faces, to get the thickness each view ray crosses;
- front faces with refraction by that thickness, Beer–Lambert absorption, milky scattering in the pale layer, a back-lit glow at thin edges, Fresnel reflections of a procedural studio, and GGX highlights;
- a soft key shadow on the floor tinted by the jelly, plus contact AO from a top-down height map.

Varieties: Crimson, Golden, Rosé. Controls: Hand/Knife tool toggle, firmness and internal damping sliders, "Give it a nudge", Reset, Pause, ¼ speed, Show mesh, plus mass/volume/kinetic readouts and an "Inside the experiment" notes drawer explaining the physics, cutting and rendering.
```

</details>
