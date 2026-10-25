# 海滩二号 Beach Two

- **类型**：交互网页 / 3D 海滩场景
- **技术栈**：WebGL / 单页网页玩具
- **标签**：`threejs` `webgl` `像素艺术` `沙滩排球` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2113299893158638078) · [提示词帖](https://x.com/vib3coded/status/2113300152677027929) · 2026-10-22（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![海滩二号 Beach Two](../assets/beach-two.jpg)

## 提示词（英文原文）

```text
Build a single-page web toy called "Beach Two": a real-time 3D scene rendered as pixel art — a beach volleyball court on a floating island with the sea in front. three.js r160 via import map (jsDelivr), English UI, original design only (no real brands).

RENDERING PIPELINE
- Orthographic camera at an isometric angle (≈31° down, azimuth π/4, rotatable in 90° steps with easing; drag sideways or buttons; wheel/pinch zoom 0.7–2.8). Fit the island outline plus palm tops into the screen area left free by the UI; snap the camera so the world origin lands on a whole art pixel.
- Render into a small half-float WebGLRenderTarget (nearest filtering, depth texture), ~480×300 art pixels at pixel size 3, no anti-aliasing.
- A mirrored reflection pass first (scene.scale.y = −1 about the water plane, hiding the sand, water and particles) into its own target; the water samples it in screen space.
- Post pass: texelFetch whole-pixel upscale, depth outlines (neighbour > 0.5 m nearer → darken ×0.5), nearest-of-~65 palette colours in OKLab (L weighted ×1.35), optional 4×4 Bayer dither, empty depth = page background. "Raw 3D" toggle shows the full-res MSAA render. Pixel size slider 2–6, palette/dither/outline checkboxes.
- Palette: foam whites and greys, sand from dry to wet, sea from shallow turquoise to deep blue, sky blues and night, sunset peach/coral/rose/violet, palm greens, team coral and teal, yellow/blue accents, skin and wood, lamp and fire yellows.

WORLD
- Island 33×26 m with rounded corners, cut like a cake: a sand heightfield grid pressed into the outline (dunes at the back, flat court, slope under the sea along a gently curving shoreline), coloured face by face with sand speckle and a wet band, smooth analytic normals. The cut side shows sand bands, and where the sea is a wall of water in depth layers; soil and rock below.
- Sea: a grid of waves updated every frame (rolling swells, chop, shoaling near shore), vertex colours by depth, foam where crests break in the shallows and along the swash line; shader mixes its own tinted colour with the mirrored beach (slight wobble) and adds sun/moon glints from facet normals. Buoys on a rope bob on the waves.
- Court 16×8 m with blue straps, net (alpha grid texture, white tapes, red-white antennae, padded posts, guy ropes).
- Palms with ringed curved trunks and drooping fronds swaying with the wind; dune grass; a boardwalk; a snack kiosk with striped awning, sign, lit hatch at night, surfboards, cooler and stools; benches; a beach shower; a lifeguard tower with a wind flag; striped umbrellas, towels, a deck chair, a sandcastle, a rowboat, a fire pit with logs; string lights on posts; two floodlights.
- Footprints and ball marks as instanced dents in the sand that fade back over time.

PEOPLE
- Box rigs (~18 boxes) posed every frame with two-bone IK: run on sand, ready stance, bump platform, setting window, spike (cock–whip–follow-through, airborne), serve with toss, block with arms up, sprawling dive, celebrate and high five, hold/throw the ball. Players have caps, glasses, buns.
- Beachgoers: one sunbathing on a towel, one in a deck chair, two standing who clap/cheer on points, a kid patting a sandcastle, two sitting by the fire. Gulls circle, flapping or gliding, casting shadows.

GAME (rally scoring to 15, win by 2, sets counted)
- Ball physics in substeps: gravity, quadratic air drag, wind with gusts, float-serve wobble; net crossing → tape dribble-over or drops into the net; posts; antennae fault; landing on sand with a puff and short roll; floating and drifting in the sea.
- AI: predict the ball's real flight; for the side it comes down on, pick who can reach the contact height in time (zones break ties); types pass/dig, set (or bump set), attack (or free ball), dive when slightly late; leave balls clearly going out; occasional "seam" where both leave the serve.
- Shot aiming by iterative simulation (lob to an apex, or a drive at a speed with bisection on launch angle plus drift correction), allowing for ~70% of the wind. Pass errors grow with incoming speed, wind and lateness; shanks on hard balls.
- Attack: run-up timed so the jump peaks at contact; candidate targets (line/cross deep, cut shots, pokes) scored by distance from the defender and block, with a taste for spiking; net-clearance check, small chances of long or net errors.
- Defence: one blocker jumps with the hitter in his lane (stuff, soft touch counting as first touch, or off the fingers), one deep defender shading away from the block.
- Serves: lobbed floats or hard flat serves; small error rates. Between rallies the nearest player fetches the ball (anywhere, even in the sea), lobs it to the server, who walks to the line.

UI
- Lit pixel-font scoreboard (CORAL vs TEAL, set number, status, serve dots, sets won). Rail: Time (Day/Sunset/Night), Wind (Calm/Breeze/Gusty + live m/s), Attack style (Auto/Spike/Shots), New match, Pause, View. Click the sand to call where the next attack goes (marker X). Light/dark themes; stacked layout on phones; "How it's drawn" panel.
```

---

## 提示词（中文）

构建一个叫做 "Beach Two"（海滩二号）的单页网页玩具：一个实时 3D 场景，渲染成像素画——浮岛上的一片沙滩排球场，前方是海。通过 import map 从 jsDelivr 引入 three.js r160。界面为英文。只用原创设计（不要真实品牌）。

### 渲染管线

- 正交相机，等距角度（向下约 31°，方位角 π/4，按 90° 一步步旋转并带缓动；可以横向拖动，也可以用按钮；滚轮或双指缩放，范围 0.7–2.8）。把岛屿轮廓连同棕榈树顶放进界面留出来的屏幕区域。吸附相机，让世界原点落在整颗艺术像素上。
- 渲染到一张较小的半精度浮点 WebGLRenderTarget（最近邻过滤，带深度纹理）。像素尺寸为 3 时大约是 480×300 艺术像素，不做抗锯齿。
- 先做一次镜像反射：绕水面把 scene.scale.y 设为 −1，藏起沙子、水和粒子，画进自己的渲染目标。水面在屏幕空间里采样它。
- 后处理：用 texelFetch 按整像素放大；深度轮廓（某个邻居比当前像素近超过 0.5 m → 变暗 ×0.5）；在 OKLab 里量化到大约 65 色调色板中最近的颜色（亮度 L 加权 ×1.35）；可选 4×4 Bayer 抖动；深度为空时用页面背景色。"Raw 3D" 开关显示全分辨率、带 MSAA 的渲染。像素尺寸滑块 2–6。调色板、抖动、轮廓各有一个复选框。
- 调色板：泡沫的白和灰；从干到湿的沙色；从浅青绿到深蓝的海；天空的蓝和夜色；日落的桃、珊瑚、玫瑰、紫罗兰；棕榈的绿；两队的珊瑚红和青绿；黄和蓝的点缀；皮肤和木头；灯和火的黄。

### 世界

- 岛是 33×26 m，圆角，像蛋糕一样被切开。沙的高度场网格压进这个轮廓（后面是沙丘，中间是平的球场，沿一条缓弯的海岸线斜插到海下）。逐面着色，带沙粒斑点和一条湿沙子。法线用平滑的解析法线。切开的侧面能看到一层层沙子；有海的地方是按深度分层的一堵水墙；下面是土和岩石。
- 海：每帧更新的波浪网格（滚动的涌浪、短碎浪、近岸浅化）。顶点颜色按深度来。浪峰在浅水破碎的地方，以及上冲带（swash line）上，形成泡沫。着色器把自己染过的颜色和镜像里的海滩混在一起（稍微晃一点），再按面法线加上太阳或月亮的闪光。一根绳子上的浮标随着浪上下。
- 球场 16×8 m，蓝色边带。球网：带 alpha 的网格纹理、白布带、红白相间的标志杆、包了护垫的网柱、拉线。
- 棕榈：树干弯曲，有一圈圈环纹，叶子下垂并随风摆。还有沙丘草、木栈道、一个小吃亭（条纹遮阳篷、招牌、夜里亮着的出餐口、冲浪板、冷藏箱和凳子）、长椅、沙滩淋浴、带风向旗的救生员塔、条纹遮阳伞、毛巾、一张躺椅、一座沙堡、一条划艇、一个堆着木头的火塘、柱子上的串灯，以及两盏泛光灯。
- 脚印和球印是沙子上的实例化凹坑，过一会儿会自己填回去。

### 人物

- 盒子骨骼，大约 18 个盒子。每一帧用双骨 IK 摆姿势：在沙上跑、准备姿势、垫球的平台、二传的击球窗口、扣球（引臂–鞭打–随挥，人在空中）、抛球发球、举手拦网、整个人扑出去的鱼跃、庆祝和击掌、拿球和扔球。球员有帽子、眼镜、丸子头。
- 海滩上的人：一个躺在毛巾上晒太阳，一个坐在躺椅里，两个站着的人在得分时鼓掌欢呼，一个小孩在拍沙堡，两个人坐在火边。海鸥盘旋，有时拍翅膀，有时滑翔，并且投下影子。

### 比赛（每球得分，打到 15 分，净胜 2 分，统计局数）

- 球的物理按子步算：重力、二次空气阻力、带阵风的风、飘球的晃动。过网时，要么沿网带滚到对面，要么掉进网里。还要处理网柱、触标志杆犯规、落在沙上溅起一小团并短短地滚一下，以及掉进海里之后漂着走。
- AI：预测球真正的飞行路线。球将落在哪一侧，就从那一侧里挑出谁能及时够到接触高度（分区用来打破平局）。动作类型有 pass/dig（传球 / 垫球）、set（二传，或者 bump set 垫传）、attack（进攻，或者 free ball 自由球）；稍微来不及时就 dive（鱼跃）。明显出界的球不要去接。偶尔出现一个 "seam"：发球时两个人都让开了。
- 击球落点用迭代模拟来瞄准（把球吊到一个最高点，或者按某个速度打平扣：对出手角度做二分，再修正漂移），大约算上 70% 的风。来球越快、风越大、人越晚到位，传球误差越大；硬球会垫飞。
- 进攻：助跑要卡时间，让起跳在触球的时候到达最高点。候选落点（直线深区、斜线深区、变线、点拨）按离防守者和拦网的距离打分，并且更想扣杀。要检查能不能过网。有很小的概率打出界，或者触网失误。
- 防守：一名拦网者跟着自己这条线上的扣球手起跳（盖死、轻轻碰到算第一下触球，或者从指尖弹出）。一名后排防守者站到拦网的另一侧。
- 发球：抛起来的飘球，或者平而快的大力发球，失误率很小。两个回合之间，离球最近的球员去把球捡回来（任何地方，包括海里），抛给发球的人，发球的人走到端线。

### 界面

- 亮着的像素字体记分牌（CORAL 对 TEAL，当前局、状态、发球圆点、各赢了几局）。侧栏：Time（Day / Sunset / Night）、Wind（Calm / Breeze / Gusty，外加实时的 m/s）、Attack style（Auto / Spike / Shots）、New match、Pause、View。点击沙子，指定下一次进攻打到哪里（标一个 X）。有浅色和深色主题。手机上改成上下堆叠。"How it's drawn" 面板说明画面是怎么画出来的。
