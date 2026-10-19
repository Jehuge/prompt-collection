# 珊瑚泻湖 Reef Lagoon

- **类型**：交互网页 / 俯视海洋模拟
- **技术栈**：Three.js r128 · WebGL · 单文件 HTML
- **标签**：`threejs` `webgl` `水面模拟` `焦散` `海洋生物` `合成音效` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs Gemini 4 Argon vs GPT-6.1 Sol vs GPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111888587360792982) · [提示词帖](https://x.com/vib3coded/status/2111889560237961423) · 2026-10-19（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5, Gemini 4 Argon, GPT-6.1 Sol, GPT-6 Astra 四个模型）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![珊瑚泻湖 Reef Lagoon](../assets/reef-lagoon.jpg)

## 提示词（中文）

构建一个名为 "Reef Lagoon"（珊瑚泻湖）的单文件自包含 HTML（内联 CSS 和 JS；唯一的外部脚本是来自 https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js 的 Three.js r128）：一个阳光照耀的马尔代夫风格泻湖的交互式俯视视图，用户把海洋生物扔进水里，看它们游动。输出完整文件，不要占位符，不要省略任何部分。

### 相机与布局

- 透视相机正上方俯视（高度约 26 世界单位，up 向量 (0,0,-1)）。调整竖直 FOV，使屏幕短边方向的可见水面约为 ±8.4 单位；长边方向随宽高比缩放。窗口尺寸变化时重新计算。
- 整个屏幕都是水。在玩具比例下，一个世界单位约等于 1 m：海豚约 2.4，大白鲨约 3.3，双髻鲨约 3.1，虎鲸约 4.5，座头鲸约 6，海龟背甲长约 1.35，蝠鲼体长约 1.6 / 翼展 3.2。

### 水面模拟

- GPU 涟漪高度场（ping-pong 的 float/half-float 渲染目标，长边约 440 个纹素，以 90 Hz 步进）。更新：取 4 个邻居的平均值，velocity += (avg − h)*1.8，velocity *= 0.9935，h += velocity，h *= 0.9993。吸收型"海绵"边缘，使离开屏幕的波浪不会反射。
- 水滴放入队列（x、z、半径、振幅、泡沫），用平滑的余弦凸包施加；第二个通道存储会扩散并消退的泡沫。

### 渲染（每帧绘制顺序）

1. 一张可平铺的动态焦散纹理（512²，带 mipmap）。
2. 阴影通道：生物几何体沿太阳方向投影到底面，从主相机渲染到半分辨率目标，使用 MAX 混合。
3. 把水下场景渲染到离屏目标。其 alpha 存储 depth*0.22，之后用于缩放折射和模糊。
   - 底面：一个大的高度场网格。深度从屏幕底部附近约 1.35 到顶部约 4.3，带轻微起伏。
   - 珊瑚头来自噪声遮罩：隆起 1–1.4 单位，暖色的赭/紫/黄色调，带疙瘩状和脑珊瑚细节，周围一圈碎石。
   - 浅色沙子，带柔和不规则的沙纹明暗。
   - 光照：环境光 + 太阳 × (基础 + 由涟漪场拉普拉斯聚焦的焦散) × 阴影 × 漂移的云影（大尺度缓慢噪声）。
   - 沿光路加视线路径的水吸收，例如 T = exp(−(0.30, 0.058, 0.04)·path)，加上按深度的松石绿→蓝散射。
4. 一个全屏水面通道。每个像素通过逆视图投影向平面 y=0 投射射线。
   - 表面法线来自涟漪场 + 滚动的风纹梯度噪声 + 轻柔的涌浪。
   - 折射：偏移采样水下目标，带色散分离和深度模糊。
   - 带云的菲涅尔天空反射、阳光闪烁、泡沫、水花坑（每次撞击周围一个短暂存在的解析碗形；要提亮它，绝不能让它变暗），以及一个可选的带螺旋泡沫臂的漩涡漏斗。
   - 温和的色调曲线。
5. 一个开启深度测试、在水面之后绘制的叠加通道：水面以上的生物、水滴（点精灵，重力 20）、柔和的水雾精灵、雨丝、扩散的环形四边形，以及一个落点标记。

### 生物（程序化几何体，无外部模型）

- 局部坐标系：鼻尖在 +x（x=0.5），尾巴朝 −x，上方为 +y，身体长度为 1。
- 身体：沿 x 放样的椭圆横截面。半宽 W(u)、半高 H(u) 和中心偏移 C(u) 是穿过控制点的 Catmull-Rom 曲线，其中 u 从鼻尖的 0 到尾部的 1。压平腹部，封闭两端，从网格计算法线。
- 鳍：薄薄的双面片，作为根弦与梢弦之间的双线性面片生成，前缘和后缘带弧度。
- 物种：
  1. 大白鲨：石板灰背部，参差的反荫蔽分界线过渡到白色腹部，鳃裂，高大的三角形背鳍，宽大后掠的胸鳍（下面尖端为深色），上叶更长的新月形尾巴。
  2. 无沟双髻鲨：扁平宽阔的头翼，眼睛在两端，古铜灰色，高大的镰刀形背鳍。
  3. 座头鲸：近黑色背部，带喉褶的斑驳白色腹部，头部有瘤状突起，非常长的扇贝边白色胸鳍，小背鳍凸起，锯齿状尾鳍。
  4. 虎鲸：黑色，带白色眼斑、白色下巴、腹部和体侧白斑，高耸背鳍后方的灰色鞍斑，桨形胸鳍。
  5. 宽吻海豚：喙和隆起的额隆（melon），灰色体侧上方的深色"披肩"和浅色腹部，弯曲的背鳍。
  6. 绿海龟：带盾片花纹和琥珀色条纹的隆起背甲，浅色腹甲，带鳞片的头，长长的前鳍肢和小小的后鳍肢。
  7. 蝠鲼：菱形后掠双翼，嘴边卷曲的角状头鳍，鞭状尾巴，黑色背部带白色肩部 V 形斑，白色带斑点的腹部。
- 每个物种绘制为一个 InstancedBufferGeometry。每实例数据：位置、朝向四元数、(游动相位、波动振幅、转向、鳍相位)、(缩放、alpha、身体拱曲、鳍振幅)、(种子、水体分类标志、湿润度、鳍肢角度偏移)。
- 顶点着色器：
  - 游动身体波：鲨鱼左右摆动，鲸、虎鲸和海豚上下摆动，海龟和蝠鲼没有。
  - 振幅包络朝尾部增大，加上转向曲率和拱曲。
  - 旋转每个横截面，使其始终垂直于弯曲的脊柱。
  - 让鳍肢绕身体轴上的铰链旋转。
  - 蝠鲼翅膀拍动向外传播，振幅 ∝ |z|^1.45。
  - 在顶点处采样 GPU 水面高度，用于水线。
- 每个物种分三个通道渲染：水下（丢弃高于局部水面高度的片元，按水着色）、水上（丢弃低于水面的部分）、阴影（投影到底面）。也用同样的材质渲染卡片缩略图。
- 用有序（Bayer）抖动做淡入淡出。光照：天空/地面环境光，水下带焦散的太阳漫反射，湿润时增强的光泽镜面反射，边缘光，在着色器中把眼睛画成深色球体。

### 行为

- 游动：在屏幕内漫游转向（保持在底部 UI 栏上方），生物之间保持间隔，偏好深度并与底面保持距离，朝目标深度俯仰，转弯时侧倾，受漩涡水流影响。
- 鲸、虎鲸和海豚定期浮上水面呼吸和喷水：水滴柱加柔和的水雾精灵加喷气声。座头鲸的喷气呈灌木状，虎鲸的高，海豚只是一小团。座头鲸下潜时尾鳍朝上。
- 鲨鱼常常让背鳍划破水面巡游，留下由小水滴组成的 V 形尾迹。
- 海龟浮上水面换气；蝠鲼拍着翅膀滑翔。
- 海豚经常做海豚式跃水；虎鲸、座头鲸、鲨鱼和蝠鲼偶尔跃出水面。跃出水面意味着快速上升，带着出水水花冲出水面，然后按下面各物种的风格重新入水。
- 点击水面产生涟漪。鲨鱼、海豚和虎鲸会过来查看那个地方；海龟和蝠鲼会逃开。

### 入水：每个物种各不相同（核心功能）

- 点击生物卡片时，从卡片的屏幕位置（投影到水平面上，y=0.6）沿抛物线把生物扔到一个随机的空位。
- 每个物种的重力（鲸 6.2，虎鲸 7.5，海豚 11，其余 10）和飞行时间（鲸 1.8 s，虎鲸 1.5，双髻鲨 1.3，蝠鲼 1.35，鲨鱼 1.2，海豚 1.15，海龟 1.0）。初速度：vy = (−y0 + ½gT²)/T。
- 在空中，朝向按飞行进度 τ ∈ [0,1] 编排，相对于轨迹俯仰角，并在前 22% 内从初始朝向混合过来：
  - 鲨鱼：鼻尖陡然朝下，像刀一样切入；尾巴猛甩。
  - 双髻鲨：螺旋翻转，转两整圈。
  - 座头鲸：翻成仰面（≈2.75 rad）再放平，胸鳍抬起，身体拱曲：一个背部拍水（backflop）。
  - 虎鲸：翻成侧面（≈1.5 rad）再放平。
  - 海豚：沿弧线干净利落地头朝下入水。
  - 海龟：鳍肢拍打着摇摇晃晃，肚子先拍到水面。
  - 蝠鲼：向前空翻（−2π），翅膀平拍水面，翅膀拍动。
- 每种入水都有自己的水花：一个水坑，长体型动物沿身体线再加几个水滴，扩散的环，按物种设定数量和速度的水滴"王冠"，水雾，气泡，以及声音。
  - 海豚：微小的 "rip" 入水水花。
  - 鲨鱼：高高的水冠；双髻鲨额外加螺旋水滴。
  - 座头鲸：巨大的白色水幕（约 500 个水滴）、水雾和一声低沉的轰响。
  - 虎鲸：大的侧向水花。
  - 海龟：低平的"扑通"。
  - 蝠鲼：宽而低的一片水雾和一声清脆的拍击。
- 入水后，生物在水下减速，拖出一串气泡，在 1.6–3.2 s 内 slerp 回游动朝向（鲸会从仰面翻回来），然后开始游动。
- 拖动卡片会让生物悬在指针下方的水面上空（水面上有目标圈），松手时以它自己的入水风格放下。
- 用户可以从水中抓起任意生物（按到其投影身体轴的距离拾取），搬运它，再把它扔回去。

### UI（英文）

- 底部磨砂玻璃栏：7 张生物卡片，缩略图由真实模型渲染，每张配一句简短描述（"Knifes straight in"、"Corkscrew dive"、"Backflop breach"、"Lands on its side"、"Clean arc dive"、"Belly plop"、"Wing slap"）。手机上显示简短名称。
- 工具按钮：Rain（雨丝、环形涟漪、太阳变暗）、Whirlpool（可拖动的、会带走生物的漩涡）、Calm、Clear（所有生物游走并淡出）、Sound（合成的 Web Audio：水花、扑通声、喷气、拍击、轰响、偶尔的座头鲸歌声、海豚哨声、虎鲸叫声、环境水声）、Hide UI。
- 左上铭牌 "Reef Lagoon"，带实时生物计数；提示气泡（toast）和一行提示。
- 键盘：1–7 扔出生物，R W C M H。

### 质量与健壮性

- 在桌面端和移动端（触摸、pointer events、无横向溢出）以及 WebGL2 和 WebGL1 下都能运行。
- 帧率慢时自适应像素比。
- 上限：总共 24 只生物，座头鲸最多 3 只。
- 开场时已有两只海豚、一只海龟、一条鲨鱼和一只蝠鲼在游；加载 1 秒后一头座头鲸跃出水面。
- 出现运行时错误和 WebGL 上下文丢失时显示提示气泡。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single self-contained HTML file (inline CSS and JS; the only external script is Three.js r128 from https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js) called "Reef Lagoon": an interactive top-down view of a sunlit Maldives-style lagoon where the user throws sea creatures into the water and watches them swim. Output the complete file, no placeholders, no omitted sections.

CAMERA AND LAYOUT
- Perspective camera straight overhead (height ~26 world units, up vector (0,0,-1)). Fit the vertical FOV so the visible water is about ±8.4 units in the short screen direction; the long direction scales with the aspect ratio. Recompute on resize.
- The whole screen is water. One world unit is roughly 1 m at toy scale: dolphin ~2.4, white shark ~3.3, hammerhead ~3.1, orca ~4.5, humpback ~6, turtle ~1.35 shell length, manta ~1.6 length / 3.2 wingspan.

WATER SIMULATION
- GPU ripple height field (ping-pong float/half-float render targets, about 440 texels on the long side, stepped at 90 Hz). Update: average of 4 neighbours, velocity += (avg − h)*1.8, velocity *= 0.9935, h += velocity, h *= 0.9993. Absorbing "sponge" edges, so waves leaving the screen don't reflect.
- Drops are queued (x, z, radius, amplitude, foam) and applied with a smooth cosine bump; a second channel stores foam that diffuses and fades.

RENDERING (draw order per frame)
1. A tileable animated caustics texture (512², mipmapped).
2. A shadow pass: creature geometry projected along the sun onto the floor, rendered from the main camera into a half-res target with MAX blending.
3. The underwater scene into an off-screen target. Its alpha stores depth*0.22, which later scales refraction and blur.
   - Floor: a large heightfield mesh. Depth goes from ~1.35 near the bottom of the screen to ~4.3 at the top, with gentle undulation.
   - Coral heads come from noise masks: raised 1–1.4 units, warm ochre/purple/yellow colours with knobbly and brain-coral detail, plus a rubble ring around them.
   - Pale sand with soft irregular ripple shading.
   - Lighting: ambient + sun × (base + caustics focused by the Laplacian of the ripple field) × shadow × drifting cloud shadows (large slow noise).
   - Water absorption along the light path plus the view path, e.g. T = exp(−(0.30, 0.058, 0.04)·path), plus depth-based turquoise→blue scatter.
4. A full-screen water-surface pass. Each pixel is ray-cast through the inverse view-projection to the plane y=0.
   - Surface normal from the ripple field + scrolling wind-ripple gradient noise + a gentle swell.
   - Refraction: offset sampling of the underwater target, with chromatic split and depth blur.
   - Fresnel sky reflection with clouds, sun glints, foam, splash craters (a short-lived analytic bowl around each impact; brighten it, never let it go dark), and an optional whirlpool funnel with spiral foam arms.
   - Mild tone curve.
5. An overlay pass, depth-tested, drawn after the surface: creatures above water, water droplets (point sprites, gravity 20), soft mist sprites, rain streaks, expanding ring quads, and a drop-target marker.

CREATURES (procedural geometry, no external models)
- Local frame: nose at +x (x=0.5), tail toward −x, up +y, body length 1.
- Body: lofted elliptical cross-sections along x. Half-width W(u), half-height H(u) and centre offset C(u) are Catmull-Rom curves through control points, where u runs 0 at the nose to 1 at the tail. Flatten the belly, cap the ends, compute normals from the grid.
- Fins: thin double-sided sheets made as bilinear patches between a root chord and a tip chord, with bowed leading and trailing edges.
- Species:
  1. Great white shark: slate-grey back with a ragged countershading line to a white belly, gill slits, tall triangular dorsal fin, big swept pectorals with dark tips underneath, crescent tail with a longer upper lobe.
  2. Great hammerhead: flat wide cephalofoil with eyes at its tips, bronze-grey colour, tall sickle dorsal fin.
  3. Humpback whale: near-black back, mottled white belly with throat pleats, knobs on the head, very long scalloped white pectorals, small dorsal hump, serrated flukes.
  4. Orca: black, with the white eye patch, white chin, belly and flank lobe, grey saddle behind a towering dorsal fin, paddle-shaped pectorals.
  5. Bottlenose dolphin: beak and melon forehead, dark cape over grey flanks and a pale belly, curved dorsal fin.
  6. Green sea turtle: domed shell with scute pattern and amber streaks, pale belly plate, scaly head, long front flippers and small rear flippers.
  7. Manta ray: diamond-shaped swept-back wings, curled horn-like fins at the mouth, whip tail, black top with white shoulder chevrons, white spotted belly.
- Draw each species as one InstancedBufferGeometry. Per-instance data: position, orientation quaternion, (swim phase, wave amplitude, turn, fin phase), (scale, alpha, body arch, fin amplitude), (seed, water-class flag, wetness, flipper angle offset).
- Vertex shader:
  - Swimming body wave: side to side for sharks, up and down for whales, orca and dolphins, none for turtle and manta.
  - Amplitude envelope grows toward the tail, plus turn curvature and arch.
  - Rotate each cross-section to stay perpendicular to the bent spine.
  - Rotate flippers on hinges about the body axis.
  - Manta wing beat travels outward with amplitude ∝ |z|^1.45.
  - Sample the GPU water height at the vertex for the waterline.
- Render each species in three passes: under water (discard fragments above the local water height, tint by water), above water (discard below), shadow (project to the floor). Also render card thumbnails with the same materials.
- Fade with an ordered (Bayer) dither. Lighting: sky/ground ambient, sun diffuse with caustics under water, glossy specular that increases when wet, rim light, eyes as dark spheres in the shader.

BEHAVIOUR
- Swimming: wander steering inside the screen (stay above the bottom dock UI), separation between creatures, preferred depth with floor clearance, pitch toward the target depth, roll into turns, currents from the whirlpool.
- Whales, orcas and dolphins periodically surface to breathe and spout: droplet column plus soft mist sprites plus a blow sound. Humpback spout is bushy, orca tall, dolphin a small puff. The humpback dives fluke-up.
- Sharks often cruise with the dorsal fin cutting the surface and leaving a V-wake of small drops.
- Turtles surface to breathe; mantas glide with wing beats.
- Dolphins porpoise-leap often; orca, humpback, shark and manta occasionally breach. A breach means rising fast, launching out of the water with an exit splash, then re-entering in the species style below.
- Tapping the water makes ripples. Sharks, dolphins and orcas come to look at the spot; turtles and mantas flee.

ENTERING THE WATER: EACH SPECIES DIFFERENT (the core feature)
- Tapping a creature card throws the creature from the card's screen position (projected onto the water plane, y=0.6) along a ballistic arc to a random free spot.
- Per-species gravity (whale 6.2, orca 7.5, dolphin 11, others 10) and flight time (whale 1.8 s, orca 1.5, hammerhead 1.3, manta 1.35, shark 1.2, dolphin 1.15, turtle 1.0). Start velocity: vy = (−y0 + ½gT²)/T.
- In the air, orientation is scripted against flight progress τ ∈ [0,1], relative to the trajectory pitch, and blended in from the start orientation over the first 22%:
  - Shark: noses steeply down for a knife entry; tail thrashes.
  - Hammerhead: corkscrews, two full rolls.
  - Humpback: rolls onto its back (≈2.75 rad) and levels out, pectorals raised, body arched: a backflop.
  - Orca: rolls onto its side (≈1.5 rad) and levels out.
  - Dolphin: follows the arc for a clean head-first dive.
  - Turtle: wobbles with flippers flapping into a belly-flop.
  - Manta: forward somersault (−2π) into a flat wing slap, wings beating.
- Each entry has its own splash: a crater drop plus several drops along the body line for long animals, expanding rings, a droplet crown with species-specific counts and speeds, mist, bubbles, and sound.
  - Dolphin: tiny "rip" splash.
  - Sharks: tall crown; hammerhead adds spiral droplets.
  - Humpback: huge white curtain (~500 droplets), mist and a low boom.
  - Orca: big side splash.
  - Turtle: low flat plop.
  - Manta: wide low sheet of spray and a sharp slap.
- After entry the creature decelerates under water with a bubble trail, slerps back to its swimming orientation over 1.6–3.2 s (the whale rolls back over from its back), then swims.
- Dragging a card holds the creature above the water under the pointer (with a target ring on the water) and drops it on release with its own entry style.
- The user can grab any creature from the water (pick by distance to its projected body axis), carry it, and throw it back.

UI (English)
- Frosted-glass dock at the bottom: 7 creature cards with thumbnails rendered from the real models and a short description each ("Knifes straight in", "Corkscrew dive", "Backflop breach", "Lands on its side", "Clean arc dive", "Belly plop", "Wing slap"). On phones show short names.
- Tool buttons: Rain (streaks, ring ripples, dimmer sun), Whirlpool (draggable vortex that carries creatures), Calm, Clear (all creatures swim off and fade), Sound (synthesized Web Audio: splashes, plops, blows, slaps, booms, occasional humpback song, dolphin whistles, orca calls, ambient water), Hide UI.
- Top-left name plate "Reef Lagoon" with a live creature count; toasts and a hint line.
- Keyboard: 1–7 throw creatures, R W C M H.

QUALITY AND ROBUSTNESS
- Works on desktop and mobile (touch, pointer events, no horizontal overflow) and in both WebGL2 and WebGL1.
- Adaptive pixel ratio when frames are slow.
- Caps: 24 creatures total, max 3 humpbacks.
- Start with two dolphins, a turtle, a shark and a manta already swimming; a humpback breaches 1 s after load.
- Show a toast for runtime errors and lost WebGL contexts.
```

</details>
