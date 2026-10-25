# 喷泉果冻 Geyser Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `间歇泉` `火山` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2112554053175554078) · [提示词帖](https://x.com/vib3coded/status/2112554223220953456) · 2026-10-20（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![喷泉果冻 Geyser Jelly](../assets/geyser-jelly.jpg)

## 提示词（英文原文）

```text
Build "Geyser Jelly" — a single-file interactive WebGPU diorama for a "Material Studies" series: a volcanic Icelandic island set inside a translucent block of jelly sea, viewed as a tabletop object on a pale paper studio backdrop.

TECH
- One self-contained HTML file: plain JS + WGSL, no libraries, no network requests (Google Fonts optional). WebGPU only, with a clean fallback screen if WebGPU/adapter is missing or the device is lost.
- Block 5.2 × 5.2 units, sea level at y = 1.0. The block can be tipped by dragging its ground/sides; it springs back and quivers like jelly (shear + squash wobble applied to everything inside in the vertex shader).
- Sea = linear shallow-water sim on a ~168² grid (heights + face velocities, a little surface tension, damping), fed by the block's tilt. Render the water with refraction of the scene behind, colored absorption through the jelly, light shafts, caustics on the bed, foam/white water, a bright meniscus on the cut faces. Cut faces of the ground show candy-coloured strata, basalt, tephra bands and turf.
- Sun shadow map, MSAA, HDR with a soft shoulder tone map. Fixed-step simulation (240 Hz bodies, 120 Hz water). Expose a debug handle on window for tests.

THE ISLAND (procedural height field + ground cover: moss, grass, sinter, scoria)
- Back-left: a scoria cone volcano with a real crater bowl holding a lava lake (dark crust plates with glowing seams), patchy summit snow. A lava channel runs from a flank vent with a spatter cone down into the sea, glowing ribbon with drifting crust; it keeps glowing under the jelly water; constant steam where it meets the sea. Warm lava light on nearby ground.
- Back-right: a grassy plateau that ends in sheer columnar-basalt cliffs on its seaward side, three basalt sea stacks with grassy tops, puffins on the ledges, a small square orange lighthouse.
- Middle: a geothermal valley — a pale sinter mound with orange bacterial runoff streaks, the geyser pool (blue over a dark vent), two milky-turquoise hot springs and one clear deep-blue one, a grey bubbling mud pot with expanding rings, fumarole steam. A timber boardwalk arcs round the front of the geyser with tourists on it, with paths to the jetty, the church and the lagoon.
- Front-left: a milky blue lagoon in white silica banks, a timber deck with a ladder, a black-timber bathhouse with a turf roof, bathers drifting up to their shoulders.
- Front-right: a meadow with three turf houses (grass roofs; white, red and tarred gables), a little white church with a red roof and spire inside a turf wall, a flagpole with a fluttering Icelandic flag, a fenced paddock with five Icelandic horses (chestnut with flaxen mane, black, grey, palomino, bay).
- A jetty on piles out to a T-head where a whale-watching boat berths; a small ticket hut. Black-sand beaches, lava boulders, kelp, urchins and sea stars on the sea floor.

THE GEYSER (Strokkur)
Cycle every ~15–20 s on its own: refill → rest (simmering, occasional bulges) → surge (three growing heaves, gurgling, wisps of steam) → a turquoise dome swells and quivers → it bursts: a white churning water column (20–35 m in the UI; 1 unit = 20 m) shoots up ballistically, hundreds of streaked drops rain back down and drift with the wind, the column breaks apart from the bottom up, a big steam cloud rolls off downwind, the sinter goes dark and wet, then the pool drains with a gurgle. Tourists raise their arms and cheer; some hold up phones during the surge.

THE VOLCANO
Tremor: the block shakes, ash billows from the crater, lava bombs fly (thud and smoke on land, hiss, steam and a splash at sea, glowing then cooling), the lava lake rises and brightens, the flow speeds up, horses bolt round the paddock, puffins take off, and the geyser goes off.

LIFE
- Humpback whale (knobbly head, long white flippers, grooved pale throat, broad flukes): cruises offshore, surfaces and blows 2–3 times (spray plumes), arches and shows its flukes as it dives, stays deep, avoids the boat and shallow water. About once a minute (or on demand) it breaches: sounds deep, turns to an open spot, rushes up, leaps clear while twisting, crashes onto its back with a huge splash, foam and a ring wave across the bay that rocks the boat.
- The boat "Hafdís" (old oak fishing boat: dark blue hull, red bottom, white wheelhouse, passengers in bright jackets): lies at the jetty ~40 s, then casts off and does a loop round the bay on a smooth filleted route, slowing right down when the whale is near, rides the waves with heave/pitch/roll, makes a wake, puffs exhaust, comes back alongside.
- Atlantic puffins: stand on the cliff edge and stacks, stretch their wings, whirr out over the bay, land on the water, dive and chase fish underwater, fly home and land.
- People: 9 tourists on the boardwalk (sometimes shuffle to another spot), walkers on the paths and jetty, 6 bathers in the lagoon. Horses graze, wander, trot when startled. A school of fish in the bay flees threats.
- Steam, ash and spray are soft translucent puffs drawn after the water with premultiplied alpha, broken up with noise, rising, spreading and drifting downwind.

UI
- Left: eyebrow "MATERIAL STUDIES", big italic serif title "Geyser / Jelly.", subtitle "A volcanic island with a geyser, set in a block of jelly sea." Bottom-left: "How to play" with the line "Set off the geyser. Shake the volcano. Watch for the whale." and a small paragraph of hints. Top-right: status pill "WebGPU · Live".
- Right glass panel: buttons Erupt / Tremor / Breach / Cast off (→ Full ahead); disabled with labels like "Surging…", "Erupting…", "Draining…", "Refilling…" when not ready. A thin liveliness meter. Tallies: Eruptions, Tallest (m), Breaches. Status lines "Strokkur: Resting 5 s / Surging / Erupting · 24 m / Draining / Refilling 68%" and "Hafdís: Alongside 18 s / Casting off / Under way 40% / Whale ahead / Coming alongside".
- Flavours: Blue lagoon (milky aqua), Lingonberry (red), Licorice (smoky dark). Sliders: Firmness, Wave damping, Wind. Buttons: Reset, Pause, Sound on/off, View.
- Interaction: tap the geyser, the volcano, the whale or the boat to trigger them (hand cursor on hover); Space sounds the boat's horn and puts the puffins up; drag across the water to make waves; drag the ground or the block's side to tip it; drag empty space or right-drag to orbit; wheel/pinch to zoom. On phones the panel becomes a bottom sheet with a "Controls" bar; no page scroll at any size.
- Sound: synthesized with Web Audio, only for events — surge bubbling, dome thump, eruption roar and spray hiss, drain gurgle, tremor rumble with rattles, bomb thuds and hisses, whale blow, breach rush and splash, boat horn, puffin and mud plops. No background ambience.

QUALITY BAR
Charming, legible miniature scale; nothing sticks through the water surface by mistake; no NaNs under stress (repeated tremors, eruptions, breaches, shaking, stirring). Verify with headless screenshots and an end-to-end browser test of every control, the geyser cycle order, the boat round trip, the breach, taps, flavours, sliders, pause, camera, mobile sheet and fallbacks — with zero console errors.
```

---

## 提示词（中文）

构建 "Geyser Jelly"（喷泉果冻）—— "Material Studies" 系列的一个单文件交互式 WebGPU 微缩场景：一座冰岛的火山岛，放在一块半透明的果冻海里，当作摆在浅色纸质摄影棚背景上的桌面物件来看。

### 技术

- 一个自包含的 HTML 文件：纯 JS 加 WGSL，不用库，也不发网络请求（Google Fonts 可选）。只用 WebGPU。如果没有 WebGPU、没有适配器，或者设备丢失，显示一块干净的降级画面。
- 块是 5.2 × 5.2 单位，海平面在 y = 1.0。拖动地面或侧面可以把块扳斜。它会弹回来，并且像果冻一样抖（剪切加上压扁的晃动，在顶点着色器里作用到里面的一切）。
- 海是大约 168² 网格上的线性浅水模拟（高度，加上网格面上的速度，一点点表面张力，还有阻尼），由块的倾斜喂进去。画水的时候折射后面的场景，果冻里有带颜色的吸收、光柱、海底焦散、泡沫和白水，切面上有一条亮的弯月面。地面的切面露出糖果色的地层、玄武岩、火山碎屑条带和草皮。
- 太阳阴影贴图，MSAA，HDR，色调映射带一个柔和的肩部。模拟用固定步长（刚体 240 Hz，水 120 Hz）。在 window 上暴露一个调试句柄，给测试用。

### 岛屿

程序化高度场，加上地面覆盖：苔藓、草、硅华、火山渣。

- 左后方：一座火山渣锥。火山口是真的一个碗，里面是熔岩湖（深色的结壳板块，接缝在发光）。山顶有一块一块的雪。一条熔岩通道从侧翼的喷口流下来，喷口旁边有一座溅射锥，然后流入海里。那是一条发光的带子，上面漂着结壳；到了果冻水面以下还在发光；碰到海的地方一直冒蒸汽。附近的地面被熔岩照暖。
- 右后方：一片草地高原，朝海的一侧是陡直的柱状玄武岩悬崖。三座玄武岩海蚀柱，顶上长着草。岩架上有海鹦。一座小的、方形的橙色灯塔。
- 中间：一条地热谷。一座浅色硅华丘，上面有橙色的细菌径流条纹。间歇泉池是蓝色的，下面是深色喷口。两处乳白、偏绿松石的温泉，一处清澈的深蓝色温泉。一口灰色的冒泡泥锅，涟漪一圈圈向外扩。喷气孔在冒蒸汽。一条木栈道从间歇泉前方绕过去，上面有游客。小路通向码头、教堂和泻湖。
- 左前方：一座乳蓝色泻湖，堤岸是白色硅华。一座木平台，带一架梯子。一座黑木浴场，屋顶是草皮。沐浴的人浸到肩膀。
- 右前方：一片草地。三座草皮屋（草屋顶；山墙分别是白的、红的和涂了焦油的）。一座小白教堂，红屋顶，有尖塔，围在一圈草皮墙里。一根旗杆，冰岛国旗在飘。一块围起来的马场，里面五匹冰岛马（栗色配亚麻色鬃、黑色、灰色、帕洛米诺、骝色）。
- 一座打在桩上的栈桥，伸到一座 T 形趸头，观鲸船停在那里。一座小售票亭。黑沙滩、熔岩石、海带，海底有海胆和海星。

### 间歇泉（Strokkur）

大约每 15–20 秒自己循环一次：回填 → 静息（微微沸着，偶尔鼓起一个包）→ 涌起（三次越来越大的抬升，咕噜声，几缕蒸汽）→ 一个绿松石色的穹顶膨胀、发抖 → 爆开。一道白色、翻腾的水柱射上去（界面上是 20–35 m；1 单位 = 20 m），走的是弹道。几百颗被拉成条的水滴落回来，并随风飘。水柱从下往上碎开。一大团蒸汽顺风滚走。硅华变得又暗又湿。然后水池咕噜一声排空。游客举起手臂欢呼；涌起的时候，有人把手机举起来。

### 火山

Tremor（颤动）：整块在震。火山口涌出火山灰。熔岩弹飞出去（落在地上是闷响和烟；落在海里是嘶的一声、蒸汽和一朵水花；先发着光，再冷却）。熔岩湖升高、变亮。熔岩流变快。马在马场里惊跑。海鹦起飞。间歇泉也跟着喷。

### 生命

- 座头鲸（头上满是结节，长长的白色鳍肢，浅色的喉腹有沟，尾叶很宽）：在近海巡游。浮上水面喷气 2–3 次（水雾柱），然后弓起背，下潜时把尾叶露出来，留在深处。它避开船，也避开浅水。大约每分钟一次（也可以手动触发），它会跃出水面：先下潜到深处，转向一片开阔的地方，向上冲，边扭转边整个跃出水面，再背部着水砸下来。巨大的水花、泡沫，以及一道环状波穿过海湾，把船摇起来。
- 船 "Hafdís"（老橡木渔船：深蓝色船体，红色船底，白色驾驶室，乘客穿着鲜艳的外套）：在码头停大约 40 秒，然后解缆，沿一条平滑、做了圆角的航线绕海湾一圈。鲸靠近的时候它会把速度降得很低。它随着浪做垂荡、纵摇和横摇，留下尾迹，喷出废气，再回来靠到码头边上。
- 大西洋海鹦：站在悬崖边和海蚀柱上，伸翅膀，嗡嗡地飞过海湾，落在水面上，潜下去追鱼，再飞回家并降落。
- 人：木栈道上 9 个游客（有时会挪到另一个位置），小路上和栈桥上有走路的人，泻湖里 6 个沐浴的人。马在吃草、闲逛，受惊时小跑。海湾里的一群鱼会躲开威胁。
- 蒸汽、火山灰和飞沫是柔和的半透明气团，画在水的后面，用预乘 alpha，再用噪声打散。它们上升、铺开，并顺风飘。

### 界面

- 左边：眉题 "MATERIAL STUDIES"，大号斜体衬线标题 "Geyser / Jelly."，副标题 "A volcanic island with a geyser, set in a block of jelly sea." 左下是 "How to play"，一行字是 "Set off the geyser. Shake the volcano. Watch for the whale."，再加一小段提示。右上是状态胶囊 "WebGPU · Live"。
- 右边一块玻璃面板。按钮：Erupt / Tremor / Breach / Cast off（之后变成 Full ahead）。还没准备好的时候按钮禁用，标签换成 "Surging…"、"Erupting…"、"Draining…"、"Refilling…" 这一类。一条细的活跃度计量。计数：Eruptions、Tallest (m)、Breaches。状态行是 "Strokkur: Resting 5 s / Surging / Erupting · 24 m / Draining / Refilling 68%" 和 "Hafdís: Alongside 18 s / Casting off / Under way 40% / Whale ahead / Coming alongside"。
- Flavours：Blue lagoon（乳白的水色）、Lingonberry（红）、Licorice（烟熏的深色）。滑块：Firmness、Wave damping、Wind。按钮：Reset、Pause、Sound on/off、View。
- 交互：点间歇泉、火山、鲸或者船来触发它们（悬停时是手形光标）。空格让船鸣笛，并让海鹦飞起来。在水面上拖动可以造浪。拖动地面或块的侧面可以扳斜它。拖空白处，或者按住右键拖，用来环绕。滚轮或双指用来缩放。手机上，面板变成底部抽屉，带一条 "Controls" 栏。任何尺寸下，页面本身都不要滚动。
- 声音用 Web Audio 合成，只给事件用：涌起时的冒泡、穹顶的闷响、喷发的轰鸣和飞沫的嘶声、排空的咕噜、颤动的隆隆加上嘎啦声、熔岩弹的闷响和嘶声、鲸的喷气、跃出时的冲势和水花、船的汽笛、海鹦入水的扑通，以及泥浆的扑通。没有背景环境音。

### 质量标准

微缩的尺度要可爱，也要看得清。不要有东西不小心穿出水面。加压的时候不要出现 NaN（反复颤动、喷发、跃出、摇晃、搅水）。用无头截图，以及一次端到端的浏览器测试，把每一项控制、间歇泉的循环顺序、船的往返、跃出、点击、口味、滑块、暂停、相机、手机抽屉和降级都走一遍——控制台零报错。
