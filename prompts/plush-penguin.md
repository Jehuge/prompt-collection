# 毛绒企鹅 Plush Penguin

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · 粒子布料
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `布料模拟` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：ChatGPT-6 Astra vs Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109288662319919127) · [提示词帖](https://x.com/vib3coded/status/2109288858701455535) · 2026-10-11（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 ChatGPT-6 Astra vs Claude Opus 5.5）。这就是 [毛绒鸽子 Plush Pigeon](plush-pigeon.md)、[毛绒西瓜 Plush Watermelon](plush-watermelon.md) 所基于的 "Plush Penguin" 引擎的原始提示词。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![毛绒企鹅 Plush Penguin](../assets/plush-penguin.jpg)

## 提示词（中文）

构建一个名为 "Plush Penguin"（毛绒企鹅）的单文件 WebGPU "material study" 页面：编辑式摄影棚布局，大号斜体衬线标题 "Plush / Penguin."，眉标 "Material Studies / No. 016"，说明文字 "A fluffy egg on two felt feet. It waddles, it toboggans, it falls over — and always gets back up."，实时状态标签，右侧标本面板，统计行（Mass、Volume、Steps、Slide in cm），可折叠的 "Inside the experiment" 说明。界面为英文，支持移动端。

### 玩具本体

一只圆滚滚的毛绒企鹅宝宝——蛋形的填充身体是一个 SDF，用 surface nets 生成网格；深色的头顶和背部，浅色蓬松的脸和肚子，大而有光泽的安全玻璃眼，小小的毛毡喙，粉色脸颊，两只扁平的毛毡脚。它的鳍状翅膀是单独的布片（粒子布料，缝在嵌入身体的点上），会耷拉、拍动和拉伸。

### 物理

六面体晶格上的 XPBD 软体（形状匹配单元 + 四面体体积保持，实时体积读数），蒙皮到网格，站在有库仑摩擦的桌面上。靠姿态移动：一个把整个身体拉向其静止形状的弱拉力，该静止形状被旋转到某个朝向并随质心移动，于是由填充物来完成移动。

### 行为

- Waddle（左右摇摆着走，每只脚抬起再放到前方）
- Belly slide（小跳一下，向前扑到肚子上，在桌面上滑行，然后摇晃着起来）
- Flap（开心地拍翅膀并跳几下）
- Topple（向后、向前或侧面倒下，再带一点过冲地摇正自己）
- Smooth fur、Reset。
- Finger：它会摇摇摆摆走向你的手指；推它会摔倒。
- Hand：把它拿起来、挤压它，拉一只翅膀它会跟着过来。

### 毛发

带 alpha-to-coverage 的实时壳层毛发——身体上是长而蓬松的绒毛，脸上是短毛，可以用 Comb 工具梳理（逆毛方向更暗，顺毛更亮）。滑块：Stuffing、Pile（mm）、Table（桌面：毛毡 ↔ 冰面摩擦，在冰面上滑得更远）。配色：Chick（雏鸟）、Classic（经典）、Little blue（小蓝企鹅）。¼ speed 和 mesh 开关、Pause。60 fps。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file WebGPU "material study" page called "Plush Penguin": editorial studio layout, large italic serif title "Plush / Penguin.", kicker "Material Studies / No. 016", caption "A fluffy egg on two felt feet. It waddles, it toboggans, it falls over — and always gets back up.", live status chip, specimen panel on the right, stats row (Mass, Volume, Steps, Slide in cm), collapsible "Inside the experiment" notes. UI in English, works on mobile.

The toy: a round plush penguin chick — an egg-shaped stuffed body as one SDF meshed with surface nets, a dark cap and back, a pale fluffy face and belly, big glossy safety-glass eyes, a small felt beak, pink cheeks, two flat felt feet. Its flippers are separate cloth pieces (particle cloth sewn to points embedded in the body) that flop, flap and stretch.

Physics: XPBD soft body on a hex lattice (shape-matched cells + tetrahedral volume preservation, live volume readout), skinned to the mesh, standing on a table with Coulomb friction. Locomotion by posture: a weak pull of the whole body toward its rest shape turned to an orientation and carried with its centre of mass, so the stuffing does the moving. Behaviours: Waddle (rocks side to side, lifting each foot and setting it down ahead), Belly slide (a little hop, flops forward onto its tummy and toboggans across the table, then rocks back up), Flap (happy flapping and a couple of hops), Topple (falls onto its back, belly or side and rocks itself upright with an overshoot), Smooth fur, Reset. Finger: it waddles over to your finger; push it and it falls over. Hand: pick it up, squash it, pull a flipper and it comes along.

Fur: real-time shell fur with alpha-to-coverage — long fluffy down on the body, short on the face, combable with a Comb tool (against the grain darker, with it shinier). Sliders: Stuffing, Pile (mm), Table (felt ↔ ice friction, so it slides further on ice). Palettes: Chick, Classic, Little blue. ¼ speed and mesh toggles, Pause. 60 fps.
```

</details>
