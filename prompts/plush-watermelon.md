# 毛绒西瓜 Plush Watermelon

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · 布料四肢
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Gemini 4 Argon vs Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111428909203866089) · [提示词帖](https://x.com/vib3coded/status/2111429205263007747) · 2026-10-17（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Gemini 4 Argon vs Claude Opus 5.5）。"Plush Penguin" 引擎来自作者的 Material Studies 系列（见本仓库 [毛绒企鹅 Plush Penguin](plush-penguin.md) 的提示词），引擎源码未公开，没有引擎时可让 AI 按同样的结构从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![毛绒西瓜 Plush Watermelon](../assets/plush-watermelon.jpg)

## 提示词（英文原文）

```text
Make "Plush Watermelon" (Material Studies No. 032) on the Plush Penguin WebGPU engine: XPBD soft-body lattice, shell fur, cloth limbs, posture-driven gait, Hand / Finger / Comb tools.

Shape (one SDF):
- A fat wedge cut from a sphere by two planes through one horizontal axis, about 76° apart.
- The axis is the top edge, so each cut face is a semicircle.
- The cut faces are slightly puffy and every seam is rounded.
- It sits on a small flat patch of its round rind.

Regions:
- Flesh: long fluffy red minky.
- Rind: a white band along the outer edge of both faces.
- Skin: green, with dark jagged stripes running pole to pole around the wedge's axis.
- Seeds: short-pile felt teardrops pointing in toward the axis, a few on the front face around the face, more on the back.

Front face: two bead eyes, rosy cheeks, and an embroidered smile thread laid into a short-pile groove.

Limbs: two brown felt legs stuck out in front, and two stubby felt cloth arms at the wedge's ends.

Actions:
- Toddle: walk on the legs.
- Rock: seesaw forward and back on the rind with a synthesized giggle.
- Wave: arm waves and hops with a toy squeak.
- Topple: fall onto its back, then get back up.
- A finger boop on the face makes it giggle and rock; it also rocks now and then when idle.

Palettes: Classic, Yellow, Sorbet.
Readouts: mass, volume, steps, rocks.
Responsive layout with no horizontal overflow on phones.
```

---

## 提示词（中文）

在 Plush Penguin WebGPU 引擎上制作 "Plush Watermelon"（毛绒西瓜，Material Studies No. 032）：XPBD 软体晶格、壳层毛发、布料四肢、由姿态驱动的步态，以及 Hand / Finger / Comb 工具。

### 形状（一个 SDF）

- 用两个经过同一水平轴、夹角约 76° 的平面从球体上切下的一块胖胖的楔块。
- 该轴就是顶边，所以每个切面都是半圆。
- 切面略微鼓起，每条接缝都是圆润的。
- 它靠圆形瓜皮上一小块平坦的区域立着。

### 区域

- 果肉：长而蓬松的红色水晶绒（minky）。
- 瓜皮：沿两个切面外缘的一条白色带。
- 外皮：绿色，带深色锯齿状条纹，绕楔块的轴从一极延伸到另一极。
- 瓜子：短绒毛毡做的泪滴，尖端指向轴心，正面脸周围有几颗，背面更多。

正面：两颗珠子眼睛、红润的脸颊，以及一条嵌在短绒凹槽里的刺绣微笑线。

四肢：两条向前伸出的棕色毛毡腿，以及楔块两端两只短短的毛毡布手臂。

### 动作

- Toddle：用腿蹒跚走路。
- Rock：在瓜皮上前后跷跷板式摇晃，伴随合成的咯咯笑声。
- Wave：挥动手臂并跳跃，伴随玩具吱吱声。
- Topple：仰面倒下，然后自己爬起来。
- 用手指轻点脸部会让它咯咯笑并摇晃；空闲时它也会时不时摇晃。

配色：Classic、Yellow、Sorbet。

读数：mass、volume、steps、rocks。

响应式布局，在手机上无横向溢出。
