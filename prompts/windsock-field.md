# 风向袋机场 Windsock Field

- **类型**：交互网页 / 像素风场景
- **技术栈**：three.js r160 · 像素后处理 · 飞行物理 · 单文件 HTML
- **标签**：`three.js` `像素风` `机场` `飞行物理` `vibe-coding` `ai-测试`
- **测试模型**：Kimi K3.1 Pro · ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2113849897438834851) · [提示词帖](https://x.com/vib3coded/status/2113850194106167681) · 2026-10-24（北京时间） · 试玩：[Kimi K3.1 Pro](https://okilzeg5izz3y.kimi.page)

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（测试模型见上）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![风向袋机场 Windsock Field](../assets/windsock-field.jpg)

## 提示词（中文）

构建一个单文件 HTML + three.js（r160，从 jsDelivr 用 import map）交互式像素风微缩场景，名叫 "Windsock Field"（风向袋机场）：漂浮圆角矩形小岛上的小型机场，正交等距相机渲染到低分辨率目标（约 480×300），再用 texelFetch 放大，带深度描边、OKLab 量化到固定 64 色调色板、可选 Bayer 抖动，以及带 MSAA 的 "Raw 3D" 开关。一切由方块搭成；没有外部资源，也没有真实品牌。

布局：前方是 09/27 跑道（边灯、入口条、漆出的号码、中线、瞄准点、PAPI、顺序进近灯），平行的单车道滑行道带四条联络道和等待线，停机坪有三个机头朝内的机位（A1–A3），玻璃立面带雨棚的航站楼，带旋转信标的塔台，拱形机库，燃油区，直升机坪，小停车场，机位后方的服务车道，围栏外有观众，树木，以及一根拴着链条的风向袋——有风时鼓起飘动，无风时耷拉。

飞机（自有物理，不是关键帧）：空速 = 推力减阻力，爬升会掉速，协调转弯（转弯率 = g·tanφ/v），基于迎角的俯仰，地面滑跑 / 抬轮 / 在 Vr 离地，飘落，触地可能弹跳。风会带着它们走：侧风时先偏航（crab），触地再摆正；五边进近时把一半逆风加到速度上。

Sparrow（上单翼教练机）：按 Upwind→Crosswind→Downwind→Base→Final 飞起落航线，做 2–3 次触地复飞，再全停。
Kestrel（轻型双发，可收起落架）：从行李拖车登机 3 名乘客加行李，飞出画面，再进港全停并下客。
Bumblebee（双翼机）：拉烟表演，在观众面前做两圈筋斗和一次横滚，再重新加入航线着陆。
Rotor 5（直升机）：从坪上起飞，飞一圈（姿态由加速度驱动），再降落。

运行：跑道锁；只有五边上没飞机才放行起飞；短五边检查，跑道占用则复飞；飘落过长或复飞失败也复飞；点击可做低空通场。滑行道是单车道：每架飞机预留它还要占用的 x 跨度，进港优先；在等待点等候的飞机算静态障碍。飞机在前方第一条空闲联络道脱离跑道。风模式：From west / From east / Shifting。持续顺风会翻转现行跑道：航线重新汇入（绝不直插五边），已在滑行道上的飞机先到旧等待点，空了再改道。除跑道上空外，飞机不得低于 3 m。看门狗：卡死 90 秒的飞机会挤过去。

地面生活：手持指挥棒的引导员把进港机引入机位；飞行员和乘客在航站楼门与飞机之间步行。加油车给每架进港机加油，停在翼尖外 1.5 m。拖车把行李推车送到双发机。两辆厢式车走单向环线（沿停机坪前缘向西，从机位间隙向北，再沿服务道回来），遇到任何机翼或即将掠过的条带就停；若已处在飞机路径上则继续开，让飞机等它们。飞机把厢式车当障碍，并保持翼尖间隙。

天气与时间：Rain 有雨丝、湿暗变色，低洼处长大的水坑用第二次镜像渲染，还有轮溅。Day / Dusk / Night 在 1.6 s 内混合；夜间有边灯、现行跑道绿/红入口条、顺序进近灯、信标、航行灯与闪光灯、泛光灯，以及亮着的航站楼和塔台舱。

界面（英文，浅色 / 深色主题）：小标题 "Pixel diorama · Airfield"、标题、短介绍。深色记分牌：DEPARTURES / 时钟 + 状态滚动条 / ARRIVALS，以及风况行（"WIND 270° 8 KT · RWY 27"）。右侧栏：Time & weather（Day/Dusk/Night、Dry/Rain、跑道湿度条）、Wind（3 种模式加风向袋读数）、Traffic（每架飞机实时状态、"Send one up"、Pause）、像素字体的塔台/飞行员通话 Radio 馈送（固定高度）、View（左转/右转、Pixel art/Raw 3D、像素大小、调色板、抖动与描边开关）。点击飞机启动或请求低空通场，点击风向袋切换风向，拖动旋转，滚轮缩放。可折叠的 "How it's drawn" 面板。手机：单列布局，16px 边距，侧栏在场景下方。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file HTML + three.js (r160, import map from jsDelivr) interactive pixel-art diorama called "Windsock Field": a small airfield on a floating rounded-rectangle island, rendered from an orthographic isometric camera into a low-res target (~480×300), upscaled with texelFetch, with depth-based outlines, OKLab quantization to a fixed 64-colour palette, optional Bayer dither, and a "Raw 3D" toggle with MSAA. Everything is built from boxes; no external assets, no real brands.
Layout: runway 09/27 across the front (edge lights, threshold bars, painted numbers, centreline, aiming points, PAPI, running approach lights), a parallel single-lane taxiway with four links and hold-short bars, an apron with three nose-in stands (A1–A3), a terminal with a glass front and canopy, a control tower with a rotating beacon, an arched hangar, a fuel farm, a helipad, a small car park, a service lane behind the stands, a fence with spectators, trees, and a chained windsock that streams with the wind and droops when it is calm.
Aircraft (own physics, not keyframes): airspeed with thrust minus drag, climbs that cost speed, coordinated turns (turn rate = g·tanφ/v), AoA-based pitch, ground roll/rotate/lift-off at Vr, flare, touchdown with a possible bounce. The wind carries them, so on crosswinds they crab and then straighten at touchdown; on final they add half the headwind to their speed.
Sparrow (high-wing trainer): flies circuits Upwind→Crosswind→Downwind→Base→Final, 2–3 touch-and-goes, then a full stop.
Kestrel (light twin, retractable gear): boards 3 passengers plus bags from a baggage tug, departs off-screen, returns inbound for a full stop, then unloads.
Bumblebee (biplane): smoke display with two loops and a roll on passes in front of the crowd, then rejoins and lands.
Rotor 5 (helicopter): lifts from the pad, flies a lap with attitude driven by acceleration, lands.
Operations: a runway lock; departure clearance only when nothing is on final; short-final check with a go-around if the runway is occupied; go-around on a long flare or a missed approach; low pass on click. The taxiway is one lane: each plane reserves the x-span of the taxiway it still has to cover, and arrivals have priority; a plane waiting at a holding point counts as a static obstacle. Planes leave the runway at the first free link ahead. Wind modes: From west / From east / Shifting. A sustained tailwind flips the active runway: circuits rejoin (never straight onto final), and planes already on the taxiway finish to their old holding point, then re-route when clear. Planes never fly below 3 m except over the runway. Watchdog: a plane stuck for 90 s squeezes past.
Ground life: a marshaller with wands guides arrivals onto the stand; pilots and passengers walk to and from the terminal door. A fuel truck refuels each arrival, parked 1.5 m off a wingtip. The tug carries carts with bags to the twin. Both vans keep to a one-way loop (westbound along the apron's front edge, northbound up the gap between stands, back along the service lane), stop for any wing or for the strip a moving plane is about to sweep, and keep going when they are already in a plane's path so it waits for them. The planes treat vans as obstacles with wingtip clearance.
Weather and time: Rain adds streaks, wet darkening and puddles that grow from low spots and show a mirrored second render pass, plus wheel spray. Day / Dusk / Night blend over 1.6 s; at night: edge lights, green/red threshold bars by the active runway, sequenced approach lights, beacon, nav lights and strobes, floodlights, a lit terminal and tower cab.
UI (English, light and dark themes): kicker "Pixel diorama · Airfield", title, short intro. A dark scoreboard with DEPARTURES / clock + status ticker / ARRIVALS and a wind line ("WIND 270° 8 KT · RWY 27"). Right rail: Time & weather (Day/Dusk/Night, Dry/Rain, runway wetness bar), Wind (3 modes plus a windsock readout), Traffic (each aircraft's live state, "Send one up", Pause), a Radio feed of tower/pilot calls in a pixel font (fixed height), View (turn left/right, Pixel art/Raw 3D, pixel size, palette, dither and outlines toggles). Click an aircraft to start it or ask for a low pass, click the windsock to swing the wind, drag to rotate, scroll to zoom. A collapsible "How it's drawn" panel. Mobile: single column with a 16px gutter and the rail below the scene.
```

</details>
