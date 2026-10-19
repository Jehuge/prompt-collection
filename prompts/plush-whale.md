# 毛绒鲸鱼 Plush Whale

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · surface nets
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `sdf` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2107869331556044814) · [提示词帖](https://x.com/vib3coded/status/2107869708091306390) · 2026-10-08（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。提示词里提到的「其他毛绒研究（plush studies）」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![毛绒鲸鱼 Plush Whale](../assets/plush-whale.jpg)

## 提示词（中文）

构建一个单文件 WebGPU 交互式 "Plush Whale"（毛绒鲸鱼），与我其他毛绒研究保持同样的摄影棚风格：浅色无缝背景（cyclorama），衬线刊头 "Material Studies / No. 019"，右侧是标本控制面板，左下是实时读数，并有 "Inside the experiment" 说明。

### 身体

一个有向距离场（SDF）——巨大圆钝的头部，逐渐收细到纤细的尾柄，宽阔的**水平**尾鳍（带凹口），两只长鳍肢和一个小背鳍凸起。把它模拟成软体：在六面体晶格上做 XPBD（每个单元做形状匹配 + 四面体体积保持），用 surface nets 生成渲染网格并蒙皮到晶格上。

### 游动

没有骨骼。鲸鱼用尾鳍游泳，不像鱼那样左右摆动，所以要做一个**竖直**弯曲的行波。每个单元的静止形状在顶部或底部被稍微拉长，越靠近尾部幅度越大，越靠后的单元相位越滞后，于是填充物会拱起、下沉，尾鳍上下拍打。小幅侧向弯曲让身体在转弯时弯曲。头部上一个弱的姿态拉力让它绕一个缓慢的圆圈转；关掉 "Circle" 时，它保持一个四分之三侧面的姿势。

### 脸部与细节

- 低低地镶在头部的小玻璃安全眼。
- 深色的背部和浅色的腹部面板，腹部下方有沿身体延伸的缝线喉褶。
- 缝出来的喷水孔和泛红的脸颊。
- 鳍和尾鳍用单独的颜色（座头鲸配色下为白色）。
- 一张长长的微笑嘴：绕头部前方真正切开的一道口子，内衬红色毛毡，嘴角有小小的向上卷曲的缝线。下颌在渲染时绕铰链张开。

### 喷水

大约每 10 秒（或按需），从喷水孔喷出一股由浅蓝和白色毛毡绒球"水滴"组成的喷泉。它们上升、落下，在摄影棚地面上弹跳，然后淡出。

### 毛发

壳层毛发（shell fur，alpha-to-coverage，4x MSAA），带 Kajiya-Kay 高光、天鹅绒般的倒伏，以及一个能把绒毛梳顺的梳子工具。

### 交互

- Hand（手）：抓住它甩动。抓住尾鳍时它拍得最用力；松手后它潜下去并恢复绕圈。
- Finger（手指）：轻点它的鼻子，它会扭动并脸红。
- Feed krill（喂磷虾）：投下一小团粉色毛毡磷虾。鲸鱼转身靠近，张大嘴吞下它们，然后开心地喷水。
- 按钮：Spout（喷水）、Feed krill（喂磷虾）、Dive（下潜：一阵快速的尾鳍拍打，伴随深深的海豚式翻滚）、Gulp（吞咽）、Smooth fur（抚平毛发）、Reset、Pause。
- 滑块：Stuffing（填充）、Pile（绒毛长度）、Fluke beat（尾鳍拍打频率）。
- 外观：Ocean（蓝色）、Humpback（炭灰色配白色鳍肢）、Lilac（淡紫）。
- 读数：Mass（质量）、Volume（相对静止状态的体积百分比）、Beat /min（每分钟拍打次数）、Krill gulps（吞下的磷虾数）。
- 支持移动端：堆叠布局、触摸、双指缩放。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file WebGPU interactive "Plush Whale" in the same studio style as my other plush studies: pale cyclorama background, serif masthead "Material Studies / No. 019", specimen control panel on the right, live readouts bottom-left, "Inside the experiment" notes.

Body: one signed-distance field — a big round blunt head tapering to a slim tail stock, wide HORIZONTAL tail flukes with a notch, two long flippers and a small dorsal bump. Simulate it as a soft body: XPBD on a hexahedral lattice (shape matching per cell + tetrahedral volume preservation), with a surface-nets render mesh skinned to the lattice.

Swimming: no bones. A whale swims with its flukes, not side to side like a fish, so make a travelling wave of VERTICAL bending. Each cell's rest shape is stretched a little longer on top or underneath, growing toward the tail and arriving later the further back the cell is, so the stuffing arches and dips and the flukes beat up and down. A small sideways bend curves the body into turns. A weak posture pull on the head turns it round a slow circle; "Circle" off makes it hold a three-quarter pose.

Face and details:
- Small glass safety eyes set low on the head.
- A deep back colour and a pale belly panel with stitched throat grooves running along the underside.
- A stitched blowhole and blushing cheeks.
- Fins and flukes in their own colour (white on the humpback finish).
- A long smiling mouth: a real cut round the front of the head, lined with red felt, with little stitched upward curls at the corners. The lower jaw drops open on a hinge at render time.

The spout: every 10 seconds or so (or on demand), a fountain of fluffy felt pom-pom droplets in pale blues and white bursts from the blowhole. They rise, rain down, bounce on the studio floor and fade.

Fur: shell fur (alpha-to-coverage, 4x MSAA) with Kajiya-Kay highlights, velvet lean, and a comb tool that lays the pile.

Interactions:
- Hand: grab and swing it. Held by the flukes it flaps hardest; released, it dives off and resumes circling.
- Finger: boop its nose and it wriggles and blushes.
- Feed krill: drops a little cloud of pink felt krill. The whale turns, closes in, opens its mouth wide, gulps them, then spouts happily.
- Buttons: Spout, Feed krill, Dive (a burst of fast fluke beats with a deep porpoising roll), Gulp, Smooth fur, Reset, Pause.
- Sliders: Stuffing, Pile, Fluke beat.
- Finishes: Ocean (blue), Humpback (charcoal with white flippers), Lilac.
- Readouts: Mass, Volume % of rest, Beat /min, Krill gulps.
- Works on mobile: stacked layout, touch, pinch zoom.
```

</details>
