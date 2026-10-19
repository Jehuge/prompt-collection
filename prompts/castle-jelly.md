# 城堡果冻 Castle Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · 浅水模拟 · SDF · 粒子烟花
- **标签**：`webgpu` `浅水模拟` `果冻` `瀑布` `烟花` `昼夜循环` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2108649845405929924) · [提示词帖](https://x.com/vib3coded/status/2108649989098594707) · 2026-10-10（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。提示词里提到的「Pirate Jelly / Island Jelly」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建一个名为 "Castle Jelly"（城堡果冻）的单文件 WebGPU "material study" 页面，延续我的果冻微缩场景系列（Pirate Jelly / Island Jelly）的风格：纸质摄影棚中桌上的一块会晃动的方形果冻湖，切面露出糖果地层，斜体衬线刊头 "Castle / Jelly."，右侧玻璃控制面板，左下 "How to play" 一行，界面为英文，移动端用底部抽屉布局。

### 微缩场景

悬崖上的一座童话城堡。块的左后方是一个高台，其正面是一堵陡峭的糖果条纹岩壁（层层蛋糕般的地层，与块的切面相匹配，湖下方有一片岩屑堆），用 SDF + surface nets 生成网格，朝上的面长着苔藓。草坪上：一座奶油色城堡，有圆塔、光亮的粉/淡紫/蓝色锥形屋顶、金色尖顶饰、飘动的三角旗、带垛口的城墙、大厅、拱形窗（白天是深色玻璃，夜晚透出灯光）、带吊桥的门楼、门边的火盆、软糖松树、开花灌木、芦苇。一条河从泉眼涌出，流过城门、穿过吊桥下方，从崖边倾泻而下，形成一道弧形瀑布落进果冻湖——并且在果冻内部继续流动：一道散开的水羽流，气泡先被压下去再升起，明亮的水流丝线沿湖底流淌。瀑布拍击水面（浅水波、泡沫、飞沫、水雾）。一艘小小的皇家大帆船（蓝色船体、白帆、王冠旗）绕湖航行。

### 交互

- Fireworks（烟花：从塔楼发射火箭，彩色爆炸照亮城堡和湖面；夜间自动燃放）
- Lower/Raise bridge（放下/升起吊桥）
- Royal salute（皇家礼炮：船开炮，溅起水花）
- Wishing coins（许愿硬币：投进瀑布下方的水潭）
- 点击塔楼 / 城门 / 火盆 / 船；拖动水面造浪，倾斜块，扔硬币和球，弯曲松树。

滑块：Firmness、Waterfall（流量）、Wave damping、Time of day（正午 → 日落 → 带星星的夜晚）。口味：Glacier（冰川）、Rose（玫瑰）、Lilac（淡紫）。阴影、焦散、透过果冻的折射、固定步长物理。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file WebGPU "material study" page called "Castle Jelly", in the style of my jelly diorama series (Pirate Jelly / Island Jelly): a square block of wobbly jelly lake on a table in a paper studio, cut faces showing candy strata, italic serif masthead "Castle / Jelly.", glass control panel on the right, "How to play" line at the bottom-left, UI in English, mobile bottom-sheet layout.
The diorama: a fairy-tale castle on a cliff. The back-left of the block is a plateau whose front is a sheer wall of candy-striped rock (layer-cake strata that match the block's cut faces, a talus under the lake), meshed from an SDF with surface nets, mossy where it faces up. On the lawn: a cream castle with round towers, glossy pink/lilac/blue cone roofs, gold finials, fluttering pennants, crenellated walls, a great hall, arched windows (dark glass by day, lamplight at night), a gatehouse with a drawbridge, a brazier by the gate, gummy pines, flowering bushes, reeds. A river wells up from a spring, runs past the gate under the drawbridge and pours off the lip as a waterfall that arcs down into the jelly lake — and keeps going inside the jelly: a fraying plume, bubbles driven down then rising, bright threads of current streaming along the lake floor. The falls pound the surface (shallow-water waves, foam, spray, mist). A little royal galleon (blue hull, white sails, crown standard) sails laps of the lake.
Interactions: Fireworks (rockets off the towers, coloured bursts that light the castle and the lake; automatic at night), Lower/Raise bridge, Royal salute (ship fires, splash), Wishing coins (into the pool under the falls); tap a tower / the gate / the brazier / the ship, drag the water to make waves, tip the block, throw coins and balls, bend the pines. Sliders: Firmness, Waterfall (flow), Wave damping, Time of day (noon → sunset → night with stars). Flavours: Glacier, Rose, Lilac. Shadows, caustics, refraction through the jelly, fixed-step physics.
```

</details>
