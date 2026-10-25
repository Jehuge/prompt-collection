# 毛绒枪鱼 Plush Marlin

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · surface nets
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `sdf` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：ChatGPT-6 Astra vs Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2108850731750940711) · [提示词帖](https://x.com/vib3coded/status/2108852066655351202) · 2026-10-10（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 ChatGPT-6 Astra vs Claude Opus 5.5）。提示词里提到的「plush hammerhead / plush shark」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![毛绒枪鱼 Plush Marlin](../assets/plush-marlin.jpg)

## 提示词（英文原文）

```text
Build a single-file WebGPU "material study" page called "Plush Marlin" in the same studio style as my plush hammerhead / plush shark: editorial layout, italic serif title "Plush / Marlin.", kicker "Material Studies / No. 030", live status chip, specimen panel (tools, fur palettes, sliders, action buttons), stats row (Mass, Volume, Beat, Fish eaten), collapsible "Inside the experiment" notes. UI in English, works on mobile.

The toy: a plush blue marlin, normal and realistic in proportion (not a meme). One SDF body meshed with surface nets: a long fusiform body, deep behind the head and slender at the tail stock, laterally compressed; a long tapering felt bill (spear) from the upper jaw, slightly upturned; a tall sail-like first dorsal fin raked back from a high peak over the head and running low down the back; a small second dorsal and anal fin; long narrow scythe pectorals and thin pelvic fins; a tall crescent (lunate) tail with the notch scooped out; big glass eyes; a small mouth slit under the bill with a lower jaw that swings open on a hinge.

Physics: XPBD soft body on a hex lattice (shape-matched cells + tet volume preservation), skinned to the mesh. It swims with a stiff travelling wave mostly in its back third, circles, banks into turns. Behaviours: Feed (a felt fish drops in; it hunts it down and snaps it up), Dash, Slash (quick side-to-side swipes of the bill, like a marlin stunning prey), Light up (its flank bars glow electric blue; they also flash when you touch its bill or when it eats). Grab it by the tail and it thrashes.

Fur: real-time shell fur — cobalt back, silver belly panel below a seam, pale vertical bars on the flanks, dark spots on the sail, an embroidered gill-cover seam, bare felt bill. Tools: Hand, Finger, Comb. Sliders: Stuffing, Pile, Tail beat. Palettes: Blue, Black, Indigo. 60 fps.
```

---

## 提示词（中文）

构建一个名为 "Plush Marlin"（毛绒枪鱼）的单文件 WebGPU "material study" 页面，与我的 plush hammerhead / plush shark 保持相同的摄影棚风格：编辑式布局，斜体衬线标题 "Plush / Marlin."，眉标 "Material Studies / No. 030"，实时状态标签，标本面板（工具、毛色配色、滑块、动作按钮），统计行（Mass、Volume、Beat、Fish eaten），可折叠的 "Inside the experiment" 说明。界面为英文，支持移动端。

### 玩具本体

一只毛绒蓝枪鱼，比例正常写实（不是表情包风格）。一个 SDF 身体，用 surface nets 生成网格：长纺锤形身体，头后方最厚，尾柄处纤细，左右侧扁；从上颌伸出一根长长的、逐渐变细的毛毡吻（长矛），微微上翘；高耸如帆的第一背鳍，从头顶上方的高峰向后倾斜，沿背部低低延伸；小的第二背鳍和臀鳍；细长的镰刀形胸鳍和细腹鳍；高大的新月形（lunate）尾鳍，中间挖出凹口；大玻璃眼；吻下方一道小嘴缝，下颌可绕铰链张开。

### 物理

六面体晶格上的 XPBD 软体（形状匹配单元 + 四面体体积保持），蒙皮到网格。它用一个僵硬的行波游动，主要集中在身体后三分之一，绕圈游，转弯时倾斜。

### 行为

- Feed（投下一条毛毡鱼；它追上去一口咬住）
- Dash（冲刺）
- Slash（用吻快速左右挥砍，像枪鱼击晕猎物那样）
- Light up（体侧条纹发出电光蓝；碰它的吻或它进食时也会闪烁）
- 抓住它的尾巴它会挣扎。

### 毛发

实时壳层毛发——钴蓝色背部，接缝下方是银色腹部面板，体侧有浅色竖条纹，背鳍"帆"上有深色斑点，绣出来的鳃盖接缝，裸露的毛毡吻。工具：Hand、Finger、Comb。滑块：Stuffing、Pile、Tail beat。配色：Blue、Black、Indigo。60 fps。
