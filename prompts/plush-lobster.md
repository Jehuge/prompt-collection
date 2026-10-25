# 毛绒龙虾 Plush Lobster

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `sdf` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2112838135927263740) · [提示词帖](https://x.com/vib3coded/status/2112838288104972598) · 2026-10-21（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。提示词要求沿用作者此前的 Plush Crab 引擎和版式，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![毛绒龙虾 Plush Lobster](../assets/plush-lobster.jpg)

## 提示词（英文原文）

```text
Build a real-time WebGPU plush-toy study of a cute stuffed lobster, in the same engine and editorial "Material Studies" page style as my Plush Crab (shell-rendered minky fur, XPBD soft body, wired legs).

Body: one signed distance field — a long domed carapace with a rounder face and a small horn, two short eye stalks with big glossy safety eyes on white felt discs, an embroidered smile and rosy cheeks, then a tail of six smooth-unioned segments that get smaller toward the back, with a crease between each, ending in a flat five-paddle tail fan. Fill it with a hex lattice of cells and tetrahedra, solved with co-rotational cell shape matching plus volume constraints on a fixed 60 Hz step; Coulomb friction on the table. The shell breathes. Only the shell keeps its footing and posture, so the tail stays free.

Tail muscle: along the tail's centre line, lengthen the cells' rest shapes above the line and shorten them below, so the stuffing itself curls the tail. At rest the tail gently lifts and settles. "Tail flip": snap the tail under hard in about 0.1 s with extra cell stiffness, throw the body back and up, and straighten the tail again mid-air so it lands stretched out well behind where it started. A finger poke on the shell triggers the same flip.

Chains (XPBD rods with a plastic wire, posed in the body frame, blended poses lie/stand/tuck/wave/hang):
- eight thin walking legs with pale knitted joint bands;
- two arms ending in a big padded palm with two plush claw fingers (dark felt tips) that open and close by one angle;
- two long thin striped feelers that sweep up and back and always twitch slightly.

Behaviours:
- walking: head first, an alternating gait with footholds on the table;
- "Snip snip": both claws open and shut out of step;
- "Wave claws": claws raised and waving;
- Finger tool: the lobster walks to the finger, faces it and pinches it gently;
- held up, its legs dangle;
- pulling a limb past its reach tows the whole body.

Rendering: fur shells with Kajiya–Kay highlights, a velvet lie the Comb tool can brush, and pile that sways on springs. Draw the tail seams as stitched short-pile creases and give the fan pale edges. Soft shadows, contact AO, a studio backdrop, PBR Neutral tone mapping.

Varieties: Red, Blue, Golden. Tools: Hand, Finger, Comb. Sliders: stuffing, pile length, wire. Buttons: Walk, Snip snip, Tail flip, Wave claws, Straighten, Smooth fur, Reset, ¼ speed, Mesh, Pause. Readouts: mass, volume, steps, flips, snips. Add an "Inside the experiment" notes drawer. English UI, mobile-friendly.
```

---

## 提示词（中文）

构建一个实时 WebGPU 毛绒玩具研究：一只可爱的填充龙虾。引擎和编辑式 "Material Studies" 页面风格与我的 Plush Crab 相同（壳层渲染的 minky 短毛、XPBD 软体、腿里穿了金属丝）。

### 身体

身体是一个有向距离场。甲壳长，拱成圆顶，脸更圆，头顶有一只小角。两根短眼柄，大而有光泽的安全眼安在白色毡片上。一张绣出来的微笑，两团玫瑰色脸颊。尾巴是六个用 smooth-union 融合在一起的体节，越往后越小，节与节之间有一道折痕，末端是扁平的五叶尾扇。用六面体晶格的单元和四面体把它填满。求解用共旋转的单元形状匹配，加上体积约束，步长固定在 60 Hz。桌面上是库仑摩擦。外壳会轻轻起伏，像在呼吸。只有外壳维持落脚和姿态，所以尾巴是自由的。

### 尾巴的肌肉

沿尾巴的中线，把中线上方那些单元的静止形状拉长，把下方的缩短，于是填充物自己就把尾巴卷起来。静止的时候，尾巴轻轻抬起，再落下去。"Tail flip"：大约 0.1 秒内把尾巴用力收到身子下面，并额外加大单元的刚度，把身体向后、向上抛起来；到了空中再把尾巴伸直，这样落地时它是舒展开的，而且落点远在它出发位置的后面。用手指戳一下外壳，也会触发同一次甩尾。

### 链条

链条是 XPBD 杆，杆里有一根可塑形的金属丝，在身体坐标系里摆姿势。姿态在 lie / stand / tuck / wave / hang 之间混合：

- 八条细的行走腿，关节处有一圈浅色的针织环；
- 两条手臂，末端是带衬垫的大掌，两根毛绒钳指（尖端是深色毡），靠一个角度开合；
- 两根又长又细的条纹触角，向上、向后扫，并且一直在轻轻抽动。

### 行为

- 走路：头朝前，左右交替，落脚点踩在桌面上；
- "Snip snip"：两只螯一开一合，左右错开；
- "Wave claws"：螯举起来挥；
- Finger 工具：龙虾走到手指那里，面向它，轻轻夹一下；
- 被提起来的时候，腿是垂着的；
- 把一只肢体拉得超过它能够到的范围，会把整个身体拖过去。

### 渲染

壳层毛发，带 Kajiya–Kay 高光。毛有一个丝绒倒向，Comb 工具可以把它梳过去。毛长挂在弹簧上，会晃。尾巴的接缝画成缝好的短毛折痕，尾扇的边缘用浅色。柔和的阴影、接触 AO、摄影棚背景、PBR Neutral 色调映射。

### 品种与控制

品种：Red、Blue、Golden。工具：Hand、Finger、Comb。滑块：stuffing、pile length、wire。按钮：Walk、Snip snip、Tail flip、Wave claws、Straighten、Smooth fur、Reset、¼ speed、Mesh、Pause。读数：mass、volume、steps、flips、snips。加一个 "Inside the experiment" 说明抽屉。界面为英文，适配手机。
