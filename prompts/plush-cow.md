# 毛绒奶牛 Plush Cow

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · WebAudio
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `程序化动画` `合成音效` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2108572856044986846) · [提示词帖](https://x.com/vib3coded/status/2108572945110954170) · 2026-10-09（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来测试 AI 模型的提示词（帖子展示的是 Claude Opus 5.5 的结果）。提示词里提到的「之前的毛绒玩具（plush goat / crab / shark / penguin）」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![毛绒奶牛 Plush Cow](../assets/plush-cow.jpg)

## 提示词（中文）

构建一个名为 "Plush Cow"（毛绒奶牛）的单文件 WebGPU "material study" 页面，与我之前的毛绒玩具（plush goat / crab / shark / penguin）保持相同的摄影棚风格：编辑式布局，大号斜体衬线标题 "Plush / Cow."，眉标 "Material Studies / No. 029"，实时状态标签，带工具和滑块的标本面板，统计行（Mass、Volume、Steps、Moos），可折叠的 "Inside the experiment" 说明。界面为英文，支持移动端（无横向滚动）。

### 玩具本体

一只圆滚滚的毛绒荷斯坦奶牛（灵感来自那头用乳房奔跑的卡通奶牛），她用自己粉色大乳房上的四个乳头站立和奔跑——张开的乳头就是她仅有的腿。身体 = 一个光滑的 SDF（圆桶形身体、大脑袋、宽大的亮粉色口鼻、带褶痕的圆乳房、四个以毛毡垫收尾的乳头、一条末端带黑色蓬松尾簇的绳状尾巴），用 surface nets 生成网格。黑色荷斯坦斑块边缘不规则（其中一块围着一只眼睛），有光泽的纽扣眼，短短的奶油色毛毡角，绣出来的椭圆鼻孔和微笑，粉色腮红，以及两只缝在两侧、笔直向外伸出的布耳朵（外白内粉），会像翅膀一样扇动。

### 物理

六面体晶格上的 XPBD 软体（形状匹配单元 + 四面体体积保持，体积读数约 100%），蒙皮到网格。由姿态驱动的移动：乳头节点就是脚，有落脚目标、摆动抬升和引导点；以对角线成对小跑（左前 + 右后，然后另外两个）。

### 行为

- Trot（小跑，四处溜达）
- Gallop（弹跳着跑圈）
- Hop（腾空，耳朵像翅膀一样扇动）
- Moo（WebAudio 低沉锯齿波 "mmm-OOO"，经过开合的低通滤波，耳朵向上一抖，缓慢甩头）
- Topple（侧身摔倒，再摇晃着爬起来）
- Smooth fur、Reset。
- 用手指轻点她的鼻子会让她哞哞叫。

### 毛发

实时壳层毛发，逐顶点绒毛长度（柔软的皮毛、头部短毛、天鹅绒般的粉色口鼻和乳房、长长的尾簇和额前刘海），可以用 Comb 工具梳理。工具：Hand（抓住并挤压、拉耳朵）、Finger（戳 / 她会跟着手指走）、Comb。滑块：Stuffing、Pile（mm）、Table friction（桌面摩擦：毛毡 ↔️ 冰面）。配色：Holstein（荷斯坦）、Jersey（娟姗）、Strawberry（草莓）。60 fps。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file WebGPU "material study" page called "Plush Cow" in the same studio style as my previous plush toys (plush goat / crab / shark / penguin): editorial layout, large italic serif title "Plush / Cow.", kicker "Material Studies / No. 029", live status chip, specimen panel with tools and sliders, stats row (Mass, Volume, Steps, Moos), collapsible "Inside the experiment" notes. UI in English, works on mobile (no horizontal scroll).

The toy: a round stuffed Holstein cow (inspired by the cartoon cow that runs on its udder) who stands and runs on the four teats of her big pink udder — the splayed teats are her only legs. Body = one smooth SDF (round barrel body, big head, wide hot-pink muzzle, rounded udder with a crease, four teats ending in felt pads, a rope tail with a black shaggy tuft) meshed with surface nets. Black Holstein spots with wobbly edges (one around an eye), glossy button eyes, stubby cream felt horns, embroidered oval nostrils and a smile, pink blush, and two cloth ears sewn on sticking straight out at the sides (white outside, pink inside) that flap like wings.

Physics: XPBD soft body on a hex lattice (shape-matched cells + tetrahedral volume preservation, volume readout ~100%), skinned to the mesh. Posture-driven locomotion: teat nodes are feet with footing targets, swing lift and a lead point; trot in diagonal pairs (front-left + back-right, then the others). Behaviours: Trot (wanders), Gallop (bouncy laps), Hop (airborne, ears beat like wings), Moo (WebAudio low sawtooth "mmm-OOO" through an opening/closing lowpass, ears flick up, slow head toss), Topple (falls on her side and rocks back up), Smooth fur, Reset. Booping her nose with the finger makes her moo.

Fur: real-time shell fur with per-vertex pile (soft coat, short head, velvety pink muzzle and udder, long tail tuft and forelock), combable with the Comb tool. Tools: Hand (grab & squash, pull ears), Finger (poke / she follows it), Comb. Sliders: Stuffing, Pile (mm), Table friction (felt ↔️ ice). Palettes: Holstein, Jersey, Strawberry. 60 fps.
```

</details>
