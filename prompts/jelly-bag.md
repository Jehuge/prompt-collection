# 果冻沙袋 Jelly Bag

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：three.js r160 · WebGL2 · 形状匹配软体 · WebAudio
- **标签**：`threejs` `webgl2` `软体模拟` `形状匹配` `拳击` `合成音效` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110850396864369001) · [提示词帖](https://x.com/vib3coded/status/2110850719972544882) · 2026-10-16（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![果冻沙袋 Jelly Bag](../assets/jelly-bag.jpg)

## 提示词（英文原文）

```text
Build "Jelly Bag" — a single-file HTML toy: a hanging boxing heavy bag made of translucent gummy candy that you punch, swing and wobble. Everything in one .html file, English UI only.

TECH
- three.js r160 as an ES module from https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js (no addons). WebGL2; if unavailable, show a polite fallback message.
- Custom orbit camera (drag the background to walk around the bag, wheel/pinch to zoom, arrow keys rotate). Use setViewOffset so the bag stays framed beside the UI panel on desktop and above the bottom sheet on mobile.
- ACES tone mapping, sRGB output, custom PMREM "gym" environment (dark room, one warm overhead lamp).

SHAPE
- The bag is an SDF: a rounded vertical cylinder (radius 0.42, half-height 0.8, edge rounding 0.15) with a slight barrel bulge in the middle (+4.5% radius at mid-height).
- Mesh it with surface nets (cell ~0.017), snap vertices to the surface, normals from the SDF gradient.
- Hardware: a steel chain of ~34 alternating torus links from the ceiling, a swivel and a ring, then four dark leather straps from the ring down to the top of the bag. The straps are boxes re-stretched every frame between the ring and the deformed attachment points.
- About 120 tiny air bubbles suspended inside the jelly (instanced spheres) that ride along with the deformation.

SOFT-BODY PHYSICS
- Lattice of ~200 nodes (spacing 0.155) filling the bag. Neighbour springs plus free-body shape matching: each substep, find the best-fit rotation R (Müller 2016 quaternion extraction, warm-started) and center of mass c. Pull each node toward the goal g = R(r − c0) + c with stiffness kA, plus internal damping, a little air drag and gravity 9. Semi-implicit Euler, 10 substeps per frame.
- Top-layer nodes hang from the swivel anchor on tension-only rope springs (they pull only when taut). Make the rope damping strong enough that there's no bungee bounce. Run ~150 pre-roll steps so the bag starts settled, then give it a gentle opening swing.
- Clamp per-node displacement (MAXD ~0.32) so hard hits never fold the surface.
- Render the deformation on the GPU: upload residuals Rᵀ(x − c) + c0 − r to a float DataTexture. In the vertex shader (onBeforeCompile on MeshPhysicalMaterial), blend them with normalized Gaussian weights (σ ≈ 0.108), compute normals from the analytic Jacobian, then transform P = R·(p + disp − c0) + c.
- Firmness slider scales the spring stiffness; Wobble damping slider scales the damping.

PUNCHING & SCORING
- Pick the bag by sphere tracing the SDF in body space.
- Two red leather boxing gloves (fist, thumb, cuff, white band, dark lining) alternate left/right. Each punch flies in from beside the camera, lands at ~0.075 s, holds briefly, then pulls back by ~0.3 s. On landing, apply an impulse along the camera ray (blended with the inverse surface normal) with Gaussian falloff (σ 0.2): strength 6 + power × 15. A "Gloves" toggle hides them and applies the impulse directly.
- Quick tap (<160 ms) = jab with power 0.32–0.52. Hold to charge a power punch: a conic charge ring around the cursor fills over ~0.85 s, power up to 1.0.
- Drag the bag itself to grab it and swing it around on its chain; release to let it swing back.
- Keyboard: Space = tap to jab / hold to charge; Enter = jab.
- Punch force in kg ≈ (170 + power × 790) × small random jitter × combo bonus (+4% per chained hit, capped). Ranks: under 300 Featherweight, under 480 Lightweight, under 650 Middleweight, under 820 Heavyweight, otherwise "Knockout!".
- Combo counts hits landed within a short window. Best score is saved in localStorage; a new best plays a bell "ding" and highlights the rank.
- A gold force number pops at the hit point and floats up.

LOOK
- Transmission jelly material: transmission 1, thickness 0.9, IOR 1.36, low roughness, attenuation colour per flavour, clearcoat, sheen, a faint emissive inner glow, DoubleSide.
- Flavours: Cherry, Blueberry, Lime, Cola (body colour, attenuation, sheen, glow, shadow tint and UI accent change together).
- Overlay shell (same mesh pushed out along the normal, masked procedurally in the fragment shader with fwidth anti-aliasing and alphaToCoverage):
  - Every wrap: dark leather top and bottom caps with a stitch line.
  - Wraps: Classic — a white label panel with "JELLY" and "HEAVY BAG · 100% GUMMY" drawn into a canvas texture with a red border; Stripes — racing stripes; Flames — flames licking up from the bottom; Plain — caps only.
- Gym scene: dark rubber floor, warm directional lamp above, additive pool of light on the floor, ~90 dust motes drifting in the light, fog tied to camera distance so the bag never disappears on mobile.
- Planar projected shadow on the floor, tinted by the flavour (multiply blend + stencil, hidden from the transmission pass).
- Vignette over the canvas.

SOUND (WebAudio, synthesized, off by default)
- Punch: filtered noise smack + low sine thud, followed by a jelly "boing" (pitch-dropping sine with LFO wobble).
- New best: a three-partial bell ding.

UI
- Single dark theme. Fonts: Bebas Neue (display), Onest (UI), JetBrains Mono (labels).
- Top-left: eyebrow "Confectionery physics · No. 10", big title "Jelly / Bag.", lede "A heavy bag made of gummy candy. It takes every hit and wobbles back for more."
- How-to card: "Click to jab. Hold to load a power punch." plus drag/Space hints.
- Right panel: "Round 1 · live" badge, Gloves and Sound toggles. A black scoreboard with a large gold force readout in kg, rank line, a green→gold→red meter bar, Best / Punches / Combo stats and a Reset link. Then Flavour swatches, Wrap swatches, and the Firmness and Wobble damping sliders.
- Mobile: the panel becomes a bottom sheet (max ~44% height), sliders side by side, smaller title.
- Accessible labels on the canvas and buttons; respect touch input (no page scroll while punching).
```

---

## 提示词（中文）

构建 "Jelly Bag"（果冻沙袋）——一个单文件 HTML 玩具：一个由半透明软糖做成的悬挂式拳击重沙袋，你可以击打它、让它摆动和晃动。所有内容放在一个 .html 文件中，界面只用英文。

### 技术

- three.js r160 作为 ES 模块，从 https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js 引入（不用 addons）。WebGL2；不可用时显示礼貌的降级提示。
- 自定义环绕相机（拖动背景绕沙袋走动，滚轮/双指缩放，方向键旋转）。使用 setViewOffset，让沙袋在桌面端保持在 UI 面板旁边的取景中，在移动端保持在底部抽屉上方。
- ACES 色调映射、sRGB 输出，自定义 PMREM "健身房" 环境（暗室，头顶一盏暖色灯）。

### 形状

- 沙袋是一个 SDF：圆角竖直圆柱（半径 0.42，半高 0.8，边缘倒圆 0.15），中间略微鼓起成桶形（中部半径 +4.5%）。
- 用 surface nets 生成网格（单元约 0.017），顶点吸附到表面，法线取自 SDF 梯度。
- 五金件：从天花板垂下一条由约 34 个交替环面链环组成的钢链，一个转环和一个圆环，然后四条深色皮带从圆环连到沙袋顶部。皮带是盒体，每帧在圆环和变形后的连接点之间重新拉伸。
- 约 120 个悬浮在果冻内部的小气泡（实例化球体），随形变一起移动。

### 软体物理

- 约 200 个节点（间距 0.155）组成的晶格充满沙袋。邻居弹簧加自由体形状匹配：每个子步找出最佳拟合旋转 R（Müller 2016 四元数提取，热启动）和质心 c。以刚度 kA 把每个节点拉向目标 g = R(r − c0) + c，加上内部阻尼、一点空气阻力和重力 9。半隐式欧拉，每帧 10 个子步。
- 顶层节点通过只受拉的绳索弹簧（只有绷紧时才产生拉力）悬挂在转环锚点上。绳索阻尼要足够强，避免蹦极式弹跳。预先运行约 150 步，让沙袋开场时已经静止，然后给它一个轻柔的开场摆动。
- 钳制每个节点的位移（MAXD 约 0.32），使重击永远不会让表面折叠。
- 在 GPU 上渲染形变：把残差 Rᵀ(x − c) + c0 − r 上传到浮点 DataTexture。在顶点着色器中（对 MeshPhysicalMaterial 使用 onBeforeCompile），用归一化高斯权重（σ ≈ 0.108）混合它们，从解析雅可比矩阵计算法线，然后变换 P = R·(p + disp − c0) + c。
- Firmness 滑块缩放弹簧刚度；Wobble damping 滑块缩放阻尼。

### 击打与计分

- 在物体空间中对 SDF 做球体追踪（sphere tracing）来拾取沙袋。
- 两只红色皮革拳套（拳面、拇指、袖口、白色带、深色内衬）左右交替。每一拳从相机旁边飞入，约 0.075 s 命中，短暂停留，然后在约 0.3 s 时收回。命中时，沿相机射线方向（与表面法线反方向混合）施加一个带高斯衰减（σ 0.2）的冲量：强度 6 + power × 15。一个 "Gloves" 开关可以隐藏拳套并直接施加冲量。
- 快速点击（<160 ms）= 刺拳（jab），力量 0.32–0.52。按住可蓄力重拳：光标周围一个锥形蓄力环在约 0.85 s 内充满，力量最高 1.0。
- 直接拖动沙袋可以抓住它、让它在链子上甩动；松手让它摆回来。
- 键盘：空格 = 点按出刺拳 / 按住蓄力；回车 = 刺拳。
- 以 kg 计的出拳力量 ≈ (170 + power × 790) × 小幅随机抖动 × 连击加成（每次连续命中 +4%，有上限）。等级：低于 300 为 Featherweight（羽量级），低于 480 为 Lightweight（轻量级），低于 650 为 Middleweight（中量级），低于 820 为 Heavyweight（重量级），否则为 "Knockout!"。
- 连击统计在短时间窗口内命中的次数。最佳成绩保存在 localStorage；刷新纪录时播放一声铃响 "ding" 并高亮等级。
- 一个金色的力量数字在命中点弹出并向上飘。

### 外观

- 透射果冻材质：transmission 1，thickness 0.9，IOR 1.36，低粗糙度，按口味设置衰减颜色，清漆层（clearcoat）、光泽（sheen）、微弱的自发光内部辉光，DoubleSide。
- 口味：Cherry、Blueberry、Lime、Cola（身体颜色、衰减、光泽、辉光、阴影色调和 UI 强调色一起改变）。
- 叠加外壳（同一网格沿法线外推，在片元着色器中用 fwidth 抗锯齿和 alphaToCoverage 程序化遮罩）：
  - 每种包裹都有：深色皮革的顶盖和底盖，带一道缝线。
  - 包裹样式：Classic——一块白色标签面板，上面有画在 canvas 纹理中的 "JELLY" 和 "HEAVY BAG · 100% GUMMY"，带红色边框；Stripes——赛车条纹；Flames——从底部向上舔舐的火焰；Plain——只有顶盖和底盖。
- 健身房场景：深色橡胶地板，上方暖色平行光灯，地面上一汪加法混合的光，约 90 粒在光中飘动的灰尘，雾与相机距离挂钩，所以在移动端沙袋永远不会消失。
- 地面上的平面投影阴影，带口味色调（正片叠底混合 + 模板缓冲，在透射通道中隐藏）。
- canvas 上叠加暗角。

### 声音（WebAudio 合成，默认关闭）

- 出拳：滤波噪声的"啪"声 + 低沉正弦"咚"声，接着是一声果冻 "boing"（音高下降的正弦波，带 LFO 颤动）。
- 新纪录：三个泛音的铃声 ding。

### UI

- 单一深色主题。字体：Bebas Neue（展示）、Onest（UI）、JetBrains Mono（标签）。
- 左上：眉标 "Confectionery physics · No. 10"，大标题 "Jelly / Bag."，导语 "A heavy bag made of gummy candy. It takes every hit and wobbles back for more."
- 操作说明卡片："Click to jab. Hold to load a power punch." 加上拖动/空格的提示。
- 右侧面板："Round 1 · live" 徽章，Gloves 和 Sound 开关。一块黑色记分板，显示大号金色的力量读数（kg）、等级行、绿→金→红的仪表条、Best / Punches / Combo 统计和一个 Reset 链接。然后是口味色板、包裹样式色板，以及 Firmness 和 Wobble damping 滑块。
- 移动端：面板变为底部抽屉（最高约 44% 高度），滑块并排，标题更小。
- canvas 和按钮上有无障碍标签；正确处理触摸输入（击打时页面不滚动）。
