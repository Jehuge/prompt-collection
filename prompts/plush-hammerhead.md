# 毛绒双髻鲨 Plush Hammerhead

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · surface nets
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `sdf` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2108486895344767283) · [提示词帖](https://x.com/vib3coded/status/2108487206155194794) · 2026-10-09（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![毛绒双髻鲨 Plush Hammerhead](../assets/plush-hammerhead.jpg)

## 提示词（中文）

构建一个名为 "Plush Hammerhead"（毛绒双髻鲨）的单文件交互式 WebGPU 页面。

### 页面

编辑式布局，大号两行标题 "Plush / Hammerhead."，暖色摄影棚灰背景，右侧控制面板，实时读数和可折叠的技术说明。界面为英文。

### 玩具本体

一只毛绒双髻鲨。它有一个宽而扁的锤形头部（头翼 cephalofoil），两端略向后掠，前缘中间有一个浅凹口。锤头两端各有一只玻璃眼，朝两侧看。它有一个高高的镰刀形背鳍、两只胸鳍，以及上叶长、下叶小的尾巴。奶油色腹部面板缝在两侧体侧的接缝下方，带绣出来的鳃线。锤头下方切出一张微笑的嘴，内衬毛毡，镶着柔软的白色毛毡牙齿；下颌绕铰链张开。

### 模拟

- 身体、锤头和鳍是同一个有向距离场，内部填充 XPBD 软体晶格：做形状匹配的六面体单元和四面体体积保持。蒙皮到高分辨率的 surface-nets 网格上。
- 它通过一个 S 形行波游动，左右弯曲单元的静止形状，越靠近尾部幅度越大；通过转头来转向，身体随每次转弯弯曲。
- 毛发用 alpha-to-coverage 壳层绘制在水晶绒（minky）绒面上。绒毛通过弹簧在每次晃动后滞后，并可以梳理。

### 行为

- 它在自己的空间里绕圈。
- Scan（扫描）：像真正的双髻鲨捕猎那样，把锤头在地面上方左右扫动。它也会时不时自己这样做，捕猎时也会扫一会儿。
- Feed 投下一条毛毡鱼：它转身，加速靠近，张大嘴一口咬住。
- Dash 是一阵快速的尾巴拍打；Chomp 张嘴再猛地合上。
- 抓住它的尾巴它会挣扎；松手它就冲出去。
- 用手指轻点锤头中间，它会扭动并脸红。

### 工具

Hand、Finger、Comb。

### 控制

- 按钮：Feed、Dash、Scan、Chomp、Smooth fur、Reset、Pause。
- 开关：Circle（绕圈）、quarter speed（¼ 速）、Mesh（网格）。
- 滑块：Stuffing、Pile、Tail beat。
- 三种布料：Bronze（古铜）、Lagoon（泻湖）、Sunset（日落）。
- 读数：质量、体积、每分钟拍尾次数、吃掉的鱼数。
- 手机布局采用堆叠面板。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file interactive WebGPU page called "Plush Hammerhead".

Page: an editorial layout with a big two-line title "Plush / Hammerhead.", a warm studio-grey background, a control panel on the right, live readouts and collapsible technical notes. English UI.

The toy: a plush hammerhead shark. It has a wide, flat hammer-shaped head (cephalofoil) whose ends sweep back a little, with a shallow notch at the middle of the front edge. A glass eye sits on each tip of the hammer, looking out sideways. It has a tall sickle-shaped dorsal fin, two pectoral fins and a tail with a long upper lobe and a small lower one. A cream belly panel is sewn on below a seam along each flank, with embroidered gill lines. A smiling mouth is cut in under the hammer, lined with felt and set with soft white felt teeth; its lower jaw swings open on a hinge.

Simulation:
- Body, hammer and fins are one signed distance field filled with a soft-body XPBD lattice: shape-matched hexahedral cells and tetrahedral volume preservation. It is skinned to a high-res surface-nets mesh.
- It swims with a travelling S-wave that bends the cells' rest shapes side to side, more toward the tail, and steers by turning its head, the body curving into each turn.
- Fur is drawn as alpha-to-coverage shells over minky pile. The pile lags behind each jiggle on a spring and can be combed.

Behaviour:
- It circles its space.
- Scan: it sweeps its hammer side to side over the floor the way real hammerheads hunt. It also does this on its own now and then, and a little while hunting.
- Feed drops in a felt fish: it turns, closes in faster, opens wide and snaps it up.
- Dash is a burst of fast tail beats; Chomp opens the mouth and snaps it shut.
- Grab it by the tail and it thrashes; let go and it shoots off.
- Boop the middle of the hammer with the finger and it wriggles and blushes.

Tools: Hand, Finger, Comb.

Controls:
- Buttons: Feed, Dash, Scan, Chomp, Smooth fur, Reset, Pause.
- Toggles: Circle, quarter speed, Mesh.
- Sliders: Stuffing, Pile, Tail beat.
- Three fabrics: Bronze, Lagoon, Sunset.
- Readouts: mass, volume, beats per minute, fish eaten.
- Phone layout with a stacked panel.
```

</details>
