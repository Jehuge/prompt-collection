# 别墅果冻 Villa Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · 刚体浮力 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `微缩场景` `船只自动驾驶` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2107617244301664483) · [提示词帖](https://x.com/vib3coded/status/2107617476473164210) · 2026-10-07（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。提示词里提到的「Island Jelly」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "Villa Jelly"——一个单文件自包含 HTML（无外部请求、无第三方库），使用原生 WebGPU + WGSL，模拟用纯 JS 编写。它属于一个编辑风格的 "MATERIAL STUDIES" 交互式果冻微缩场景系列。场景：一块方形切开的果冻块，呈现一座热带小岛，后方是一栋现代白色别墅，一片松石绿泻湖环绕着前方的两条边，就像一个房地产微缩模型——但海是一块会晃动的果冻，透过切面能看到糖果条纹般的地层。必须流畅运行（模拟约 3 ms/帧）。

### 页面 / 布局（暖色纸张编辑风格）

- 纸色 #ece9e3，墨色 #241f1d，分隔线 #d5d0c8，强调色 #17a39b（松石绿）。衬线斜体标题字体（Iowan Old Style / Palatino / Georgia），无衬线 UI 字体，等宽数字。
- 左上：眉标 "MATERIAL STUDIES"，巨大的斜体 H1 "Villa / Jelly."，一条短分隔线，说明文字 "A white house, ten palms, a boat that never sits still and a sea that wobbles back."
- 右上状态胶囊：绿点 + "WEBGPU · LIVE"（另有 Paused / Unavailable 状态）。
- 右侧玻璃面板：
  - "THE SEA"：一排三个深色按钮——"Beach ball"（沙滩球）、"Rubber duck"（橡皮鸭）、"Starfish"（海星），每个从上方往泻湖里丢一个；一条细的强调色仪表显示海面有多活跃；计数 "Afloat · Sunk · Ashore"（漂浮 · 沉底 · 上岸）。
  - "FLAVOUR"：三个带光泽果冻球的色板——Turquoise（默认）、Curaçao（鲜艳蓝）、Raspberry（粉色）。
  - 滑块：Firmness（硬度）50、Wave damping（波浪阻尼）30、Tide（潮位）0（±10 cm）。
  - Reset · Pause · Reset view。
- 左下 "HOW TO PLAY"：斜体 "Stir the sea. Tip the block. Throw a duck." + 一行灰色小字："Drag across the water to make waves and watch the boat ride them · drag the side of the block to tip it and slosh the lagoon · grab the boat to steer it, let go and it carries on · pick up a ball, a duck or a starfish and throw it · drag a palm to bend it · drag empty space or right-drag to orbit · scroll or pinch to zoom"（在水面拖动造浪、看船乘浪；拖动块的侧面使其倾斜、让泻湖晃荡；抓住船来操控，松手后它继续航行；捡起球、鸭子或海星扔出去；拖动棕榈树使其弯曲；拖动空白处或右键拖动来环绕视角；滚轮或双指缩放）。
- 微缩场景居中放在标题区与面板之间的空白处。移动端：面板变为底部抽屉（"Controls" 栏，默认收起），触摸环绕、双指缩放、页面不滚动。缺少 WebGPU / adapter 时显示 "Villa Jelly." 降级卡片。控制台零报错。

### 微缩场景（块 5.2 × 5.2，海平面 1.3）

- 地形高度场：小岛占据地块后方约 60%；波浪状海岸线沿 +z 和 +x 两条边延伸（前方转角用 soft-max 做圆角），因此泻湖是沿着面向相机的两条边的 L 形（相机从前方转角看过去，az ≈0.74，el ≈0.5，FOV 34°）。
- 从海到内陆的剖面：泻湖底约 0.5 深，带沙纹 → 短的海滩斜坡 → 窄沙滩 → 陡峭的沙岸 → 抬高的草坪平台（+0.455）。草坪有割草机留下的条纹，略带光泽，像青柠果冻；浅色铺路石板构成露台、玻璃立面前的一条平台，以及通往台阶的小路。
- 块的切面：糖果地层（巧克力基岩、焦糖黏土、随口味变化的薄荷/蓝/粉色贝壳带、香草色沙层、海下的湿沙；草坪下方：深色土壤，顶部一条绿色草层），压入了卵石斑点。海的切面是半透明果冻墙，带明亮的弯月面（meniscus）线和柔和的转角线；透过它们能看到海床和地层。
- 别墅（白色、现代、方正）：石质基座；底层为通高的深色玻璃立面，被白色竖框分隔；车库侧翼配深色百叶门；楼板向前延伸成阳台，由四根细白柱支撑，配深色金属栏杆；上层有一条长玻璃带；左端一面白色翼墙；薄而外挑的白色屋顶板，带灰色内嵌，屋顶上一个小盒体。深色玻璃反射摄影棚柔光箱，后面是昏暗温暖的室内。
- 露台上方的凉棚：四根深色金属柱、横梁、一块会随微风"呼吸"的下垂米色帆布；L 形户外沙发配靠垫、矮桌、地毯。
- 白色台阶带侧墙，从草坪沿沙岸下到海滩，顶部两盏庭院灯。
- 海滩：白色遮阳伞（扇贝边，会飘动）、两张白色躺椅、带桨的红色皮划艇；海滩草丛；沙岸、海滩和泻湖底都有岩石。
- 茂密植被（重要——不要稀疏、光秃的树）：10 棵高大的椰子树，树干是环纹焦糖软糖质感（树根膨大，弯曲倾斜），每棵树冠有 16 片拱形羽状叶（每片 30 对小叶，V 形折叠，扫向叶尖，嫩叶直立，老叶下垂），另加 2 片下垂的干枯稻草色叶子；草坪边缘和房子周围有几十丛团块状软糖灌木，部分开着粉/红/白色花。

### 物理（与 "Island Jelly" 相同）

- 海：168² 交错网格上的线性浅水模拟，120 Hz，波速 √(g·depth)，使波浪在浅水区变慢变陡；加一个小的表面张力项，让果冻涟漪富有弹性；阻尼滑块；平均水位校正；潮位滑块改变水位和湿区范围。
- 块：拖动侧面使其倾斜（弹簧-阻尼，最大约 0.17 rad）；平面内重力让海水晃向低侧再平静下来；果冻顶面带惯性地剪切和压扁；块内的一切都在顶点着色器中随之晃动。
- 手指搅动：在水面上拖动会推动移动的凹陷，产生波浪。
- 漂浮物（块坐标系中的刚体球，240 Hz）：沿水面法线的浮力，朝水流方向的强果冻阻力，每帧把排开的体积还给海（它们会自己产生涟漪），入水时产生带气泡和泡沫的水花坑，果冻中悬浮着细小气泡。与地形、棕榈树干、别墅盒体、彼此以及船发生碰撞。
  - Beach ball（沙滩球）：r 0.085，非常轻，浮得很高，会弹跳、打水漂、滚动；六块彩色瓣片（红、蓝、黄）配白色顶盖，有光泽的乙烯基材质。
  - Rubber duck（橡皮鸭）：半浮在水中，总会自己扶正、头朝上（对齐水面或地面法线），黄色身体、橙色嘴、黑眼睛。
  - Starfish（海星）：缓慢下沉，在果冻中滑翔下降，平贴在海底；珊瑚色/粉色/紫色，带糖霜般的凸点。
  - 初始状态：一个球在海滩上，一个在草坪上，两只鸭子漂浮着，两只海星在泻湖底。
- 棕榈树：每个树冠一个二维弯曲弹簧，由微风、块倾斜和用户拖动驱动；顶点着色器弯曲树干（∝t²）并让叶尖飘动。

### 船（自主航行）

- 小型白色日间巡航艇（缩放后船体长约 0.62）：深 V 型放样船体，海军蓝船底和水线条纹，白色甲板，柚木驾驶舱地板，船尾长椅，驾驶座，带深色后倾挡风玻璃和侧窗的低矮船舱，细柱支撑的白色硬顶，双深色舷外机，不锈钢船首栏杆。
- 漂浮在模拟水面上：8 个船体采样点根据局部水面给出起伏/俯仰/横滚（自身造成的波谷做钳制，避免陷进去），随速度抬头，转弯时内倾；平面内：沿波浪坡被推动（有上限），被水流拖拽，前后阻力小、侧向阻力大（龙骨），碰到沙地有地形惩罚，撞到块壁会反弹。
- 自动驾驶：纯追踪（pure-pursuit）算法，沿 L 形泻湖绕一条闭合环形跑道航行（沿外侧航道出去，绕过转角，掉头，沿内侧航道回来），弯道减速，巡航速度约 0.78 u/s，永不搁浅。
- 航行时排开水 → 在波浪模拟中产生真实的尾迹，冲上海滩；另加一个泡沫场：船尾白色蕾丝状尾迹、两侧泡沫线和船首浪花，在几秒内消退。
- 用户可以抓住船首把它拖过水面；松手后它找到环线上最近的点继续航行。它会把漂浮的鸭子/球推开。

### 渲染

- 渲染通道：太阳阴影贴图（全部物体）、焦散（让网格透过波浪折射到底面，亮度取决于三角形面积变化）、带距离缓冲的不透明场景、海的背面，然后在场景副本上绘制果冻海：按路径长度做 Beer–Lambert 吸收（口味 sigma）、散射色调、折射、焦散光柱、菲涅尔摄影棚反射、阳光闪烁、拍打沙滩的岸线蕾丝泡沫、尾迹/水花泡沫场、边缘高光。块下方的地面得到带色调、带焦散斑点的阴影。
- 柔和的摄影棚灯光：纸张背景，左前方大柔光箱，后方冷色灯条；半球环境光；色调肩部压缩 + 抖动（dither）。
- 材质：哑光涂料和石材、深色反光玻璃、光泽胶衣/金属、半透明帆布、半透明软糖灌木和棕榈叶（背光辉光）、哑光带斑点的岩石。
- 口味切换水的 sigma/色调和地层颜色：Turquoise（sigma ≈ 2.1/0.36/0.5，色调 0.07/0.46/0.42）、Curaçao（2.7/1.05/0.26，色调 0.02/0.2/0.52）、Raspberry（0.34/2.2/1.25，色调 0.44/0.05/0.17）。

### QA（无头 Chromium + SwiftShader）

- 调试钩子 window.__vj（world、boat、bodies、water、block、advance、drop、pick、project、setPalette、reset、setPause、freeze 标志）。验证：6 个初始物体且计数为 2/2/2；别墅 + 10 棵棕榈树已构建；船在 14 秒内绕行 ≥6 单位且不搁浅，并留下泡沫和波浪；空闲稳定性；丢下的球浮得高、鸭子直立、海星平沉；计数 UI 一致；搅动产生的波浪会平息；倾斜块时海水堆向低侧并恢复；船可以被抓住、拖动并恢复航线；扔进海里的球会上下浮动，放在海滩上的鸭子直立；棕榈树会弯；口味、滑块、暂停、环绕、缩放正常；压力测试无 NaN；模拟 < 5 ms/帧；无网络请求；无控制台报错；页面不滚动；移动端抽屉 + 触摸；WebGPU 降级。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Villa Jelly" — a single self-contained HTML file (no external requests, no libraries) using native WebGPU + WGSL, simulation in plain JS. It belongs to an editorial "MATERIAL STUDIES" series of interactive jelly dioramas. Scene: a square cut-out block of jelly showing a tropical island with a modern white villa at the back and a turquoise lagoon wrapping the two front edges, like a miniature real-estate diorama — but the sea is a wobbling block of jelly with candy-striped strata visible through its cut faces. Must run smoothly (sim ≈3 ms/frame).

PAGE / LAYOUT (warm paper editorial)
- Paper #ece9e3, ink #241f1d, rules #d5d0c8, accent #17a39b (turquoise). Serif italic display (Iowan Old Style / Palatino / Georgia), sans UI, mono numbers.
- Top-left: eyebrow "MATERIAL STUDIES", huge italic H1 "Villa / Jelly.", short rule, caption "A white house, ten palms, a boat that never sits still and a sea that wobbles back."
- Top-right status pill: green dot + "WEBGPU · LIVE" (Paused / Unavailable states).
- Right glass panel:
  • "THE SEA": three dark buttons in a row — "Beach ball", "Rubber duck", "Starfish" (each drops one into the lagoon from above); thin accent meter showing how lively the sea is; tally "Afloat · Sunk · Ashore".
  • "FLAVOUR": three swatches with glossy jelly balls — Turquoise (default), Curaçao (vivid blue), Raspberry (pink).
  • Sliders: Firmness 50, Wave damping 30, Tide 0 (±10 cm).
  • Reset · Pause · Reset view.
- Bottom-left "HOW TO PLAY": italic "Stir the sea. Tip the block. Throw a duck." + small grey line: "Drag across the water to make waves and watch the boat ride them · drag the side of the block to tip it and slosh the lagoon · grab the boat to steer it, let go and it carries on · pick up a ball, a duck or a starfish and throw it · drag a palm to bend it · drag empty space or right-drag to orbit · scroll or pinch to zoom".
- Centre the diorama in the free space between masthead and panel. Mobile: panel becomes a bottom sheet ("Controls" bar, closed by default), touch orbit, pinch zoom, no page scroll. Fallback card "Villa Jelly." if WebGPU/adapter missing. Zero console errors.

THE DIORAMA (block 5.2 × 5.2, sea level 1.3)
- Terrain heightfield: the island fills the back ~60% of the tile; wavy shorelines run along the +z and +x edges (soft-max rounded front corner), so the lagoon is an L along the two edges facing the camera (camera from the front corner, az ≈0.74, el ≈0.5, FOV 34°).
- Profile from sea inland: lagoon floor ≈0.5 deep with sand ripples → short beach slope → narrow sandy beach → steep sandy bank → raised lawn plateau (+0.455). Lawn is striped by a mower, slightly glossy like lime jelly; pale paving slabs for a patio, a terrace strip in front of the glass and a path to the stairs.
- Cut faces of the block: candy strata (chocolate bedrock, caramel clay, a mint/blue/pink shell band depending on flavour, vanilla sand, wet sand under the sea; under the lawn: dark soil then a green grass band on top) with pressed-in pebble specks. The sea's cut faces are translucent jelly walls with a bright meniscus line and soft corner lines; you see the seabed and strata through them.
- Villa (white, modern, boxy): stone plinth; ground floor with a full-height dark glass front split by white mullions; garage wing with dark slatted door; floor slab that runs forward as a balcony on four slim white columns with a dark metal rail; upper floor with a long glass band; a white fin wall at the left end; thin overhanging white roof slab with grey inset, small roof box. Dark glass reflects the studio softbox with a dim warm room behind.
- Pergola over the patio: four dark metal posts, beams, a sagging beige canvas that breathes in the breeze; L-shaped outdoor sofa with cushions, low table, rug.
- White stairs with cheek walls from the lawn down the bank to the beach, two garden lamps at the top.
- Beach: white umbrella (scalloped, flutters), two white loungers, red kayak with paddle; beach grass tufts; rocks on the bank, beach and lagoon floor.
- LUSH vegetation (important — no sparse, bald trees): 10 tall coconut palms with ringed caramel-gummy trunks (swollen foot, curving lean) and full crowns of 16 arching pinnate fronds each (30 leaflet pairs, V-folded, swept to the tip, young fronds upright, old ones drooping) plus 2 dry straw-coloured hanging fronds; dozens of lumpy gummy bushes along the lawn edge and around the house, some with pink/red/white flowers.

PHYSICS (same as "Island Jelly")
- Sea: linear shallow-water sim on a 168² staggered grid at 120 Hz, wave speed √(g·depth) so waves slow and steepen over the shallows, small surface-tension term for springy jelly ripples, damping slider, mean-level correction, tide slider changes the level and the wet area.
- Block: drag its side to tip it (spring-damper, max ~0.17 rad); in-plane gravity makes the sea slosh to the low side and settle; the jelly top shears and squashes with inertia; everything inside is wobbled in the vertex shader.
- Finger stirring: dragging over the water pushes moving dents that make waves.
- Floating bodies (rigid spheres in block frame, 240 Hz): buoyancy along the surface normal, heavy jelly drag towards the flow, displaced volume handed back to the sea every frame (they make their own ripples), splash craters with bubbles and foam on entry, tiny air bubbles suspended in the jelly. Contacts with terrain, palm trunks, villa boxes, each other and the boat.
  • Beach ball: r 0.085, very light, floats high, bounces and skips, rolls; six coloured gores (red, blue, yellow) with white caps, glossy vinyl.
  • Rubber duck: floats half-in, always rights itself head-up (aligns to surface or ground normal), yellow body, orange beak, black eyes.
  • Starfish: sinks slowly, planes down through the jelly, settles flat against the floor; coral/pink/purple with sugared knobs.
  Start state: one ball on the beach, one on the lawn, two ducks afloat, two starfish on the lagoon floor.
- Palms: one 2D bend spring per crown driven by breeze, block tilt and user drag; vertex shader bends the trunk (∝t²) and flutters frond tips.

THE BOAT (runs by itself)
- Small white day cruiser (scaled hull ~0.62 long): deep-V lofted hull with navy bottom and boot stripe, white deck, teak cockpit sole, aft bench, helm seats, low cabin with dark raked windscreen and side windows, white hard-top on slim posts, twin dark outboards, stainless bow rail.
- Floats on the sim: 8 hull points give heave/pitch/roll from the local surface (own trough clamped so it can't sink into it), noses up with speed, leans into turns; in-plane: pushed (capped) down wave slopes, dragged by the flow, low drag fore-aft and high sideways (keel), terrain penalty if it touches sand, bounces off block walls.
- Autopilot: pure-pursuit around a closed racetrack loop following the L-shaped lagoon (out along the outer lane, round the corner, U-turn, back along the inner lane), slowing in bends, cruise ≈0.78 u/s, never grounds.
- It displaces water as it moves → a real wake in the wave sim that runs up the beach; plus a foam field: white lacy trail from the stern, side lines and bow spray, fading over a few seconds.
- User can grab and tow it by the bow across the water; released, it finds the nearest point of its loop and carries on. It shoves floating ducks/balls aside.

RENDERING
- Passes: sun shadow map (everything), caustics (refract a grid through the waves onto the floor, brightness by triangle area change), opaque scene with distance buffer, back-faces of the sea, then the jelly sea over a copy of the scene: Beer–Lambert absorption by path length (flavour sigma), scattered tint, refraction, caustic light shafts, Fresnel studio reflection, sun glints, shoreline lace foam that laps the sand, wake/splash foam field, rim highlights. The floor under the block gets a tinted, caustic-flecked shadow.
- Soft studio lighting: paper backdrop, big softbox front-left, cool strip behind; hemispherical ambient; tone shoulder + dither.
- Materials: matte painted render and stone, dark reflective glass, glossy gel-coat/metal, translucent canvas, gummy translucent shrubs and palm fronds (backlit glow), matte speckled rocks.
- Flavours swap water sigma/tint and strata colours: Turquoise (sigma ≈ 2.1/0.36/0.5, tint 0.07/0.46/0.42), Curaçao (2.7/1.05/0.26, tint 0.02/0.2/0.52), Raspberry (0.34/2.2/1.25, tint 0.44/0.05/0.17).

QA (headless Chromium + SwiftShader)
- Debug hook window.__vj (world, boat, bodies, water, block, advance, drop, pick, project, setPalette, reset, setPause, freeze flag). Verify: 6 starting bodies and tally 2/2/2; villa + 10 palms built; boat laps ≥6 units in 14 s without grounding and leaves foam + waves; idle stability; dropped ball floats high, duck upright, starfish sunk flat; tally UI matches; stirring makes waves that die down; tipping the block piles the sea on the low side and settles back; boat can be grabbed, towed and resumes its course; ball thrown into sea bobs, duck put on the beach sits upright; palms bend; flavours, sliders, pause, orbit, zoom; stress test with no NaN; sim < 5 ms/frame; no network requests; no console errors; no page scroll; mobile sheet + touch; WebGPU fallback.
```

</details>
