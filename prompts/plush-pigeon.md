# 毛绒鸽子 Plush Pigeon

- **系列**：Material Studies No. 031
- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · 布料
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `布料模拟` `程序化动画` `合成音效` `创意编程` `vibe-coding`

> 说明："Plush Penguin" 引擎来自 [@vib3coded](https://x.com/vib3coded) 的 Material Studies 系列（毛绒企鹅），这条提示词要求在同一引擎上做一只毛绒鸽子。该引擎源码未公开，没有引擎时可让 AI 按同样的结构从头搭建。界面上的工具名（Hand / Finger / Comb）、配色名（Blue bar / Ash red / Snow）和读数（mass / volume / steps / coos）保持英文。英文原文附在文末。

---

## 效果

![毛绒鸽子 Plush Pigeon](../assets/plush-pigeon.jpg)

## 提示词（中文）

在 Plush Penguin WebGPU 引擎上制作 "Plush Pigeon"（Material Studies No. 031）：XPBD 软体晶格（XPBD soft-body lattice）、壳层毛发（shell fur）、布料翅膀（cloth wings）、由姿态驱动的步态（posture-driven gait），以及三种工具 Hand（手）/ Finger（手指）/ Comb（梳子）。

### 玩具本体

一只圆滚滚、吃得很饱的原鸽（rock dove），用柔软的灰色水晶绒（minky）制成。

- **形状**：用一个 SDF（有向距离场）构成：圆圆的身体、挺起的胸脯、一段脖子向上连到青绿色（teal）的圆顶脑袋、一条带深色横带的扁平尾巴，以及两只粉色毛毡脚，每只三趾朝前、一趾朝后。
- **颈环**：带虹彩光泽，上半部偏绿、下半部偏紫，在胸前位置向下垂得更低。
- **脸部**：有光泽的珠子眼睛，外圈为橙色眼环；一个小小的深色毛毡喙，喙基部有浅色的蜡膜（cere）。
- **翅膀**：两只填充棉花的布料翅膀缝在肩部，沿身体两侧向下、向后折叠，每只翅膀上有两道炭灰色翼斑（bars），翼尖颜色更深。
- **毛长**：头部和颈环处的毛更短，脚部剪短到毛毡质感。

### 生命感（行为）

- **昂首阔步（Strut）**：一种摇摇摆摆的走路方式，脖子部位晶格单元的剪切肌肉（shear muscles）让脑袋随每一步前后点动。弯曲法向必须与脖子轴线保持正交，否则剪切力会推动整个身体。
- **咕咕叫（Coo）**：胸部单元鼓起，脑袋鞠躬两次，并播放一段合成的三音滚动 "croo" 叫声。
- **拍翅（Flap）**：拍打翅膀并伴随小跳，同时有羽毛扑簌的声音。
- **摔倒（Topple）**，然后自己爬起来。
- **手指（Finger）**：鸽子会踱步走向举着的手指；轻点（boop）它的喙会让它咕咕叫；闲着时它有时也会自己咕咕叫。

### 配色

Blue bar（蓝灰斑）、Ash red（灰红）、Snow（雪白）。

### 读数

mass（质量）、volume（体积）、steps（步数）、coos（叫声次数）。

### 布局

响应式布局（适配桌面与手机）。

---

<details>
<summary>英文原文（English original）</summary>

```text
Make "Plush Pigeon" (Material Studies No. 031) on the Plush Penguin WebGPU engine: XPBD soft-body lattice, shell fur, cloth wings, posture-driven gait, tools Hand / Finger / Comb.

The toy: a round, well-fed rock dove of soft grey minky.
- Shape: one SDF with a round body, a proud chest, a neck rising into a teal domed head, a flat tail with a dark band, and two pink felt feet with three toes forward and one behind.
- Neck ring: iridescent, green above and violet below, dipping lower over the chest.
- Face: glossy bead eyes with an orange ring; a small dark felt beak with a pale cere.
- Wings: two stuffed cloth wings sewn at the shoulders, folded down and back along the sides, each with two charcoal bars and a darker tip.
- Fur length: shorter on the head and neck ring, cropped to felt on the feet.

Life:
- Strut: a waddle in which neck-cell shear muscles bob the head with every step. Keep the bend normal orthogonal to the neck axis, or the shear pushes the whole body.
- Coo: the chest cells swell, the head bows twice, and a synthesized three-note rolling "croo" plays.
- Flap: wing flaps with hops and a feather-flutter sound.
- Topple, then get back up.
- Finger: struts over to a held finger; a boop on the beak makes it coo; it sometimes coos when idle.

Palettes: Blue bar, Ash red, Snow.
Readouts: mass, volume, steps, coos.
Responsive layout.
```

</details>
