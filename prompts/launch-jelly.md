# 发射果冻 Launch Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `航天发射场` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 · GPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2114132632166347208) · [提示词帖](https://x.com/vib3coded/status/2114132746645688569) · 2026-10-25（北京时间） · 试玩：[Claude Opus 5.5](https://claude.ai/artifact/55k4Wc38FV3deVaAtQ6adE) · [ChatGPT-6 Astra](https://launch-jelly-vibecoded1.vercel.app)

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（测试模型见上）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![发射果冻 Launch Jelly](../assets/launch-jelly.jpg)

## 提示词（中文）

构建 "Launch Jelly"（发射果冻）—— "Material Studies" 系列里的一个单文件交互式 WebGPU 微缩场景：低矮热带小岛上的航天发射场，被切成一块半透明果冻立方体，放在摄影棚的地面上。一切都是程序化的（没有外部资源，也没有网络请求），一个 HTML 文件，内联 JS 和 WGSL。

### 果冻块

- 一块会晃的果冻立方体。可以抓住它的侧面把它扳斜，松手后它会弹回来。滑块：firmness（硬度）、wave damping（波浪阻尼）、wind（风，0–20 m/s）。
- 海水是浅水模拟（风浪、尾迹、泡沫），沙质海底有沙纹和焦散，海草、珊瑚头、海绵、海星、海螺，海底还有一只旧火箭发动机喷管。切面露出沙子、含壳石灰岩和糖果一样的岩层。在水面上拖动会把浪搅起来。

### 场景

- 后方和左侧是陆地：沙丘、灌丛、棕榈、沙丘草、海滩。
- 混凝土护堤上的发射台：座架架在朝海开口的火焰壕沟上，钢制导流板，四根红白相间的避雷桅杆，挂着下垂的悬链线，还有一座消防水塔、储罐区（液氧球罐、煤油罐、氮气瓶）和泛光灯。
- 一座长机库，波纹墙面，垂直提升大门；通向发射台的轨道；一辆运输起竖车（白色桁架强背装在带液压推杆的轨道车上）。
- 着陆区（带圆环和十字的混凝土圆）、翻修棚、消防车，以及一台会跟着飞行物转的跟踪雷达。
- 媒体区：挤满观众的看台、一面旗，还有一块琥珀色七段数码倒计时时钟（T−0:10 … T+0:45）。
- 码头带护舷和系船柱，一台长桁架臂履带吊，两个助推器支架，一座仓库。
- 海上：一艘无人船（深色甲板带着陆靶、防爆墙、推进器舱）、一艘拖船，以及一艘带四臂大网的整流罩回收船。
- 火箭：两级——助推器九台发动机、黑色级间段、四条折叠着陆腿、四片栅格舵；上面级带长而暗的真空喷管；两瓣整流罩各自带翼伞。

### 会发生什么

- Roll out（滚出）：机库门升起，起竖车把火箭水平运出并竖到座架上；火箭喷出液氧白雾。
- Launch（发射）：十秒倒计时带蜂鸣和时钟，强背后仰，消防水喷出，T−3 点火，巨大蒸汽云从壕沟涌向海面，缓慢离地，果冻块颤抖，观众欢呼，海鸥起飞。火箭向航区俯仰爬升，拖着翻滚的尾烟飞出视野；相机跟着升起。
- Staging（级间分离）：主发动机关机（MECO）、分离，上面级点亮淡蓝紫色真空火焰离去。助推器翻转，回飞燃烧，栅格舵展开，再入燃烧，导引下降，单发着陆燃烧，腿甩出，触地——落在无人船上或回着陆区（可切换，或点船/点着陆区）。双重音爆（回着陆区是三重）。助推器回来时带着烟灰；甲板和着陆区被烤焦。
- Recovery（回收）：拖船把无人船拖回码头；吊车钩住助推器提起（会像摆锤一样晃），收起腿，放到支架上；船再被拖出去。整流罩两半在橙白翼伞下盘旋落下：一半落入船网，另一半溅水后被捞起；船把它们带回。
- Reuse（复用）：下一次滚出用的是飞过的助推器（"B1 · flight 2"，烟灰部分擦掉）。
- Storm（风暴）：风、浪、雨，房间变暗，闪电打在桅杆、吊车或海面上。风暴中或风速超过 15 m/s 时禁止发射（"No go · weather / wind"）；进行中的倒计时会保持（hold）。

### 生命

棕鹈鹕盘旋并俯冲捉鱼；海鸥停在桅杆、灯和屋顶上；一群宽吻海豚；海牛在浅滩啃草并浮出水面换气；鱼群；海月水母；倒计时前离开的发射台船员、码头上的工人，以及在起飞和着陆时举手欢呼的观众。

### 渲染

发动机羽流是发光的半透明锥体（白热核心、橙色、下方有激波钻石，在稀薄空气中变宽并转成蓝紫色），照亮地面、烟雾和火箭；蒸汽和尾气是柔和的发光团；飞过的助推器有烟灰条纹；还有阴影、折射和焦散。

### 控制与界面

- 按钮：Roll out、Launch（倒计时中变为 Hold）、Land on ship / Land at pad、Storm。空格 = 滚出 / 发射。点击：火箭 = 发射，机库 = 滚出，无人船 / 着陆区 = 选择着陆点。
- 计数：Launches、Landings、Fairings；火箭（T−/T+ 时间线：Liftoff、Max Q、Stage separation、Boostback、Entry burn、Landing burn…）、无人船和整流罩回收船各有一行状态。
- Flavours（果冻配色）：Lime、Curaçao、Blackcurrant。声音开关、暂停、重置、视角。
- 所有声音用 WebAudio 合成，只在事件发生时响（门电机、液压、倒计时蜂鸣、燃烧中的发动机轰鸣循环、音爆、触地闷响、拖船汽笛、绞车、入网、雷）——没有一直循环的背景环境音。
- 手机上：控制放在底部抽屉里，触摸环绕，双指缩放。没有 WebGPU 时给出降级提示。
- 英文文案："Launch Jelly. A spaceport on a low island, its rockets flying and coming home, set in a block of jelly." —— "Roll it out. Light it up. Bring the booster home."

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Launch Jelly" — a single-file interactive WebGPU diorama in the "Material Studies" series: a spaceport on a low tropical island, cut out as a cube of translucent jelly on a studio floor. Everything procedural (no external assets, no network), one HTML file with inline JS/WGSL.

THE BLOCK
- A wobbly jelly cube you can grab by its sides and tip; it springs back. Sliders: firmness, wave damping, wind (0–20 m/s).
- Shallow-water sim for the sea (wind waves, wakes, foam), sandy seabed with ripples and caustics, seagrass, coral heads, sponges, starfish, conchs, an old rocket engine bell on the bottom. Cut faces show sand, shelly limestone and candy strata. Drag the water to stir it.

THE SCENE
- Land along the back and left: dunes, scrub, palms, dune grass, a beach.
- Launch pad on a concrete berm: mount over a flame trench opening toward the sea, steel deflector, four red-and-white lightning masts with sagging catenary wires, a deluge water tower, tank farm (LOX sphere, kerosene tanks, nitrogen bottles), floodlights.
- A long hangar with ribbed siding and a vertical-lift door, rails to the pad, a transporter-erector (white lattice strongback on a rail car with hydraulic rams).
- Landing zone (concrete circle with ring and cross), refurbishment shed, fire truck, a tracking radar dish that follows whatever is flying.
- Press site: bleachers full of spectators, a flag, a big amber seven-segment countdown clock (T−0:10 … T+0:45).
- Quay with fenders and bollards, a crawler crane with a long lattice boom, two booster stands, a warehouse.
- At sea: a drone ship (dark deck with landing target, blast walls, thruster houses), a tug, a fairing-recovery boat with a big net on four arms.
- The rocket: two stages — booster with nine engines, black interstage, four folding landing legs, four grid fins; upper stage with a long dark vacuum nozzle; a two-piece fairing whose halves carry parafoils.

WHAT HAPPENS
- Roll out: the hangar door lifts, the erector carries the rocket out horizontally on rails and stands it on the mount; it vents LOX wisps.
- Launch: 10-second count with beeps and the clock, strongback leans back, deluge water, ignition at T−3 with huge steam clouds boiling out of the trench toward the sea, slow liftoff, the block trembles, the crowd cheers, gulls go up. The rocket pitches downrange and climbs out of sight leaving a billowing exhaust trail; the camera rises with it.
- Staging: MECO, separation, the upper stage lights a pale blue-violet vacuum flame and leaves. The booster flips, boostback burn, grid fins out, entry burn, steers down, landing burn on one engine, legs swing out, touchdown — on the drone ship or back at the landing zone (toggle, or tap the ship / the pad). Double sonic boom (triple for the landing zone). Boosters come back sooty; the deck and pad get scorched.
- Recovery: the tug tows the drone ship to the quay; the crane hooks the booster, lifts it (pendulum swing), folds its legs, sets it on a stand; the ship is towed back out. Fairing halves come down under orange-and-white parafoils, circling in: one lands in the boat's net, the other splashes and is fished out; the boat brings them home.
- Reuse: the next rollout takes a flight-proven booster ("B1 · flight 2", soot partly cleaned).
- Storm: wind, waves, rain, darkened room, lightning on the masts, the crane or the sea. No launches in a storm or above 15 m/s ("No go · weather / wind"); a count in progress holds.

LIFE
- Brown pelicans that circle and plunge-dive for fish, gulls on masts, lamps and roofs, a pod of bottlenose dolphins, manatees grazing the shallows and surfacing to breathe, fish schools, moon jellies; pad crew who leave before the count, hands on the quay, spectators who raise their arms at liftoff and landing.

RENDERING
- Engine plumes as glowing translucent cones (white-hot core, orange, shock diamonds low down, widening and turning blue-violet in thin air) that light the ground, the smoke and the rocket orange; steam and exhaust as soft lit puffs; soot streaks on flown boosters; shadows, refraction, caustics.

CONTROLS & UI
- Buttons: Roll out, Launch (Hold during the count), Land on ship / Land at pad, Storm. Space rolls out / launches. Taps: rocket = launch, hangar = roll out, drone ship / landing zone = choose landing site.
- Tallies: Launches, Landings, Fairings; status lines for the Rocket (T−/T+ timeline: Liftoff, Max Q, Stage separation, Boostback, Entry burn, Landing burn…), the Drone ship and the Fairing boat.
- Flavours: Lime, Curaçao, Blackcurrant. Sound toggle, pause, reset, view.
- All sounds synthesised with WebAudio, only for events (door motor, hydraulics, countdown beeps, engine roar loop while burning, sonic booms, touchdown thud, tug horn, winch, net catch, thunder) — no background ambience.
- Mobile bottom sheet, touch orbit, pinch zoom; a fallback message without WebGPU.
- Copy: "Launch Jelly. A spaceport on a low island, its rockets flying and coming home, set in a block of jelly." — "Roll it out. Light it up. Bring the booster home."
```

</details>
