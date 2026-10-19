# 港口果冻 Harbor Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · boids · WebAudio
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `集装箱港口` `自动编排` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109794326574227823) · [提示词帖](https://x.com/vib3coded/status/2109794506232967245) · 2026-10-13（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "Harbor Jelly"（港口果冻）——一个单文件自包含 HTML（无外部请求、无第三方库），用 WebGPU/WGSL 渲染一个交互式 3D 微缩场景：一座小型的、正在运转的集装箱港口，置于一块会晃动的半透明方形果冻海中，放在纸质摄影棚背景上。它属于名为 "Material Studies" 的系列，所以要匹配该系列的外观：暖色纸张背景，衬线斜体展示标题（"Harbor Jelly."），小号大写眉标 "MATERIAL STUDIES"，右上角状态胶囊（"WebGPU · Live"），右侧磨砂控制面板，左下 "How to play" 一行。界面为英文。仅亮色主题，这是有意为之。

### 果冻块

- 一块 5.2 × 5.2 的块，用 3/4 环绕相机观看。地面和海在块的侧面被平整切开，所以能看到横截面上糖果色的土壤地层，海的切面透过果冻展示水下的一切。
- 水是在交错网格上的实时线性浅水模拟（高度在单元中心，速度在面上），带一点表面张力，让它感觉像果冻。渲染时要有折射、按深度吸收、投射到底面的焦散、光柱、菲涅尔摄影棚反射、泡沫（尾迹、水花、岸线蕾丝）以及切边上明亮的弯月面。
- 拖动侧面可以让整个块倾斜。水晃到低侧，果冻剪切并颤动，然后重新平静、恢复水平。

### 港口（布局）

- 后方是一道竖直的混凝土码头岸壁，有橡胶护舷、系缆桩、爬梯，水线以下长满贻贝和海草。
- 左侧：集装箱码头。平整的沥青堆场画着标线，带两条起重机轨道的混凝土条带，灯塔架，以及一个小的码头办公室。数百个彩色集装箱整齐成排堆放。每个都是带波纹的钢箱，有箱门端和颜色更深的角柱，以 GPU 实例绘制，约十种涂装。
- 右侧：一座古老的石砌渔港码头，有鹅卵石步道、波纹铁皮鱼市棚和灯柱。一座木栈桥立在长满贻贝的桩上，有交叉支撑，旁边系着两艘小渔船。
- 在这一切后面，一座小镇沿着长满青草的山坡向上延伸：三排人字形屋顶的房子，采用北欧港口色彩（法伦红、赭黄、白、浅蓝、薄荷绿、粉），瓦片或石板屋顶，白框窗户、门和烟囱。有一座带绿色铜尖顶的白色教堂，以及一些圆形的树。
- 一道乱石防波堤护卫着渔港，顶部有混凝土胸墙。大石块在堤顶附近，较小的、长满海草的石块滚落到水下。堤头立着一座红白相间条纹的灯塔，带观景廊和玻璃灯室，灯缓缓旋转。
- 开阔的港池中：两艘系在浮筒上随风摆动的小游艇（白色船体、彩色条纹、透过果冻可见的鳍龙骨、收起的帆），黄色系泊浮标，以及一个绿色航道浮标，都随波起伏。
- 海底：浅色沙子带淤泥堆积、海草丛、石头、海星、一个带锚链的旧锚、一个遗失的轮胎。

### 船的一天（全自动循环，约 100 秒）

1. 一艘小型支线集装箱船（海军蓝干舷、红色防污漆、船尾白色生活区带驾驶台两翼、带黄色色带的烟囱、旋转的雷达、可见的螺旋桨）靠泊在码头，甲板上装着集装箱，6 排位 × 4 列 × 2 层。
2. 轨道上两台岸桥（ship-to-shore 门式起重机），一红一蓝，各有门架腿、带机房的后伸臂、带前拉索的 A 形架、铰接的臂架、挂着司机室的小车，以及吊在四根钢丝绳上的黄色吊具。它们放下臂架交换箱子：从船上箱堆顶部卸箱到堆场箱堆，然后把别的箱子装上船。每个动作都是一个平滑的序列：大车行走、小车外伸、下放到箱子上（跟随船的起伏）、锁定、起升、小车横移、下放、解锁。两台起重机之间的距离不得小于其门腿宽度；空闲的起重机会让开另一台。
3. 作业完成后，小车停放，臂架向上收起，一艘拖船绕到船首。拖船有黑色船体、红白相间的上层建筑、一圈轮胎护舷、一个大的船首护舷，烟囱冒出一团团烟。它递出拖缆并倒车离开，把船首拉离码头，同时大船转出去。然后解掉拖缆，拖船原地掉头回港，大船鸣笛。
4. 大船沿一条平滑路径绕港口航行一圈，经过灯塔。它在多个采样点上随水起伏（起伏、俯仰、横滚），并把排开的水还给模拟，所以会留下真实的船首波、尾迹和白水。
5. 与此同时，拖船驶到一个待命点。当大船停在码头外时，拖船顶上去，把它横推靠上护舷，螺旋桨尾流翻腾。然后拖船后退离开，臂架放下，起重机重新开始工作。

- 保证一切无碰撞（大船和拖船 vs. 码头、防波堤、栈桥、游艇和浮标；不得搁浅）。用一个无头 node 测试来检查。

### 生命

- 鱼群（鲭鱼、鲱鱼、橙色小隆头鱼）作为 boids，始终待在水中、在船体下方，遇到手指、水花和行驶的船会散开，有食物时会聚过来。
- 海月水母：玻璃般脉动的伞盖，有四个粉色环、褶皱的口腕和一圈触手。随水流漂移。
- 银鸥（白身、灰色背羽、黑色翼尖、带红点的黄喙）。它们盘旋、侧倾、滑翔，并落在栖点上：路灯、屋脊、教堂尖顶、灯塔观景廊、起重机顶端、船的桅杆、拖船、游艇桅顶。移动物体上的栖点会随之移动。汽笛响起时它们全部起飞，一些会俯冲去抢食物。
- 鸣笛时船的烟囱喷出蒸汽；果冻中困着细小气泡。

### 控制（右侧面板；手机上为底部抽屉）

- "Cast off"（解缆）让船提前出发（起重机先完成手上那只箱子）。出海后按钮变为 "Call her in"（召回），催她回港；忙碌时按钮置灰。
- "Horn"（汽笛，也可按空格）播放合成的 WebAudio 船笛：两个相隔五度、略微失谐的低音锯齿"簧片"，经过低通，只有在用户手势之后才开始。它还会喷出蒸汽并惊散海鸥。
- "Feed the fish"（喂鱼）从栈桥末端撒下饲料；鱼冲过来，海鸥俯冲而下。
- 计数：Boxes moved / Voyages / Fed（搬运箱数 / 航次 / 喂食）。一行船舶状态（"Unloading 3 / 8"、"Loading"、"Booms up"、"Tug coming"、"Casting off"、"At sea 40%"、"Coming in"、"Berthing"）。一个小的活跃度仪表。
- 口味色板改变水色和地层：Sea glass（海玻璃，青薄荷）、Blueberry（蓝莓，深蓝）、Lime（青柠）。
- 滑块：Firmness、Wave damping、Tide（±10 cm；海平面、船只和漂浮物随之变化）。
- 按钮：Reset、Pause、Sound on/off、Reset view。

### 指针交互

- 在水面上拖动造浪（光标为十字准星）。
- 拖动块的侧面使其倾斜。
- 捡起一个橙白相间的救生圈扔出去。救生圈平浮在波浪上，会从栈桥、建筑和防波堤上弹开，并被大船和拖船推开。
- 拖动空白处或右键拖动来环绕视角；滚轮或双指缩放。
- 手机上：触摸环绕、双指缩放，以及一个可折叠的控制底部抽屉。

### 渲染细节

- 管线：阴影贴图 → 焦散通道 → 不透明场景（带距离缓冲）→ 水的背面通道 → 在场景副本上的水面通道 → 色调映射 + 抖动。
- 移动的装置是静态顶点缓冲，其顶点带有物体 id；大约 24 个物体变换（位置 + 四元数）放在 uniform 缓冲中。缆绳的两端分别位于各自物体的坐标系中，所以会拉伸：起重机钢丝绳、前拉索、拖缆。
- 道具着色器中的材质类型：哑光涂料、玻璃、光泽钢、屋瓦、木纹、波纹板（扰动法线形成凸棱）、方整石砌体、橡胶、岩石、发光的灯、摇曳的海草，以及水线条（boot-top）以下涂防污漆的船体。
- 果冻的剪切和压扁晃动作用于块内的一切。

### 质量标准

- 在笔记本上流畅运行；模拟每帧约 2 ms 以内。
- 缺少 WebGPU 或 adapter 失败时显示友好的降级页面。
- 无控制台报错，页面不滚动。遵守 prefers-reduced-motion。
- 交付时附带一个编排逻辑的无头测试和一个 Playwright 端到端测试。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Harbor Jelly" — a single self-contained HTML file (no external requests, no libraries) that renders an interactive 3D diorama with WebGPU/WGSL: a small working container harbor set inside a square block of wobbly, translucent jelly sea, sitting on a paper studio backdrop. It belongs to a series called "Material Studies", so match that look: warm paper background, serif italic display title ("Harbor Jelly."), small uppercase eyebrow "MATERIAL STUDIES", a status pill top-right ("WebGPU · Live"), a frosted control panel on the right, and a "How to play" line bottom-left. English UI. Light theme only, by design.

THE BLOCK
- A 5.2 × 5.2 block seen from a 3/4 orbit camera. The ground and sea are cut flat at the block's sides, so you see candy-coloured soil strata in cross-section, and the sea's cut faces show everything underwater through the jelly.
- The water is a real-time linear shallow-water simulation on a staggered grid (heights at cell centres, velocities on faces) with a little surface tension, so it feels like jelly. Render it with refraction, absorption by depth, caustics projected onto the floor, light shafts, a Fresnel studio reflection, foam (wakes, splashes, a shoreline lace) and a bright meniscus on the cut edges.
- The whole block can be tipped by dragging its side. The water sloshes to the low side, the jelly shears and quivers, then it settles flat again.

THE HARBOR (layout)
- Along the back runs a vertical concrete quay wall, with rubber fenders, bollards, ladders, and mussels and weed crusting it below the waterline.
- Left part: a container terminal. A flat asphalt yard with painted lines, concrete strips with two crane rails, light towers, and a small terminal office. Hundreds of colourful containers are stacked in neat rows. Each is a ribbed steel box with door ends and darker corner posts, drawn as GPU instances in about ten liveries.
- Right part: an old stone fishing quay with a cobbled promenade, a corrugated fish-market shed and lamp posts. A timber pier stands on mussel-covered piles with cross-bracing, with two small fishing boats moored alongside.
- Behind it all, a town climbs a grassy hill: three rows of gabled houses in Nordic harbour colours (falu red, ochre, white, pale blue, mint, pink) with tiled or slate roofs, white-framed windows, doors and chimneys. There is a white church with a green copper spire, and some round trees.
- A rubble breakwater shelters the fishing harbour, with a concrete crown wall. Big rocks sit near the crest, smaller weedy ones tumble down under water. On its head stands a red-and-white banded lighthouse with a gallery and a glass lantern, whose lamp slowly turns.
- In the open basin: two small yachts swinging on their moorings (white hulls, coloured stripe, fin keels visible through the jelly, furled sails), yellow mooring buoys, and a green channel buoy, all bobbing on the waves.
- On the floor: pale sand with drifts of silt, weed tufts, stones, starfish, an old anchor with chain, a lost tyre.

THE SHIP'S DAY (fully automatic loop, about 100 s)
1. A small feeder container ship (navy topsides, red antifouling, white accommodation block at the stern with bridge wings, funnel with a yellow band, turning radar, visible propeller) lies alongside with containers on deck, 6 bays × 4 rows × 2 tiers.
2. Two ship-to-shore gantry cranes on the rails, one red and one blue, each with portal legs, a backreach with a machinery house, an A-frame with forestays, a hinged boom, a trolley with a hanging cab, and a yellow spreader on four wire falls. They lower their booms and swap boxes: unload from the tops of the ship's stacks into yard stacks, then load other boxes aboard. Every move is a smooth sequence: travel, trolley out, lower onto the box (tracking the ship's bobbing), latch, hoist, trolley across, lower, unlatch. Cranes never get closer than their leg width; an idle crane moves out of the other's way.
3. When the work is done the trolleys park, the booms swing up, and a tug comes round to the bow. The tug has a black hull, white and red superstructure, a tyre fender all round, a big bow fender, and puffs of funnel smoke. It passes a tow line and backs away, pulling the bow off the quay while the ship swings out. Then the line is cast off, the tug pivots on the spot and goes home, and the ship sounds her horn.
4. The ship sails a lap of the harbour along a smooth path, past the lighthouse. She rides the water on several sample points (heave, pitch, roll) and hands the displaced water back to the sim, so she leaves a real bow wave, wake and white water.
5. Meanwhile the tug goes out to a standby spot. When the ship stops off the quay, the tug noses in and pushes her sideways onto the fenders, with prop wash churning. Then it backs off, the booms come down, and the cranes start again.
- Keep everything collision-free (ship and tug vs. quay, breakwater, pier, yachts and buoy; no grounding). Check it with a headless node test.

LIFE
- Fish schools (mackerel, herring, small orange wrasse) as boids that stay in the water and under the hulls, scatter from fingers, splashes and moving ships, and come to food.
- Moon jellyfish: glassy pulsing bells with four pink rings, frilly oral arms and a fringe of tentacles. They drift with the water flow.
- Herring gulls (white body, grey mantle, black wingtips, yellow bill with a red spot). They circle, bank and glide, and land on perches: lamps, roof ridges, the church spire, the lighthouse gallery, the crane apexes, the ship's mast, the tug, the yachts' masthead. Perches on moving things move with them. They all take off when the horn sounds, and some dive at food.
- Steam puffs from the ship's funnel on the horn; tiny bubbles caught in the jelly.

CONTROLS (right panel; bottom sheet on phones)
- "Cast off" sends the ship early (cranes finish the box in hand). At sea the button becomes "Call her in" and hurries her home; it greys out while busy.
- "Horn" (also Space) plays a synthesized WebAudio ship horn: two low detuned sawtooth reeds a fifth apart, low-passed, starting only after a user gesture. It also blows steam and scatters the gulls.
- "Feed the fish" scatters pellets off the end of the pier; fish rush in and gulls swoop down.
- Tally: Boxes moved / Voyages / Fed. A ship status line ("Unloading 3 / 8", "Loading", "Booms up", "Tug coming", "Casting off", "At sea 40%", "Coming in", "Berthing"). A small activity meter.
- Flavour swatches change the water colour and strata: Sea glass (teal-mint), Blueberry (deep blue), Lime.
- Sliders: Firmness, Wave damping, Tide (±10 cm; the sea level, ships and floating things follow).
- Buttons: Reset, Pause, Sound on/off, Reset view.

POINTER INTERACTION
- Drag across the water to make waves (with a crosshair cursor).
- Drag the side of the block to tip it.
- Pick up an orange-and-white lifebuoy and throw it. Lifebuoys float flat on the waves, bounce off the pier, buildings and breakwater, and are shoved aside by the ship and tug.
- Drag empty space or right-drag to orbit; scroll or pinch to zoom.
- On phones: touch orbit, pinch zoom, and a collapsible bottom sheet for the controls.

RENDERING DETAILS
- Pipeline: shadow map → caustics pass → opaque scene (with a distance buffer) → back-face pass of the water → water pass over a copy of the scene → tone map + dither.
- Moving rigs are static vertex buffers whose vertices carry an object id; about 24 object transforms (position + quaternion) live in the uniform buffer. Cables are drawn with one end in each object's frame, so they stretch: crane falls, forestays, the tow line.
- Material kinds in the prop shader: matte paint, glass, gloss steel, roof tiles, timber grain, corrugated sheet (normal-perturbed ribs), dressed-stone masonry, rubber, rock, glowing lamps, swaying weed, and hulls with antifouling below a boot-top line.
- The jelly shear and squash wobble applies to everything inside the block.

QUALITY BAR
- Smooth on a laptop; simulation under about 2 ms per frame.
- A friendly fallback screen if WebGPU is missing or the adapter fails.
- No console errors, no page scroll. Respect prefers-reduced-motion.
- Ship it with a headless test of the choreography and a Playwright end-to-end test.
```

</details>
