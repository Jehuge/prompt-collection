# 离岸果冻 Offshore Jelly

- **类型**：交互网页 / 果冻微缩场景
- **技术栈**：WebGPU · WGSL · 浅水模拟 · 单文件 HTML
- **标签**：`webgpu` `wgsl` `浅水模拟` `果冻` `海上平台` `风力发电` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2113401221910253853) · [提示词帖](https://x.com/vib3coded/status/2113401353196466400) · 2026-10-22（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![离岸果冻 Offshore Jelly](../assets/offshore-jelly.jpg)

## 提示词（中文）

构建 "Offshore Jelly"（离岸果冻）—— "Material Studies" 系列里的一个单文件交互式 WebGPU 微缩场景：从北海切出一块半透明果冻立方体，放在摄影棚的地面上。一切都是程序化的（没有外部资源，也没有网络请求），一个 HTML 文件，内联 JS 和 WGSL。

### 果冻块

- 一块会晃的果冻立方体。可以抓住它的侧面把它扳斜，松手后它会弹回来。滑块：firmness（硬度）、damping（阻尼）、wind（风，0–20 m/s）。
- 内部：海面是浅水模拟（波浪、尾迹、泡沫、白浪）。海底有沙纹、冲刷出来的岩石、海带、巨石、海星、螃蟹、海胆、一条管线、缆绳，以及一艘小沉船。海底有焦散。在水面上拖动会把浪搅起来。
- 浪来自风：几列波列，波高随风速变大。

### 场景

- 一座生产平台，站在四条腿的钢导管架上（斜撑、立管、导管、靠船件，水线以下有海生物附着）：主甲板和底层甲板、工艺模块、井架、生活区、救生艇、一台带堆场的座式起重机，以及一根放空臂，火焰闪烁并冒烟。
- 八角形直升机甲板，上面有一个 H、一张网、一圈周边灯和一个风向袋。
- 五台单桩海上风机：过渡段带黄色平台、靠船爬梯、吊柱、塔筒、机舱、叶尖涂红的三叶片叶轮，以及闪烁的红色航空灯。叶轮转速和出力（MW）跟着风走。
- 一块岩石小岛（skerry），上面一座灯塔的光束在转；海豹爬上来休息。

### 会发生什么

- Supply run（补给）：一艘平台供应船从待命位置驶来，靠动力定位停在导管架旁边（推进器打出泡沫）。起重机做四次吊装——集装箱在吊钩上摆动，放到平台上，再回装到船的甲板上。然后她驶回待命位置。
- Helicopter（直升机）：从西边飞来，转向迎风，降落在直升机甲板；一名甲板军官走出来；乘客下机。再按一次就让它离开（旋翼加速、升空、飞走）。主旋翼和尾桨都在转，下洗气流把水面压平。
- Crew boat（船员交通船）：一艘小双体船驶向一台风机，把船首顶到靠船件上，技术人员顺着梯子爬上平台。下一次她把人接走，送回去。
- Storm（风暴）：风加到大风，浪变高，带着白浪和飞沫，下雨，房间变暗。闪电打在叶片、灯塔、井架或海面上，有闪光也有雷声。风速超过切出（cut-out）后，风机顺桨停转（0 MW）；直升机停飞。然后风减弱，风机重新转起来。

### 生命

导管架和沉船周围有鱼群。海鸥停在栏杆上，汽笛一响就起飞。塘鹅俯冲捉鱼。还有一群鼠海豚、海豹、海月水母，以及在甲板上走动的船员。

### 控制与界面

- 按钮：Supply run、Helicopter（已经降落时变为起飞）、Crew boat、Storm。空格 = 船的汽笛。点一台风机可以开关它；点供应船或直升机甲板会把它们叫来。拖动环绕视角，滚轮或双指缩放。
- 计数：Power (MW)、Lifts、Flights。供应船、直升机和船员交通船各有一行状态。
- Flavours（果冻配色）：North Sea、Curaçao、Blackcurrant。
- 声音用 WebAudio 合成，只在事件发生时响（汽笛、绞车、放下、碰撞、旋翼、雷、雨）——没有一直循环的背景环境音。有声音开关，也可以暂停。
- 手机上：控制放在底部抽屉里，触摸环绕，双指缩放。没有 WebGPU 时给出一句清楚的降级提示。
- 英文文案："Offshore Jelly. A wind farm and a platform working a stretch of North Sea, set in a block of jelly." —— "Call in the supply boat. Fly the crew out. Brew up a storm."

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Offshore Jelly" — a single-file interactive WebGPU diorama in the "Material Studies" series: a stretch of North Sea cut out as a cube of translucent jelly, sitting on a studio floor. Everything is procedural (no external assets, no network), one HTML file with inline JS/WGSL.

THE BLOCK
- A wobbly jelly cube you can grab by its sides and tip; it springs back. Sliders: firmness, damping, wind (0–20 m/s).
- Inside: a shallow-water simulation for the sea surface (waves, wakes, foam, whitecaps), seabed with sand ripples, scour rocks, kelp, boulders, starfish, crabs, urchins, a pipeline, cables and a small wreck. Caustics on the seabed. Dragging the water stirs up waves.
- Waves come from the wind: several wave trains whose height grows with wind speed.

THE SCENE
- A production platform on a four-legged steel jacket (braces, risers, conductors, boat landing, marine growth below the waterline): main and cellar decks, process module, derrick, living quarters, lifeboats, a pedestal crane with a laydown area, a flare boom with a flickering flame and smoke.
- An octagonal helideck with an H, a net, perimeter lights and a windsock.
- Five offshore wind turbines on monopiles: transition piece with yellow platform, boat landing ladder, davit, tower, nacelle, three-blade rotors with red tips, blinking red aviation lights. Rotor speed and power output (MW) follow the wind.
- A rocky skerry with a lighthouse whose beam turns; seals haul out on it.

WHAT HAPPENS
- Supply run: a platform supply vessel comes in from standby, holds station next to the jacket on dynamic positioning (thruster foam), and the crane does four lifts — containers swing on the hook, are set down on the platform and back-loaded onto the boat's deck. Then she sails back to standby.
- Helicopter: flies in from the west, turns into the wind, lands on the helideck; a deck officer walks out; passengers get off. A second press sends it away (spin-up, lift, outbound). Rotor and tail rotor spin, downwash flattens the water.
- Crew boat: a small catamaran sails out to a turbine, pushes its bow onto the boat landing, and technicians climb the ladder onto the platform. Next time she picks them up and brings them home.
- Storm: the wind builds to a gale, waves get big with whitecaps and spray, rain falls, the room darkens, lightning strikes blades, the lighthouse, the derrick or the sea with a flash and thunder. Above cut-out the turbines feather their blades and stop (0 MW); the helicopter is grounded. Then it eases and the turbines restart.

LIFE
- Schools of fish around the jacket and wrecks, gulls that perch on railings and take off on the horn, gannets that plunge-dive for fish, a pod of porpoises, seals, moon jellyfish, crew walking the decks.

CONTROLS & UI
- Buttons: Supply run, Helicopter (take-off when landed), Crew boat, Storm. Space = ship's horn. Tapping a turbine switches it on/off, tapping the supply boat or helideck calls them. Orbit by drag, zoom by wheel/pinch.
- Tallies: Power (MW), Lifts, Flights; status lines for the supply boat, helicopter and crew boat.
- Flavours (jelly colour palettes): North Sea, Curaçao, Blackcurrant.
- Sounds are synthesised with WebAudio and only play for events (horn, winch, set-down, bump, rotor, thunder, rain) — no constant background ambience. Sound toggle and pause.
- Mobile: a bottom sheet with the controls, touch orbit and pinch zoom. Clean fallback message when WebGPU is unavailable.
- Copy in English: "Offshore Jelly. A wind farm and a platform working a stretch of North Sea, set in a block of jelly." — "Call in the supply boat. Fly the crew out. Brew up a storm."
```

</details>
