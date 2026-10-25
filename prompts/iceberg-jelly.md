# 冰山果冻 Iceberg Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · 刚体冰块 · WebAudio
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `冰山崩解` `极地动物` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2110517313413796092) · [提示词帖](https://x.com/vib3coded/status/2110517517395403207) · 2026-10-15（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。结尾的 "publish it as an artifact" 是针对 Claude Artifacts 的要求，其他工具可忽略。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![冰山果冻 Iceberg Jelly](../assets/iceberg-jelly.jpg)

## 提示词（英文原文）

```text
Build "Iceberg Jelly" — the next piece in my "Material Studies" series of jelly dioramas: a single self-contained HTML file using WebGPU (WGSL), no external libraries, English UI.

THE SCENE
A square block of jelly (5.2 × 5.2 units) standing on a pale, cool-grey paper studio backdrop with a soft floor shadow. Inside it, a polar bay:
- At the back left, a glacier flows down a valley between jagged mountains and ends in an ice cliff standing in deep water. The cliff has vertical runnels and blue bands. The glacier surface has chevron crevasses along its margins, transverse crevasses and seracs near the front, and grey lateral moraines. Its tongue is flanked by moraine banks, so only its front stands in the water.
- Mountains: a peaky left range and a spur on the right of the glacier, with a snowy ridge along the back. Dark volcanic rock with orange lichen, and snow in ragged patches on flatter and higher ground (not everywhere).
- At the back right, a low peninsula with an Adélie penguin rookery: an organic, irregular patch of round pebbles stained pink with krill, with pebble-ring nests. Behind it, a small research station (red and yellow huts on stilts, fuel drums, a radio mast with guy wires, a flag, a turning anemometer, a snowmobile) and a timber quay.
- A ragged skerry of two low rocks off to the front right, where Weddell seals haul out.
- The sea floor is grey gravel with shells, sponges, sea stars and swaying anemones, visible through the clear jelly front face.
- The cut faces of the block show candy-coloured strata, dark basalt columns under the land, and layered blue glacier ice with a dirty basal layer under the glacier.

PHYSICS
- Shallow-water simulation on a ~168² grid for the bay: waves, wakes, foam, refraction, caustics on the floor, light shafts, and absorption that depends on the flavour.
- Every piece of ice is a rigid body: tabular, dome, pinnacle and wedge bergs, growlers, pancake floes, and glacier slabs. Each is a star-shaped faceted mesh (superellipsoid plus lobes plus two octaves of noise), a lattice of mass points for buoyancy and drag, and contact spheres for ground, walls, each other and the ship. Settle stable poses at load so nothing capsizes at the start.
- Calving: three slabs stand along the cliff. About once a minute (or on demand) one breaks off with a crack, a puff of ice dust, a splash, spray and a wave, then capsizes until it finds a stable way up. The glacier slowly pushes a new slab out. Old slabs melt away.
- The displaced water is handed back to the waves without feedback: wakes only when a piece moves fast, splashes when it plunges in. Slow drift makes no waves.
- The jelly block itself wobbles, shears and squashes, and can be tipped by dragging its side.

LIFE
- An icebreaker, "Polaris" (red hull with a spoon bow, white superstructure, yellow funnel with smoke, a turning radar, a helideck), lies at the quay. Now and then (or on demand) she casts off, shoulders round the bay through the pack, pushing floes and bergs aside, and comes back alongside. A status line shows Alongside / Casting off / Under way / Breaking ice / Coming alongside, with a countdown or progress.
- 22 Adélie penguins: blue-black backs, white shirt fronts, white eye rings, pink feet. They stand on nests and look about, have the odd ecstatic display, waddle or toboggan to the beach, dive in, "fly" underwater with beating flippers, porpoise, leap out onto floes and bergs, and slide off when a floe tips. They chase silverfish and thrown fish.
- 3 Weddell seals (spotted grey) haul out on the skerry and floes, lift their heads, and go for swims.
- An orca (proper eye patch and grey saddle) patrols deep water, surfaces to blow and dives. Penguins keep clear of it.
- Schools of silverfish; gentle snowfall.

UI (same layout as the rest of the series)
Masthead "Material Studies / Iceberg Jelly." with a one-line description. A "WebGPU · Live" status pill. A glass control panel on the right that turns into a bottom sheet on mobile:
- Buttons: Calve (shows "Wait…" while no slab is ready), Cast off / Full ahead, Throw fish, Horn (Space).
- A water-energy meter; tallies for Calved, Capsized, Fed; the ship status line.
- Flavours: Glacier mint, Blue raspberry, Blackberry. Each changes the water's absorption, its tint and the strata.
- Sliders: Firmness, Wave damping, Snowfall.
- Reset, Pause, Sound on/off, View.
- A "How to play" footer.
Interaction: pick up and throw floes and bergs; drag across the water to make waves; drag the ground or the side of the block to tip it; drag empty space or right-drag to orbit; scroll or pinch to zoom.

Web Audio sounds: calving crack and rumble, splashes, a capsizing groan, ice knocking on the hull, a deep two-reed ship's horn, penguin plops, and wind that rises with the snowfall.

Show a fallback screen when WebGPU is unavailable. Respect prefers-reduced-motion. No network requests.

QUALITY BAR
Low-poly faceted ice with chalky snowy tops, glassy blue underwater parts, blue bands, sparkles and translucency. Soft shadows. Cool polar light. Performance around 60 fps on a laptop. Test headlessly: no NaNs over long soaks, a calm start, calving plus capsize, a full ship round trip, feeding, picking up ice, the mobile sheet, and no console errors.
Deliver the HTML file and publish it as an artifact.
```

---

## 提示词（中文）

构建 "Iceberg Jelly"（冰山果冻）——我的 "Material Studies" 果冻微缩场景系列的下一件作品：一个使用 WebGPU（WGSL）的单文件自包含 HTML，无外部库，界面为英文。

### 场景

一块方形果冻（5.2 × 5.2 单位），立在浅色、冷灰调的纸质摄影棚背景上，地面有柔和阴影。里面是一个极地海湾：

- 左后方，一条冰川沿锯齿状群山之间的山谷流下，末端是立在深水中的冰崖。冰崖上有竖直的沟槽和蓝色条带。冰川表面沿边缘有人字形冰裂缝，靠近前端有横向裂缝和冰塔（seracs），还有灰色的侧碛。冰舌两侧是冰碛堤，所以只有它的前端立在水中。
- 山脉：冰川左侧是一列尖峰，右侧是一道山脊支脉，后方是一条积雪的山脊。深色火山岩带橙色地衣，雪呈不规则斑块状分布在较平坦和较高的地方（不是到处都有）。
- 右后方，一个低矮的半岛上有阿德利企鹅繁殖地：一片有机、不规则的圆卵石区域，被磷虾染成粉色，有卵石围成的巢。它后面是一个小科考站（高脚柱上的红黄小屋、燃料桶、带拉线的无线电天线杆、一面旗、旋转的风速计、一辆雪地摩托）和一座木码头。
- 右前方是由两块低矮礁石组成的参差小礁（skerry），威德尔海豹在那里上岸。
- 海底是灰色砾石，有贝壳、海绵、海星和摇曳的海葵，透过清澈的果冻正面可见。
- 块的切面露出糖果色地层、陆地下方的深色玄武岩柱，以及冰川下方分层的蓝色冰川冰和脏污的底层。

### 物理

- 海湾用约 168² 网格的浅水模拟：波浪、尾迹、泡沫、折射、底面焦散、光柱，以及取决于口味的吸收。
- 每块冰都是刚体：平顶冰山、穹顶冰山、尖塔冰山和楔形冰山、小冰块（growlers）、饼状浮冰，以及冰川冰板。每块都是星形的多面网格（超椭球 + 瓣 + 两个倍频程的噪声），一个用于浮力和阻力的质点晶格，以及用于与地面、墙壁、彼此和船碰撞的接触球。加载时把它们稳定到平衡姿态，这样开场时不会有东西翻倒。
- 崩解（calving）：冰崖上立着三块冰板。大约每分钟一次（或按需），其中一块伴随一声爆裂、一团冰尘、水花、飞沫和一道波浪断裂下来，然后翻滚，直到找到稳定的朝上姿态。冰川会慢慢推出一块新冰板。旧冰板会逐渐融化消失。
- 排开的水无反馈地还给波浪：只有冰块快速移动时才有尾迹，冲入水中时才有水花。缓慢漂移不产生波浪。
- 果冻块本身会晃动、剪切和压扁，并可通过拖动其侧面使其倾斜。

### 生命

- 一艘破冰船 "Polaris"（勺形船首的红色船体、白色上层建筑、冒烟的黄色烟囱、旋转的雷达、直升机甲板）停靠在码头。不时（或按需）她会解缆，在浮冰群中挤开一条路绕海湾一圈，把浮冰和冰山推开，然后回来靠泊。一行状态显示 Alongside / Casting off / Under way / Breaking ice / Coming alongside，并带倒计时或进度。
- 22 只阿德利企鹅：蓝黑色背部、白色"衬衫"前胸、白眼圈、粉色脚。它们站在巢上东张西望，偶尔做出狂喜的求偶展示，摇摇摆摆走或用肚子滑到海滩，跳入水中，在水下拍着鳍状翅膀"飞行"，做海豚式跃水，跳到浮冰和冰山上，浮冰倾斜时滑下去。它们追逐银鱼和扔进来的鱼。
- 3 只威德尔海豹（灰色带斑点）在小礁和浮冰上上岸，抬起头，然后下水游一圈。
- 一头虎鲸（正确的眼斑和灰色鞍斑）在深水巡游，浮上水面喷气再下潜。企鹅会躲开它。
- 银鱼群；轻柔的降雪。

### UI（与系列其他作品布局相同）

刊头 "Material Studies / Iceberg Jelly."，配一行描述。一个 "WebGPU · Live" 状态胶囊。右侧一个玻璃控制面板，在移动端变为底部抽屉：
- 按钮：Calve（崩解；没有冰板就绪时显示 "Wait…"）、Cast off / Full ahead（解缆 / 全速前进）、Throw fish（扔鱼）、Horn（汽笛，空格键）。
- 一个水能量仪表；Calved、Capsized、Fed（崩解、翻覆、喂食）计数；船舶状态行。
- 口味：Glacier mint（冰川薄荷）、Blue raspberry（蓝树莓）、Blackberry（黑莓）。每种都会改变水的吸收、色调和地层。
- 滑块：Firmness、Wave damping、Snowfall（降雪）。
- Reset、Pause、Sound on/off、View。
- 一个 "How to play" 页脚。

交互：捡起并扔出浮冰和冰山；在水面拖动造浪；拖动地面或块的侧面使其倾斜；拖动空白处或右键拖动环绕视角；滚轮或双指缩放。

Web Audio 音效：崩解的爆裂声和隆隆声、水花声、翻覆时的呻吟声、冰块撞击船体的声音、低沉的双簧片船笛、企鹅入水的扑通声，以及随降雪增强的风声。

WebGPU 不可用时显示降级页面。遵守 prefers-reduced-motion。无网络请求。

### 质量标准

低多边形多面冰体，顶部是粉笔质感的积雪，水下部分是玻璃般的蓝色，有蓝色条带、闪光和半透明感。柔和阴影。冷色调的极地光线。在笔记本上约 60 fps。无头测试：长时间运行不出现 NaN，开场平静，崩解加翻覆，船完整往返一次，喂食，捡起冰块，移动端抽屉，无控制台报错。

交付 HTML 文件并将其发布为 artifact。
