# 百香果果冻 Passion Fruit Jelly

- **类型**：交互网页 / 软体果冻
- **技术栈**：WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `xpbd` `软体模拟` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2113069968266834400) · [提示词帖](https://x.com/vib3coded/status/2113070117189808506) · 2026-10-22（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。提示词要求沿用作者此前的 Melon / Avocado / Peach jelly 切片的引擎和版式，那些源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![百香果果冻 Passion Fruit Jelly](../assets/passion-fruit-jelly.jpg)

## 提示词（中文）

构建一个实时 WebGPU 软体 "jelly" 研究：半颗百香果。引擎和编辑式页面风格与我的 Melon / Avocado / Peach jelly 切片相同。

### 几何

几何来自 SDF。一个略微压扁的球，顶部切平。外面是一层薄的、起皱的紫色果皮，然后是一圈大约 0.15 R 厚的白色中果皮壁。里面是一个凹窝，盛着凹凸不平的半透明橙色果肉，液面略低于杯缘。

### 模拟

模拟在 CPU 上做 XPBD：共旋转形状匹配加上体积约束，网格是每个单元 5 个四面体的六面体晶格，60 Hz、10 个子步。四面体按区域分开——果皮杯结实、有皮革感；果肉非常软，体积约束是柔顺的。所以抓住果肉时，它会像黏糊一样缩颈、拉长，然后瘫软回去，而不是把整颗果实提起来。

### 渲染

渲染一张蒙皮到晶格上的 surface nets 网格：折射、Beer–Lambert 吸收、次表面散射、菲涅尔摄影棚反射、GGX、阴影贴图、接触 AO、PBR Neutral 色调映射。着色区域由静止空间的 SDF 决定：果皮上圆润的皱纹凹凸（掠射角和远处会淡掉），浅色的中果皮，衬在凹窝里的一层薄黄膜，果肉里柔软的 Voronoi 汁囊细胞。大约 100 颗深色、扁平的泪滴形种子，以及几个气泡，嵌在果肉里，跟着晃动一起动。

### 品种与控制

品种：Purple、Golden、Granadilla。控制：firmness、internal damping、nudge、reset、¼ speed、show mesh、pause。读数：质量、体积、动能。有一份 "Inside the experiment" 说明。界面为英文，适配手机。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a real-time WebGPU soft-body "jelly" study of a halved passion fruit, same engine and editorial page style as my Melon / Avocado / Peach jelly slices. Geometry from SDFs: a slightly squashed sphere cut flat at the top, a thin wrinkled purple skin, a ~0.15 R white pith wall, and a hollow filled with lumpy translucent orange pulp sitting a little below the rim. Sim: CPU XPBD co-rotational shape matching + volume constraints on a 5-tet hex lattice, 10 substeps at 60 Hz, with per-tet regions — a firm, leathery rind cup and a very soft pulp whose volume constraints are compliant, so grabbing the pulp makes it neck and stretch like goo and slump back instead of lifting the whole fruit. Render a surface-nets mesh skinned to the lattice: refraction, Beer–Lambert absorption, subsurface scattering, Fresnel studio reflections, GGX, shadow map, contact AO, PBR Neutral tone mapping. Shader regions from rest-space SDFs: rounded wrinkle bump on the skin (faded at grazing angles and distance), pale pith, a thin yellow membrane lining the hollow, soft Voronoi juice-sac cells in the pulp; ~100 dark flat teardrop seeds and a few bubbles embedded in the pulp so they ride the wobble. Varieties: Purple, Golden, Granadilla. Controls: firmness, internal damping, nudge, reset, ¼ speed, show mesh, pause; mass/volume/kinetic readouts; "Inside the experiment" notes. English UI, mobile-friendly.
```

</details>
