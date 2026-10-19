# 涨潮时的鸟居 Torii at High Tide

- **类型**：交互网页 / 3D 水体微缩场景
- **技术栈**：Three.js r160 · WebGL · SSR · GPU 波动方程
- **标签**：`threejs` `webgl` `水面模拟` `鸟居` `四季` `潮汐` `微缩场景` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110014604524896392) · [提示词帖](https://x.com/vib3coded/status/2110014758548078979) · 2026-10-13（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![涨潮时的鸟居 Torii at High Tide](../assets/torii-at-high-tide.jpg)

## 提示词（中文）

构建一个单文件交互式 WebGL 微缩场景（一个 index.html，无构建步骤），通过 import map 从 cdn.jsdelivr.net 加载 Three.js r160，并从 three/examples/jsm 引入 OrbitControls 和 BufferGeometryUtils（mergeVertices、mergeGeometries）。一切都是程序化的——不使用外部模型或纹理。

### 概念

"Torii at High Tide"（涨潮时的鸟居）：一座受严岛（Itsukushima）启发的日式神社微缩小岛，置于一个 10×10、边缘为圆角的透明水块中（竖直转角半径约 0.6，顶边半径约 0.26），放在一块薄薄的沙色底板上，背景是暖色和纸（washi）质感，地面有一道随距离淡出的柔和阴影（这样黄昏时的长阴影不会横穿整个页面）。

### 地形（高度场约 400×400，裁切到圆角水块内，沿边界有一圈"裙边"，使横截面透过水体可见）

- 在一个面向相机的局部坐标系中工作（u = 横向，v = 朝向观众）。
- 后方是一座森林覆盖的穹顶形山丘（约 2.4 高），山脚是一片低矮的沙质神社台地，前方是一片宽阔、缓缓倾斜的潮滩（从约 -0.06 降到约 -0.46），在前方和两侧下降到约 -1.0。
- 两个多岩石的花岗岩岬角环抱海湾，每个上面有 1–2 棵倾斜的盆景式松树（分段树干 + 扁平的树冠垫）。
- 山腰上一块整平的空地用来放五重塔。
- 地形着色器：陡坡上是花岗岩（带斑点，水线正上方一条更暗的湿带，水线下被藻类染暗），带湿线的沙子，满潮线以下更深的湿润潮间带沙，山上和台地上成片的苔藓/草，冬季朝上的表面有积雪，水下有程序化的动态焦散。CPU 按顶点烘焙地平线 AO，另加树冠遮挡带来的变暗。

### 建筑（全部合并为一个顶点着色网格 + 一个自发光 "glow" 网格；写一个小的 Builder，用颜色和变换添加盒体/圆柱/球体/自定义几何体，然后 mergeGeometries）

- 两部（Ryōbu）式鸟居，立在海湾中、位于神社的中轴线上（约 1.9 高）：朱红色带锥度的主柱配黑色柱脚护套，四根支撑用的袖柱（sode-bashira），带黑色柱帽，每根各有两道连接横梁；贯（nuki）横梁，中间的额束配深色匾额，岛木（shimaki），以及一根弯曲的笠木（kasagi，两端上翘的挤出形状），顶层为黑色。主柱必须止于岛木内部，不能从笠木中穿出来。
- 建在潮滩上方高脚柱上的神社：木板平台（带板缝条和深色边梁），下方是一排排延伸到海床的木柱；一座正殿和一座较小的前殿（白墙、朱红立柱和横梁，正面是障子风格的面板 = 细密深色格栅后面的发光面板），一座带朱红栏杆的较低前方舞台，以及两条建在高脚柱上、带屋顶的朱红回廊，先向两侧延伸再折回岸边。
- 屋顶：一个四坡屋顶生成器，带内凹的轮廓和上翘的檐角（顶面是深色桧皮棕，木质暖色底面，浅色封檐板饰边，黑色屋脊盖）。
- 山腰空地上的一座五重塔：石基座，白墙配朱红立柱，斗栱层，逐层缩小的外展屋顶，带相轮的青铜塔刹。
- 台地和舞台上的石灯笼（tōrō）：六角形底座、灯柱、带发光窗的火袋、小屋顶、宝珠。

### 植被

- 约 4–5k 个树冠团块（icosphere 的 InstancedMesh，带顶点噪声置换 + 片元凹凸），每棵树 2–4 个成簇，按实例根据邻近遮挡计算 AO，顶部更亮。
- 通过实例属性分四类：阔叶树、樱花、枫树、松树（扁平树冠垫）。樱花聚集在山的较低处，台地上还有 5 棵能看到树干的主景樱花树；松树占据山顶和岬角。
- 颜色来自每类的深/浅调色板 uniform，由 JS 按季节混合。

### 四季（循环 0..4 = 春、夏、秋、冬；由工具栏按钮触发动画过渡）

- 春：粉色樱花，飘落的花瓣。夏：郁郁葱葱的绿色，无粒子。秋：红枫，橙/黄色阔叶，飘落的枫叶。冬：落叶树团块变成近乎光秃的棕色并缩小约 38%，树冠顶部、屋顶、平台、岩石和地面有积雪；雪花落到水面上立即融化。

### 水（写实，不是果冻）

- 管线：不透明场景 → 带 DepthTexture 的 MSAA HalfFloat 目标；复制到第二个目标，然后用自定义 ShaderMaterial 绘制水面并做手动深度测试；然后是漂浮粒子；最后一个全屏通道做 ACES 色调映射、sRGB、轻微移轴。透明 canvas 叠在 CSS 背景上。
- 颜色来自真实厚度：重建每个水像素后方的深度，按 Beer–Lambert 吸收趋向由用户水色派生出的深散射色（潮滩上方浅，深处蓝；侧壁获得额外路径长度，因此呈现为水体）。
- 屏幕空间折射、菲涅尔天空反射、由精细动态细节法线产生的阳光闪烁。
- 屏幕空间反射（对深度缓冲做约 26 步光线步进，移动端更少），让鸟居、神社和点亮的灯笼倒映在水中。
- 涟漪：在 256×256 HalfFloat ping-pong 目标上做 GPU 波动方程，固定 60 Hz 步长，用陆地遮罩纹理让波浪在岸边反射。光标移动沿路径注入胶囊形水滴；点击产生水花。
- 岸边泡沫只出现在地形接近水面**且**坡度平缓的地方（悬崖、立柱或鸟居柱子周围不要有白色轮廓）；泡沫带宽度按坡度缩放；被噪声打碎。
- 潮汐：工具栏开关在满潮（0）和低潮（-0.55）之间做动画：水块边缘移动、侧面拉伸；低潮时整片潮滩露出，鸟居立在湿沙上。

### 粒子（花瓣 / 叶子 / 雪，约 700 个实例化四边形，CPU 模拟）

- 从樱花团块（春）、落叶树团块（秋）或天空（冬）生成；下落时飘舞；一阵阵的风从岛吹向海湾，让它们落到水面。
- 落地：落在水上时变成漂浮状态（顶点着色器用与水面相同的涟漪 + 波浪高度把它们抬起），缓慢漂移，被光标移动推开，被点击水花吹散，退潮时搁浅，涨潮时重新浮起；落在陆地上则静止并淡出。
- 形状在片元着色器中绘制：带缺口的花瓣、五裂枫叶、柔和的雪花圆盘。对场景深度做手动深度测试。

### 锦鲤

- 7 条锦鲤（车削身体 + 叉形扇尾 + 胸鳍，合并），InstancedMesh，在顶点着色器中做游动摆动，并按品种程序化生成花纹（红白 kohaku、大正三色 sanke、昭和三色 showa、黄金 ogon、纯橙色）。它们四处游荡，避开浅水和水块壁，逃离光标和水花。在水下渲染，因此会被折射和染色。

### 时间（滑块，以 11:00 到约 19:10 的时钟显示）

- 从正午到黄金时刻，太阳高度、颜色和强度、半球光颜色以及水面的天空反射随之变化；接近黄昏时障子面板和灯笼发光（自发光），三个暖色点光源照亮神社、舞台和鸟居。

### UI（编辑风格、极简、英文）

品牌标识 "shiosai°" 配一个小鸟居标志，标题 "A gate that / stands in the sea."，眉标 "Shrine and tide, in miniature"，竖排说明文字 "A study of tide and seasons"，地点标签 "Shrine Cove · 34°16′ N · 132°19′ E"，一个悬浮胶囊工具栏（reset、显示当前季节名的季节循环、High tide / Low tide 开关、Tune、全屏），页脚放提示和自适应 FPS + "Season · time" 读数，一个玻璃质感的设置面板（季节、时间、飘落花瓣；水色、潮位、波高、涟漪强度、清澈度、焦散；太阳方位角、移轴），以及一张 "How it's made" 卡片。朱红色强调色，通过 CSS token 实现亮色和暗色主题，响应式适配到 390 px（面板变为底部抽屉），遵守 prefers-reduced-motion，自适应像素比，并为触屏设备提供更轻量的模式。开场：水注满水块，同时相机缓缓推近。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file interactive WebGL diorama (one index.html, no build step) with Three.js r160 loaded via an import map from cdn.jsdelivr.net, plus OrbitControls and BufferGeometryUtils (mergeVertices, mergeGeometries) from three/examples/jsm. Everything is procedural — no external models or textures.

CONCEPT
"Torii at High Tide": a miniature Japanese shrine island inspired by Itsukushima, inside a 10×10 block of clear water with rounded edges (vertical corner radius ~0.6, top edge radius ~0.26), on a thin sand-colored base slab, on a warm washi-paper background with a soft floor shadow that fades out with distance (so long dusk shadows never streak across the page).

TERRAIN (heightfield ~400×400, clipped to the rounded block, with a boundary "skirt" so the cross-section shows through the water)
- Work in a local frame facing the camera (u = across, v = toward the viewer).
- A forested dome-shaped hill at the back (~2.4 high), a low sandy shrine terrace at its foot, then a wide, gently sloping tidal flat in front (from ~-0.06 down to ~-0.46), dropping to ~-1.0 at the front and sides.
- Two rocky granite headlands framing the bay, each with 1–2 leaning bonsai-style pines (segmented trunks + flattened canopy pads).
- A flattened clearing on the hill flank for the pagoda.
- Terrain shader: granite rock on steep slopes (speckled, darker wet band just above the waterline, algae-dark below it), sand with a wet line, darker wet intertidal sand below the high-tide mark, moss/grass on the hill and in patches on the terrace, snow on upward-facing surfaces in winter, procedural animated caustics under water. CPU-baked horizon AO per vertex plus canopy-cover darkening.

ARCHITECTURE (merge everything into one vertex-colored mesh + one emissive "glow" mesh; write a small Builder that adds boxes/cylinders/spheres/custom geometry with a color and a transform, then mergeGeometries)
- Ryōbu-style torii standing in the bay on the axis of the shrine (~1.9 tall): vermilion tapered main pillars with black base sheaths, four supporting sode-bashira legs with black caps and two connecting beams each, nuki tie beam, central strut with a dark plaque, shimaki, and a curved kasagi (extruded shape with upturned ends) with a black top layer. Pillars must end inside the shimaki, not poke through the kasagi.
- Shrine on stilts over the tidal flat: plank deck (with plank-gap strips and dark edge beams) on a grid of wooden stilts reaching the seabed; a main hall and a smaller front hall (white walls, vermilion posts and tie beams, shoji-style front panels = glow panels behind a thin dark lattice), a lower front stage with vermilion railings, and two roofed vermilion corridors on stilts running sideways then back to the shore.
- Roofs: a hip-roof generator with a concave profile and lifted eave corners (top surface dark cypress-bark brown, warm wood underside, pale fascia trim, black ridge cap).
- A five-storey pagoda on the hill clearing: stone plinth, white walls with vermilion posts, bracket layer, flared roofs decreasing in size, bronze finial with rings.
- Stone tōrō lanterns on the terrace and on the stage (hexagonal base, post, firebox with emissive windows, small roof, jewel).

VEGETATION
- ~4–5k canopy blobs (InstancedMesh of icospheres with vertex-noise displacement + fragment bump), clustered 2–4 per tree, per-instance AO from neighbour occlusion, brighter tops.
- Four kinds via an instance attribute: broadleaf, cherry, maple, pine (flattened pads). Cherries cluster lower on the hill and as 5 feature trees with visible trunks on the terrace; pines dominate the summit and the headlands.
- Colors come from per-kind dark/light palette uniforms that the JS blends across seasons.

SEASONS (cyclic 0..4 = spring, summer, autumn, winter; animated transition from a dock button)
- Spring: pink sakura, falling petals. Summer: lush green, no particles. Autumn: red maples, orange/yellow broadleaf, falling maple leaves. Winter: bare-ish brown deciduous blobs shrunk ~38%, snow on canopy tops, roofs, decks, rocks and ground; snowfall that melts instantly on the water.

WATER (realistic, not jelly)
- Pipeline: opaque scene → MSAA HalfFloat target with DepthTexture; copy to a second target, then draw the water with a custom ShaderMaterial doing a manual depth test; then floating particles; final fullscreen pass with ACES tone mapping, sRGB, subtle tilt-shift. Transparent canvas over the CSS background.
- Color from real thickness: reconstruct the depth behind each water pixel, Beer–Lambert absorption toward a deep scatter color derived from the user's water color (pale over the flats, blue in the deep; side walls get extra path length so they read as a water volume).
- Screen-space refraction, Fresnel sky reflection, sun glints from fine animated detail normals.
- Screen-space reflections (~26 ray-march steps against the depth buffer, fewer on mobile) so the torii, shrine and lit lanterns reflect in the water.
- Ripples: GPU wave equation on a 256×256 HalfFloat ping-pong target, fixed 60 Hz steps, land-mask texture so waves reflect off the shore. Cursor movement injects capsule drops along its path; a click makes a splash.
- Shore foam only where the terrain is near the water level AND gently sloped (no white outlines around cliffs, stilts or the torii pillars); foam band width scaled by slope; broken by noise.
- Tide: a dock toggle animates between high tide (0) and low tide (-0.55): the water block's rim moves and its sides stretch; at low tide the whole flat is exposed and the torii stands on wet sand.

PARTICLES (petals / leaves / snow, ~700 instanced quads, CPU-simulated)
- Spawn from cherry blobs (spring), deciduous blobs (autumn) or the sky (winter); flutter while falling; a gusting wind blows from the island toward the bay so they reach the water.
- Landing: on water they become floating (vertex shader lifts them by the same ripple + wave height as the water), drift slowly, get pushed by the cursor's movement and blown away by click splashes, strand when the tide drops, re-float when it rises; on land they rest and fade.
- Shapes drawn in the fragment shader: notched petal, five-lobed maple leaf, soft snow disc. Manual depth test against the scene depth.

KOI
- 7 koi (lathe body + forked fan tail + pectoral fins, merged), InstancedMesh with a swimming sway in the vertex shader and procedural patterns per type (kohaku, sanke, showa, ogon, plain orange). They wander, steer away from shallow water and the block walls, and flee the cursor and splashes. Rendered under the water so they are refracted and tinted.

TIME OF DAY (slider, shown as a clock from 11:00 to ~19:10)
- Sun elevation, color and intensity, hemisphere colors, and the water's sky reflection shift from noon to golden hour; towards dusk the shoji panels and lanterns glow (emissive) and three warm point lights light the shrine, the stage and the torii.

UI (editorial, minimal, English)
Brand "shiosai°" with a small torii mark, headline "A gate that / stands in the sea.", eyebrow "Shrine and tide, in miniature", a vertical caption "A study of tide and seasons", a location label "Shrine Cove · 34°16′ N · 132°19′ E", a floating pill dock (reset, season cycle with the current season name, High tide / Low tide toggle, Tune, fullscreen), hints and an adaptive FPS + "Season · time" readout in the footer, a glassy settings panel (season, time of day, falling petals; water color, tide level, wave height, ripple strength, clarity, caustics; sun azimuth, tilt-shift), and a "How it's made" card. Vermilion accent, light and dark themes via CSS tokens, responsive to 390 px (panel becomes a bottom sheet), prefers-reduced-motion respected, adaptive pixel ratio and a lighter mode for touch devices. Intro: the water fills the block while the camera eases in.
```

</details>
