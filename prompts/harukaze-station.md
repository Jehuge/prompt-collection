# 春风站 Harukaze Station

- **类型**：交互网页 / 低多边形微缩场景
- **技术栈**：Three.js · MeshToonMaterial · OutlineEffect
- **标签**：`threejs` `low-poly` `toon` `日本车站` `樱花` `昼夜` `vibe-coding` `ai-测试`
- **测试模型**：Gemini 4 Argon vs Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111965632338292943) · [提示词帖](https://x.com/vib3coded/status/2111965978770669760) · 2026-10-19（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Gemini 4 Argon vs Claude Opus 5.5）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![春风站 Harukaze Station](../assets/harukaze-station.jpg)

## 提示词（中文）

构建一个单文件自包含 HTML：一个春天里日本乡村火车站的交互式低多边形 3D 微缩场景，使用 Three.js（从 CDN 引入 ES 模块）。不使用外部模型或图片——所有几何体都在代码中由基本体生成，纹理（草地、标牌）在 <canvas> 上绘制。

### 风格

一个漂浮的微缩场景块（顶部是草地，侧面是分层的泥土和石头），背景是柔和的粉彩天空渐变。使用带 3 级渐变贴图的 MeshToonMaterial、深色墨线描边（OutlineEffect）、柔和的平行光阴影、明亮饱和的配色。

### 场景

- 一条横穿场景块的单线铁轨，两端驶入长满绿草、带混凝土洞口的隧道山丘。
- 混凝土站台，带黄色盲道，带波纹板屋顶的候车棚，长椅，悬挂的时钟，一座带青绿色人字形屋顶和 "春風駅" 招牌的小站房，站名牌（はるかぜ / Harukaze，并标出相邻车站），自动售货机，垃圾桶，路灯，围栏。
- 一条与铁轨相交的道路，带平交道口：条纹立柱、X 形警示标志、红色闪烁灯、栏杆臂；道路标线和 "止まれ"。
- 带下垂电线的电线杆、架空接触网、村庄小房子、一块菜地、灌木丛，以及樱花树——蓬松的粉色团块树冠，草地上画着落下的花瓣。

### 动画

- 一列两节编组的通勤列车（白色车身配粉色条纹，带受电弓）从一个隧道驶出，在站台停靠，然后驶入另一个隧道；用裁切平面把它在隧道内的部分隐藏。每约 32 秒循环一次。
- 列车通过前，道口灯交替闪烁、栏杆放下，通过后再升起。
- 约 460 片实例化的樱花花瓣随风飘动。
- 相机缓慢自动环绕；用 OrbitControls 实现拖动和缩放。

### UI（英文）

左下标题 "春風駅 / Harukaze Station" 配一行小说明；右下玻璃工具栏，包含 Day / Night、Orbit on/off 和 Train（呼叫下一班列车）。夜间模式：带星星的深色天空，亮着灯的窗户，带加法混合辉光精灵的路灯点光源，发光的道口灯和列车前灯。

### 技术

按材质合并静态网格，控制在几十次绘制调用以内；使用带种子的随机数，让每次加载场景都完全相同；响应式适配到手机宽度；遵守 prefers-reduced-motion。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single self-contained HTML file: an interactive low-poly 3D diorama of a rural Japanese railway station in spring, using Three.js (ES modules from a CDN). No external models or images — generate all geometry from primitives in code and paint textures (grass, signs) on <canvas>.

Style: a floating diorama block (grass top, layered earth and stone sides) on a soft pastel sky gradient. MeshToonMaterial with a 3-step gradient map, dark ink outlines (OutlineEffect), soft directional shadows, bright saturated palette.

Scene:
- A single railway track across the block, running into green tunnel hills with concrete portals at both ends.
- Concrete platform with a yellow tactile strip, a shelter with a corrugated roof, benches, a hanging clock, a small station building with a teal gable roof and a "春風駅" sign, a station name board (はるかぜ / Harukaze, with neighbouring stations), vending machines, bins, lamps, fence.
- A road crossing the track with a level crossing: striped poles, crossbuck, red flashing lamps, barrier arms; road markings and "止まれ".
- Utility poles with sagging wires, overhead catenary, small village houses, a vegetable patch, bushes, and cherry trees with puffy pink blob crowns and fallen petals painted on the grass.

Animation:
- A two-car commuter train (white with a pink stripe, pantograph) comes out of one tunnel, stops at the platform, then departs into the other; clipping planes hide it inside the tunnels. Loop every ~32 s.
- Crossing lamps blink alternately and the arms lower before the train passes, then rise.
- ~460 instanced sakura petals drifting in the wind.
- Slow auto-orbit camera; OrbitControls for drag and zoom.

UI (English): bottom-left title "春風駅 / Harukaze Station" with a small caption; bottom-right glass toolbar with Day / Night, Orbit on/off, and Train (call the next train). Night mode: dark sky with stars, lit windows, lamp point lights with additive glow sprites, glowing crossing lamps and train headlights.

Technical: merge static meshes by material into a few dozen draw calls; use a seeded random so the scene is identical on every load; responsive down to phone width; respect prefers-reduced-motion.
```

</details>
