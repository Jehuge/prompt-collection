# 船闸果冻 Lock Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 多水体浅水模拟 · 角色动画
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `运河船闸` `自动编排` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110329593441796383) · [提示词帖](https://x.com/vib3coded/status/2110329833653772346) · 2026-10-14（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![船闸果冻 Lock Jelly](../assets/lock-jelly.jpg)

## 提示词（英文原文）

```text
Build "Lock Jelly." — a single self-contained HTML file (WebGPU + WGSL, no libraries, no network, works from file://), part of a "Material Studies" series of jelly dioramas. If WebGPU is missing or the adapter fails, show a clean fallback card instead of the scene.

CONCEPT
A square block of clear coloured jelly (about 5.2 × 5.2 units, ~2 units high) holding a little English canal scene. The canal runs along the FRONT edge of the block, so the block's front face cuts the water lengthways: you see the lock chamber in cross-section, the water inside it rising and falling between the gates, fish swimming, the boat's hull below the waterline. All cut faces show candy-coloured soil strata; under the pounds a blue-grey puddle-clay lining, under the chamber a brick invert on a concrete bed, under the fields brown earth and turf.

LAYOUT (left to right along the front)
- Upper pound on the left at the higher level, opening into a round winding hole (a bay for turning boats); near the lock it narrows between brick wing walls.
- The lock chamber in the middle: brick walls with dressed-stone quoins and coping, a slimy band between the two water levels and weed below, an iron ladder, a gauge board, a stone cill under the top gate, recesses that the open gates fold into.
- Below the bottom gate a short walled tail, then the lower pound bends away from the front face, runs under a humpback brick bridge into a basin with a willow-covered island, lily pads in its corners and a sunken bicycle on the bed.
- The ground steps down from an upper terrace to a lower one along a grassy bank.
- Behind the lock: stone setts around the chamber, bollards, a gravel towpath, a lane, the keeper's whitewashed cottage with a slate roof, green door, picket-fence garden full of flowers and washing flapping on a line, a gas lamp, a bench, a white windmill with turning lattice sails, oaks, willows, poplars, a hedge, sheep, reeds on the soft banks.

WATER
- Linear shallow-water waves on a staggered grid (~168²) with a little surface tension, so short ripples are springy like jelly; damping and firmness are adjustable.
- Three separate bodies of water — upper pound, chamber, lower pound — each with its own rest level. Faces between bodies stay shut unless the gate between them is open and the levels are equal. The chamber's level is moved bodily when paddles are drawn (Torricelli-style flow), with boils, white water and a dimple at the intake.
- Rendering: refraction of the scene behind, flavour-coloured absorption, sun caustics on the bed, soft light shafts, foam (wakes, paddle churn), a meniscus line on the cut faces. Split the surface mesh along the gate lines so the step in level at a shut gate is a clean wall hidden by the gate leaf, not a ramp.
- The block itself can be tipped by dragging its side; the jelly shears and wobbles, the water sloshes, and it settles back.

THE LOCK AND THE KEEPER
- Two single-leaf timber gates (planks, rails, diagonal brace, iron straps, a walkway with a handrail), each with a white balance beam with black bands. Ground-paddle pedestals with toothed racks that rise when wound.
- An articulated lock keeper (flat cap, navy jumper, cords, windlass in hand; torso, arms, thighs and shins as separate parts). He walks with a proper gait, plans his route around the bench, pedestals, bollards and any beam lying across his way (going round the beam's end), leans his back on a beam and walks it round backwards to swing a gate, winds the windlass with his arm circling the spindle, and sits on his bench between jobs. He sets off for the gate as the boat comes in.
- The cycle: the boat lies in the full chamber → keeper shuts the top gate → winds up the bottom paddles → the chamber empties into the tail with white water → winds them down → opens the bottom gate → the boat leaves, runs the tail, swings round the bend, ducks under the bridge, goes round the island and comes back into the chamber bow first → shut bottom gate → round to the top paddles → chamber fills with boils → open the top gate → the boat goes up the pound, turns in the winding hole and comes back. Repeat forever. A gate may only open when the levels match.

BOATS
- A traditional narrowboat "Wobble": black lofted hull, a green cabin with red lining-out, brass portholes, a cratch board and cover at the bow, a chimney with brass bands (puffing smoke), a painted Buckby can, plank and pole on the roof, rope fenders, a headlamp, a brass swan-neck tiller and a steerer in a red jumper. It follows smooth filleted routes (check the stern never swings out through the block's face), slows near the gates, heaves, pitches and rolls on the local surface, and hands its displaced volume back to the water so it makes bow waves and wakes.
- Three moored narrowboats in the basin in different liveries with flowerpots on the roofs and one ginger cat, tied to bank pins with stretchy mooring lines.

LIFE
- Roach, perch and bream as boids that stay in their own body of water (they can only move between pound and chamber while a gate is open), under the surface and hulls, off the bed, scattering from the boat and splashes.
- Mallards (drakes, ducks) and a duck with four ducklings that follow exactly along her trail; a pair of mute swans in the basin. They paddle the surface, ride the chamber down and up, upend now and then, get out of the boat's way and come for bread.
- A grey heron that wades in the shallows or stands on a moored boat's roof, stabs at fish (sometimes catching one), and flaps off somewhere quieter when the boat passes or someone toots.
- Chimney smoke from the boat and the cottage.

UI (editorial, like a print magazine)
- Top-left: small caps eyebrow "MATERIAL STUDIES", a huge italic serif title "Lock / Jelly.", a short subtitle. Top-right: a status pill "WebGPU · Live / Paused / Unavailable".
- Right: a frosted-glass control panel (a bottom sheet on mobile) with: buttons Hurry (speeds the keeper, paddles and boat), Toot (horn; also Space), Throw bread, Rubber duck (drops a yellow rubber duck that floats upright, can be picked up and thrown, rides the lock, is stopped by gates and shoved by boats); a liveliness meter; tallies Trips · Lockfuls · Fed; a status line "Wobble — Emptying the lock 62%" telling the story step by step; three flavours Greengage, Elderflower, Blackcurrant (change the water colour/absorption and strata); sliders Firmness, Wave damping, Paddle speed; Reset, Pause, Sound on/off, View.
- Bottom-left: "How to play — Throw bread. Toot the horn. Hurry the keeper." with a small line of instructions.
- Interaction: drag across the water to make waves, drag the block's side to tip it, pick up and throw rubber ducks, drag empty space to orbit, scroll/pinch to zoom; touch works.
- Soft studio lighting on a warm paper backdrop with the block's tinted, caustic-flecked shadow; WebAudio sounds: the boat's horn, the gate thudding shut, a creak, the windlass ratchet, and the rush of water that swells with the flow.

QUALITY
Keep it smooth (fixed-step physics, cheap per frame), no console errors, no page scroll, works at phone width. Test it headlessly: a full round trip happens, levels go exactly from upper to lower and back, no gate opens across a step, the keeper never walks into the water or through obstacles, the boat never touches a gate leaf, and every button works.
```

---

## 提示词（中文）

构建 "Lock Jelly."（船闸果冻）——一个单文件自包含 HTML（WebGPU + WGSL，无第三方库，无网络请求，可从 file:// 运行），属于 "Material Studies" 果冻微缩场景系列。如果缺少 WebGPU 或 adapter 失败，显示一张干净的降级卡片来代替场景。

### 概念

一块透明的彩色方形果冻（约 5.2 × 5.2 单位，约 2 单位高），里面是一个英国小运河场景。运河沿块的**前**边延伸，所以块的正面纵向剖开水体：你能看到船闸闸室的横截面，闸门之间的水位升降，鱼在游，船体在水线以下的部分。所有切面都露出糖果色的土壤地层；河段下方是蓝灰色的捣实黏土（puddle clay）衬层，闸室下方是混凝土基床上的砖砌底拱，田地下方是棕色泥土和草皮。

### 布局（沿正面从左到右）

- 左侧是位于较高水位的上游河段，连通一个圆形的掉头池（winding hole，供船掉头的港湾）；靠近船闸处在砖砌翼墙之间收窄。
- 中间是船闸闸室：砖墙，配方整石的墙角石和压顶石，两个水位之间有一条滑腻的水痕带，再往下长着水草，一架铁梯，一块水位标尺，上闸门下方的石质门槛，以及打开的闸门折入的墙龛。
- 下闸门下方是一小段有墙的尾渠，然后下游河段从正面拐开，从一座驼峰砖桥下穿过，进入一个港池，池中有一座长满柳树的小岛，角落里有睡莲叶，水底躺着一辆沉没的自行车。
- 地面沿一道长草的堤岸从上层台地降到下层台地。
- 船闸后方：闸室周围铺着石块，系缆桩，砾石纤道，一条小路，闸管员的白墙石板顶小屋，绿色的门，尖桩篱笆围起的花园开满鲜花，晾衣绳上衣服在飘，一盏煤气灯，一张长椅，一座带旋转格栅风帆的白色风车，橡树、柳树、杨树，一道树篱，羊，柔软河岸上的芦苇。

### 水

- 交错网格（约 168²）上的线性浅水波，带一点表面张力，让短涟漪像果冻一样有弹性；阻尼和硬度可调。
- 三个独立水体——上游河段、闸室、下游河段——各有自己的静止水位。水体之间的界面保持封闭，除非两者之间的闸门打开且水位相等。拉起闸门放水阀（paddles）时，闸室水位整体移动（Torricelli 式出流），伴有翻涌、白水和进水口处的漩涡凹陷。
- 渲染：折射后方场景，按口味着色的吸收，水底的阳光焦散，柔和的光柱，泡沫（尾迹、放水阀翻腾），切面上的弯月面线。沿闸门线切分水面网格，使闭合闸门处的水位落差是一道被闸门门叶遮住的干净竖墙，而不是一个斜坡。
- 拖动侧面可以让块本身倾斜；果冻剪切并晃动，水晃荡，然后恢复平静。

### 船闸与闸管员

- 两扇单叶木闸门（木板、横档、斜撑、铁箍，带扶手的走道），每扇配一根带黑色色带的白色平衡梁。地面放水阀底座带齿条，绞动时升起。
- 一个分节的闸管员（平顶帽、海军蓝毛衣、灯芯绒裤、手持绞柄 windlass；躯干、手臂、大腿和小腿是独立部件）。他以正确的步态行走，规划绕开长椅、底座、系缆桩以及横在路上的平衡梁的路线（绕过梁的末端），用后背靠住平衡梁、倒退着推它转动来开关闸门，手臂绕着转轴画圈来绞动绞柄，在两项工作之间坐在长椅上。船进来时他就动身走向闸门。
- 循环：船停在满水的闸室中 → 闸管员关上上闸门 → 绞起下游放水阀 → 闸室向尾渠泄水，翻起白水 → 把放水阀绞下 → 打开下闸门 → 船驶出，穿过尾渠，绕过弯道，从桥下钻过，绕岛一圈，再船头朝前回到闸室 → 关下闸门 → 绕到上游放水阀 → 闸室在翻涌中注满 → 打开上闸门 → 船驶上上游河段，在掉头池掉头再回来。无限循环。只有水位相等时闸门才能打开。

### 船

- 一艘传统窄船（narrowboat）"Wobble"：黑色放样船体，绿色船舱配红色描边，黄铜舷窗，船首的 cratch 挡板和罩布，带黄铜箍的烟囱（冒烟），一个彩绘的 Buckby 水罐，船顶上的跳板和撑篙，绳编护舷，一盏前灯，黄铜天鹅颈舵柄，以及一个穿红毛衣的掌舵人。它沿平滑倒圆的路线航行（检查船尾永远不会甩出块的正面），靠近闸门时减速，根据局部水面起伏、俯仰和横滚，并把排开的体积还给水，所以会产生船首波和尾迹。
- 港池里系着三艘涂装各异的窄船，船顶放着花盆，还有一只橘猫，用有弹性的系泊缆系在岸边桩上。

### 生命

- 拟鲤（roach）、河鲈（perch）和欧鳊（bream）作为 boids，留在各自的水体中（只有闸门打开时才能在河段与闸室之间移动），待在水面和船体下方、不碰底，遇到船和水花会散开。
- 绿头鸭（公鸭、母鸭），以及一只带着四只小鸭的母鸭，小鸭严格沿着她的轨迹跟随；港池里有一对疣鼻天鹅。它们在水面划水，随闸室水位一起下降和上升，时不时倒立觅食，给船让路，有面包时会游过来。
- 一只苍鹭在浅水中涉水，或站在系泊船的船顶上，啄鱼（有时能抓到一条），船经过或有人鸣笛时会飞去更安静的地方。
- 船和小屋的烟囱冒烟。

### UI（编辑风格，像印刷杂志）

- 左上：小型大写眉标 "MATERIAL STUDIES"，巨大的斜体衬线标题 "Lock / Jelly."，一行短副标题。右上：状态胶囊 "WebGPU · Live / Paused / Unavailable"。
- 右侧：磨砂玻璃控制面板（移动端为底部抽屉），包括：按钮 Hurry（加快闸管员、放水阀和船的速度）、Toot（鸣笛；也可按空格）、Throw bread（扔面包）、Rubber duck（投下一只直立漂浮的黄色橡皮鸭，可以捡起来扔，会随船闸升降，会被闸门挡住、被船推开）；一个活跃度仪表；计数 Trips · Lockfuls · Fed（航次 · 过闸次数 · 喂食）；一行状态 "Wobble — Emptying the lock 62%"，一步步讲述过程；三种口味 Greengage（青梅）、Elderflower（接骨木花）、Blackcurrant（黑加仑）（改变水色/吸收和地层）；滑块 Firmness、Wave damping、Paddle speed（放水阀速度）；Reset、Pause、Sound on/off、View。
- 左下："How to play — Throw bread. Toot the horn. Hurry the keeper." 加一行小字说明。
- 交互：在水面拖动造浪，拖动块的侧面使其倾斜，捡起并扔橡皮鸭，拖动空白处环绕视角，滚轮/双指缩放；支持触摸。
- 暖色纸张背景上的柔和摄影棚灯光，块投下带色调、带焦散斑点的阴影；WebAudio 音效：船笛、闸门砰地关上、吱呀声、绞柄棘轮声，以及随流量增强的水流声。

### 质量

保持流畅（固定步长物理，每帧开销低），无控制台报错，页面不滚动，在手机宽度下可用。无头测试：完成一整个往返；水位精确地从上游降到下游再回升；没有闸门在有水位落差时打开；闸管员永远不会走进水里或穿过障碍物；船永远不会碰到闸门门叶；每个按钮都可用。
