# 螃蟹果冻 Crab Jelly

- **类型**：交互网页 / 果冻生物
- **技术栈**：WebGPU · XPBD 软体
- **标签**：`webgpu` `xpbd` `软体模拟` `果冻` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109588091069452587) · [提示词帖](https://x.com/vib3coded/status/2109588435841228822) · 2026-10-12（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来测试 AI 模型的提示词（帖子展示的是 Claude Opus 5.5 的结果）。提示词里提到的「Octo Jelly / Squid Jelly / Fugu Jelly」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建一个名为 "Crab Jelly"（螃蟹果冻）的单文件 WebGPU "material study" 页面，延续我的果冻生物系列（Octo Jelly / Squid Jelly / Fugu Jelly）的风格：编辑式布局，大号斜体衬线标题 "Crab / Jelly."，眉标 "Material Studies"，一句简短而有诗意的说明，实时状态标签，右侧玻璃控制面板，统计行，可折叠的 "Inside the experiment" 说明。界面为英文，支持移动端，60 fps。

### 生物

一只由果冻做成的半透明软糖螃蟹——宽而圆的蟹壳、两只长在小眼柄上的眼睛、两只大钳子和八条分节的步足——坐在柔和纸质摄影棚中的一个白盘子上。果冻有真实的折射和次表面辉光，蟹壳上有较深的糖晶斑点，有光泽的湿润高光，柔和的接触阴影，内部困着细小气泡。

### 物理

身体和钳子用 XPBD 软体（形状匹配单元 + 四面体体积保持），让整只螃蟹像果冻一样晃动、颤动；腿是链条，在盘子上保持落脚。

### 行为

- Scuttle（用八条腿一阵阵地横着跑）
- Snap（钳子张开再拍合，带一下颤动）
- Wave（举起一只钳子挥动）
- Dig（扭动着钻进一小堆糖沙里，直到只露出眼睛）
- Flip（翻倒仰面朝天，腿乱划，然后自己翻回来）

### 交互

戳它会晃动并横着后退；按压蟹壳会压扁再弹回；抓住蟹壳把它拿起来——腿会悬垂并乱蹬；拖动一只钳子它会夹住你的指针；扔下它会弹跳。

滑块：Firmness（软 ↔ 硬果冻）、Wobble damping（晃动阻尼）、Light（摄影棚灯光角度）。口味：Strawberry（草莓红）、Mango（芒果橙金）、Blue raspberry（蓝树莓）。Reset、Pause、¼ speed。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file WebGPU "material study" page called "Crab Jelly", in the style of my jelly creature series (Octo Jelly / Squid Jelly / Fugu Jelly): editorial layout, large italic serif title "Crab / Jelly.", kicker "Material Studies", a short poetic caption, live status chip, glass control panel on the right, stats row, collapsible "Inside the experiment" notes. UI in English, works on mobile, 60 fps.

The creature: a translucent gummy crab made of jelly — a wide rounded carapace, two eyes on little stalks, two big claws and eight jointed walking legs — sitting on a white plate in a soft paper studio. Real refraction and subsurface glow through the jelly, a darker sugar-crystal speckle on the shell, a glossy wet highlight, soft contact shadow, tiny air bubbles trapped inside.

Physics: XPBD soft body (shape-matched cells + tetrahedral volume preservation) for the body and claws, so the whole crab wobbles and jiggles like jelly; legs as chains that keep their footing on the plate. Behaviours: Scuttle (runs sideways in short bursts on its eight legs), Snap (claws open and clap shut with a jiggle), Wave (raises one claw and waves), Dig (wriggles down into a little heap of sugar sand until only the eyes poke out), Flip (falls on its back, legs paddling, then rights itself). Interactions: poke it and it wobbles and backs away sideways; press on the shell and it squashes and springs back; pick it up by the carapace — legs dangle and kick; drag a claw and it pinches your pointer; drop it and it bounces. Sliders: Firmness (soft ↔ firm jelly), Wobble damping, Light (studio angle). Flavours: Strawberry (red), Mango (orange-gold), Blue raspberry (blue). Reset, Pause, ¼ speed.
```

</details>
