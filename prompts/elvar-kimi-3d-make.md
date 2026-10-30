# Elvar 一句话出 3D 模型（Kimi 3D Make）

- **类型**：3D 模型生成 / 可旋转查看 · 爆炸图 · 局部修改
- **技术栈**：Kimi K3.1 Pro · 3D Make（kimi.ai 左侧入口，输入框 `Bring your idea to 3D...`）
- **原作者**：[@elvar_official](https://x.com/elvar_official)（Elvar）
- **出处**：长文 [How to Turn an Idea Into a 3D Model You Can Explore](https://x.com/elvar_official/article/2113949756376388093)；相关帖：[可拆解无人机](https://x.com/elvar_official/status/2113990648646750546)、[Kimi vs GPT-6 Astra 沙虫](https://x.com/elvar_official/status/2114325660248281265)
- **标签**：`kimi` `3d-make` `文生3D` `爆炸图` `建筑内景` `局部修改` `提示词模板`

> 说明：本页内容来自 Elvar 的公开长文与帖子，这里只做收集与中文翻译，版权归原作者。和 [Anatomy 可拆解机器](elvar-anatomy.md) 那套不同：这里是**真正生成 3D 模型**，不是写代码搭交互页面。

---

## 好提示词的四要素

**物体 + 关键零件 + 外观（材质/配色） + 视角/背景**。先要一个清晰的简化版，主零件容易认，再一次只改一处。

## 工作流程

1. 打开 kimi.ai → 左侧 **3D Make** → 在 `Bring your idea to 3D...` 输入一句话描述。
2. 生成后**多角度转一圈检查**：零件是否齐、比例是否对、有没有穿插。
3. 需要看内部 → 发「爆炸图」跟进提示。
4. 哪里不对 → 用「局部修改模板」**一次只改一个零件**，其余保持不变。
5. 满意后导出 / 截图 / 录转盘视频。

---

## 模板 1：涡扇发动机（中文）

为一个可视化讲解创建一台涡扇喷气发动机的 3D 模型。展示大尺寸前风扇、压气机各级、燃烧段、涡轮各级，以及一侧打开的机匣，让内部可见。

金属用银色，每个主要部分用不同的强调色。放在白色背景上，四分之三视角。先做一个清晰的简化模型，让主要零件容易辨认。

<details>
<summary>英文原文（English original）</summary>

```text
Create a 3D model of a turbofan jet engine for a visual explanation.
Show a large front fan, compressor stages, a combustion section,
turbine stages and a casing with one side open so the inside is visible.

Use silver metal with a different accent color for each main stage.
Place it on a white background in a three-quarter view.
Start with a clear simplified model where the main parts are easy to recognize.
```

</details>

---

## 模板 2：爆炸图跟进（中文）

保持这台发动机的设计。做一个爆炸版本：各主要部分沿发动机长度方向分开，按正确的装配顺序排列。留出足够空间看清每一部分。所有零件保持在同一根轴线上对齐。使用相同的配色和背景。

<details>
<summary>英文原文（English original）</summary>

```text
Keep this engine design. Make an exploded version with the main stages
separated along the engine's length, in the correct assembly order.
Leave enough space to see each stage. Keep every part aligned on the same axis.
Use the same colors and background.
```

</details>

---

## 模板 3：雨林中庭 · 初版（中文）

创建一个带圆形玻璃屋顶的室内雨林中庭 3D 模型。
一道瀑布从中央开口落下，流入圆形水池。
两层弯曲步道与种植露台环绕水面。

使用日光、浅色石材和绿色植物。
用一个宽视角同时看到屋顶开口、瀑布和水池。
第一版保持简单，步道清晰、建筑结构可读。

<details>
<summary>英文原文（English original）</summary>

```text
Create a 3D indoor rainforest atrium with a circular glass roof.
A waterfall descends through an opening in the center into a round basin.
Curved walkways and planted terraces surround the water on two levels.

Use daylight, pale stone and green plants.
Show a wide view that includes the roof opening, waterfall and basin together.
Keep the first version simple, with clear walkways and readable architecture.
```

</details>

---

## 模板 3b：雨林中庭 · 跟进加植被（中文）

保持屋顶、水池和步道布局。
给种植增加层次：几棵高棕榈、更小的树、露台上的蕨类和低矮植物。步道保持畅通。
让瀑布成为视觉中心，透过绿植仍然可见。

<details>
<summary>英文原文（English original）</summary>

```text
Keep the roof, basin and walkway layout.
Add more variety to the planting: a few tall palms, smaller trees,
ferns and low plants on the terraces. Keep the paths clear.
Make the waterfall the center of attention and keep it visible through the greenery.
```

</details>

布局稳定后可改氛围，例如：`Show this at dusk with warm lights along the paths.`

---

## 模板 4：哥特教堂内景 · 初版（中文）

创建一座受科隆大教堂启发的哥特教堂内部 3D 场景。
包含长中殿、重复石柱、尖拱、肋拱穹顶和通高彩色玻璃窗。

视角放在人眼高度，沿中殿向前看。
石材用浅色，日光穿过彩色玻璃。
先搭主要建筑形体，并保持中殿通道通畅。

<details>
<summary>英文原文（English original）</summary>

```text
Create a 3D Gothic cathedral interior inspired by Cologne Cathedral.
Include a long central aisle, repeated stone columns, pointed arches,
a ribbed vaulted ceiling and tall stained-glass windows.

Place the view at human eye level looking down the aisle.
Use pale stone and daylight passing through the colored windows.
Start with the main architectural forms and keep the central aisle clear.
```

</details>

---

## 模板 4b：哥特教堂 · 跟进加细节与彩光（中文）

保持教堂布局与比例。
给柱子和拱肋加细节。让彩色玻璃的颜色落到地面上，同时保留建筑形体。
保持沿中殿向前的视角，并让远端可读。

<details>
<summary>英文原文（English original）</summary>

```text
Keep the cathedral layout and proportions.
Add detail to the columns and vault ribs. Make the stained-glass colors
visible on the floor while preserving the shape of the architecture.
Keep the view down the central aisle and make the far end readable.
```

</details>

同一套写法也可用于图书馆、车站大厅或展览空间：先描述房间，点出关键特征，再定视角。

---

## 模板 5：局部修改（中文）

保持这个模型的其余部分不变。
修改这个部分：[零件名称，或附上标注过的截图]。
它现在是这样的：[看得见的问题]。
改成这样：[期望的样子]。

<details>
<summary>英文原文（English original）</summary>

```text
Keep the rest of this model unchanged.
Change this part: [name the part or attach a marked screenshot].
It currently looks like this: [describe the visible problem].
Make it look like this instead: [describe the change].
```

</details>

示例：`The walkway ends in mid-air. Connect it to the upper terrace.` 一次只改一处，改完再转一圈检查。

---

## 致谢

- 提示词与方法：[@elvar_official](https://x.com/elvar_official) · [原文长文](https://x.com/elvar_official/article/2113949756376388093)
- 工具：Kimi K3.1 Pro · 3D Make

本仓库仅做收集与翻译，非原创。
