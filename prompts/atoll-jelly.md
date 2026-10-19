# 环礁果冻 Atoll Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · boids · 单文件 HTML
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `boids` `水上飞机` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2107977531726934288) · [提示词帖](https://x.com/vib3coded/status/2107977713415864782) · 2026-10-08（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。提示词里提到的「Island Jelly」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "Atoll Jelly"——一个自包含 HTML 文件，原生 WebGPU + WGSL，模拟用纯 JS，无外部请求。它是编辑风格 "MATERIAL STUDIES" 交互式果冻微缩场景系列的一员：一块方形切开的松石绿果冻泻湖，位于马尔代夫，有一座棕榈小岛、一条连着水上屋的栈桥、一架按自己日程运行的水上飞机，果冻下方还有珊瑚礁生物。

### 页面

暖色纸张（#ece9e3），墨色 #241f1d，强调色 #12a2a6，斜体衬线 H1 "Atoll / Jelly."，眉标 "MATERIAL STUDIES"，说明文字 "Six bungalows on stilts, a seaplane that comes and goes, and eagle rays gliding through the jelly below."。状态胶囊 "WEBGPU · LIVE"。右侧玻璃面板："THE LAGOON" 下有三个深色按钮 "Seaplane"（水上飞机）、"Feed the fish"（喂鱼）、"Float ring"（游泳圈），一条细仪表，计数 "Landings · Fed · Afloat"（降落 · 喂食 · 漂浮）；"FLAVOUR" 色板 Turquoise / Sapphire / Lime；滑块 Firmness、Wave damping、Tide（±10 cm）；Reset · Pause · Reset view。左下 "HOW TO PLAY"："Stir the lagoon. Feed the fish. Wave the seaplane off." + 一行灰色的手势说明。移动端底部抽屉、触摸环绕/双指缩放、WebGPU 降级卡片、页面不滚动、控制台无报错。

### 场景（块 5.2²，海平面 1.3）

白沙泻湖约 0.3 深，在前方转角附近倾斜进一个深"蓝洞"；八个珊瑚头（凸起），装饰着脑珊瑚、枝状珊瑚和海扇，颜色有粉/紫/橙/黄/青，轻微摇摆；左后角是一座沙质小岛（沙滩环、低矮的林木丘、软糖灌木、两把茅草遮阳伞配躺椅），岛上有 8 棵茂密的椰子树（每棵 16 片拱形羽状叶 + 下垂的干叶）；一座开放式大堂亭，顶着巨大的茅草四坡屋顶。一条架在细高脚桩上的木板栈桥从小岛斜穿泻湖，配矮灯柱；五座水上屋交替挂在栈桥两侧，末端还有一座更大的：高脚桩上的木板平台，浅色木屋带朝海的玻璃门，茅草四坡屋顶（带状稻草纹理），小泳池，两张躺椅，一把下水的钢梯。一个漂浮的水上飞机浮台，带一个小茅草遮阳棚，用一条高脚步道连到小岛南侧海滩。块的切面在半透明果冻墙下呈现糖果地层（沙、贝壳带、焦糖、巧克力）。

### 水（同 "Island Jelly"）

线性浅水模拟（168² 交错网格，120 Hz，√(g·depth) 波速，小表面张力，阻尼），手指搅动，块倾斜与晃荡，漂浮物把排开的体积还给海，水花坑 + 气泡，泡沫场（会消退并呈蕾丝状的白水），焦散，光柱，折射，按口味的 Beer–Lambert 吸收，岸线蕾丝泡沫。

### 水上飞机

双发浮筒水上飞机：白色机身带青色腰线，上单翼配青色翼尖，支柱，双浮筒，3 叶螺旋桨在顶点着色器中旋转。固定的每日循环——在浮台等待 → 在浮筒上原地转 180° → 滑出 → 起飞滑跑（水花）→ 爬升 → 在约 3.1 高度绕微缩场景飞一圈跑道航线并带倾斜转弯 → 进近 → 接水（水花坑、白水和一次颠簸）→ 着陆滑跑 → 转弯 → 滑回浮台。在水面上它随果冻起伏：四个浮筒采样点决定高度、俯仰和横滚；浮筒把体积推进模拟（尾迹）并产生泡沫。"Seaplane" 按钮：若在等待则立即出发，若在飞行则加快航线提前降落。统计降落次数。

### 珊瑚礁生物

42 条 boids 鱼，分四种颜色（黄高鳍刺尾鱼、蓝身黄尾、黑白条纹、橙身白条），与同类结群，四处游荡，始终保持在水中（不碰底、在水面下、离开浅滩、在块内），尾巴在顶点着色器中摆动；3 条斑点鹞鲼在海底附近滑翔，翅膀波浪式拍动，鞭状尾巴。水中的手指、任何水花或水上飞机掠过的浮筒都会把它们惊散。"Feed the fish" 撒下 16 粒饲料，先漂浮后下沉；鱼和鳐鱼会游过来吃掉它们（计入 Fed）。

### 游泳圈

糖果条纹充气游泳圈（粉 / 橙 / 蓝配白）——轻，浮得高，平躺在波浪上，有阻尼所以永远不会弹出果冻，会被水上飞机推开；可以捡起来扔；也能落在平台和海滩上。

### QA

钩子 window.__aj；检查：完整的水上飞机循环和一次降落、高度 > 2.8、浮筒贴着水面、接水泡沫 + 波浪、鱼始终在水中、喂食能引来鱼并被吃掉、手指能惊散鱼群、游泳圈平浮、搅动产生的波浪会平息、倾斜后晃荡并恢复、口味/滑块/暂停/环绕/缩放、压力测试、模拟 < 5 ms、无网络请求、无报错、移动端、降级。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Atoll Jelly" — one self-contained HTML file, native WebGPU + WGSL, sim in plain JS, no external requests. An entry in the editorial "MATERIAL STUDIES" series of interactive jelly dioramas: a square cut-out block of turquoise jelly lagoon in the Maldives with a palm islet, a jetty of overwater bungalows, a seaplane that runs its own day, and reef life under the jelly.

PAGE: warm paper (#ece9e3), ink #241f1d, accent #12a2a6, italic serif H1 "Atoll / Jelly.", eyebrow "MATERIAL STUDIES", caption "Six bungalows on stilts, a seaplane that comes and goes, and eagle rays gliding through the jelly below." Status pill "WEBGPU · LIVE". Right glass panel: "THE LAGOON" with three dark buttons "Seaplane", "Feed the fish", "Float ring", a thin meter, tally "Landings · Fed · Afloat"; "FLAVOUR" swatches Turquoise / Sapphire / Lime; sliders Firmness, Wave damping, Tide (±10 cm); Reset · Pause · Reset view. Bottom-left "HOW TO PLAY": "Stir the lagoon. Feed the fish. Wave the seaplane off." + one grey line of gestures. Mobile bottom sheet, touch orbit/pinch, WebGPU fallback card, no scroll, no console errors.

SCENE (block 5.2², sea level 1.3): white-sand lagoon ~0.3 deep sloping into a deep "blue hole" near the front corner; eight coral heads (bumps) dressed with brain corals, branching corals and sea fans in pink/purple/orange/yellow/teal that sway slightly; a sandy islet in the back-left corner (beach ring, low wooded hump, gummy shrubs, two thatched parasols with loungers) with 8 lush coconut palms (16 arching pinnate fronds each + dry hanging fronds); an open lobby pavilion under a big hipped thatch roof. A plank jetty on thin stilts runs from the islet diagonally across the lagoon with low lamp posts; five bungalows hang off it on alternating sides plus a larger one at the end: plank decks on stilts, pale timber huts with glass doors to the sea, hipped thatched roofs (banded straw texture), plunge pool, two loungers, a steel ladder into the water. A floating seaplane pontoon with a tiny thatched shade, linked to the islet's south beach by a stilted walk. Block cut faces show candy strata (sand, shell band, caramel, chocolate) under translucent jelly walls.

WATER (as "Island Jelly"): linear shallow-water sim (168² staggered grid, 120 Hz, √(g·depth) wave speed, small surface tension, damping), finger stirring, block tilting with slosh, floating bodies hand displaced volume back to the sea, splash craters + bubbles, a foam field (white water that fades and laces), caustics, light shafts, refraction, Beer–Lambert flavour absorption, shoreline lace.

SEAPLANE (twin-engine floatplane: white with teal cheatline, high wing with teal tips, struts, twin floats, 3-bladed propellers spinning in the vertex shader): a fixed daily loop — wait at the pontoon → pivot 180° on its floats → taxi out → take-off run (spray) → climb → a racetrack circuit around the diorama at ~3.1 height with banking → approach → touchdown with crater, white water and a jolt → landing run → turn → taxi back to the pontoon. On water it rides the jelly: four float samples set height, pitch and roll; its floats push volume into the sim (wake) and foam. "Seaplane" button: leave now if waiting, or hurry the circuit to land early. Counts landings.

REEF LIFE: 42 boids fish in four colour kinds (yellow tang, blue with yellow tail, black-white banded, orange with white bars), schooling with their own kind, wandering, kept in the water (off the floor, under the surface, out of the shallows, inside the block), tails beating in the vertex shader; 3 spotted eagle rays gliding near the floor with wave-flapping wings and whip tails. A finger in the water, any splash, or the seaplane's floats rushing by scatter them. "Feed the fish" scatters 16 pellets that float, then sink; fish and rays home in and eat them (counted as Fed).

FLOAT RINGS: inflatable candy-striped rings (pink / orange / blue with white) — light, float high, lie flat on the waves, damped so they never pop out of the jelly, shoved aside by the seaplane; pick up and throw; land on decks and beach too.

QA: hook window.__aj; checks for the full seaplane cycle and one landing, altitude > 2.8, floats riding the surface, touchdown foam + waves, fish always in water, feeding brings fish and gets eaten, a finger scatters a school, rings float flat, stirring makes waves that die down, tilt sloshes and settles, flavours/sliders/pause/orbit/zoom, stress, sim < 5 ms, no network, no errors, mobile, fallback.
```

</details>
