# 街角球场 Corner Court

- **类型**：交互网页 / 3D 场景
- **技术栈**：WebGL · 单文件 HTML
- **标签**：`threejs` `webgl` `像素艺术` `街头篮球` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2112989996366102944) · [提示词帖](https://x.com/vib3coded/status/2112990235453985198) · 2026-10-21（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![街角球场 Corner Court](../assets/corner-court.jpg)

## 提示词（中文）

构建 "Corner Court"（街角球场）——一个单文件、实时的 three.js 页面（r160，通过 import map 从 jsDelivr 引入的 ES 模块）：一座漂浮城市街区上的原创街头篮球半场，等距微缩场景，渲染成边缘清楚的像素画。界面文字用英文。

### 渲染管线

- 正交相机，俯仰角（elevation）约 31°，方位角 45°，再按 90° 一步步转（转向有动画；可以横向拖动，也可以用按钮）。滚轮或双指缩放。把整块台面放进空出来的屏幕区域。
- 画进一张小目标（屏幕尺寸除以像素尺寸），不做抗锯齿。把相机吸附到整像素。
- 后处理：
  - 深度轮廓（一个像素比邻居靠前超过 0.55 m 时，把它变暗）；
  - 映射到一套固定的、大约 54 色的城市调色板里、在 OKLab 中最近的颜色（混凝土和沥青的灰、天空和夜空的蓝、球场青绿、陶土和橙、红、黄、叶子的绿、皮肤和木头、黄昏的紫、霓虹粉）；可选 4×4 Bayer 抖动；
  - 用 texelFetch 按整像素放大。背景（深度 = 1）就是页面的颜色。
- 硬阴影（BasicShadowMap）。Lambert、平面着色的低多边形。
- 水坑反射：绕地面把场景镜像再画一次（scene.scale.y = -1，藏起地面网格和雨），画进第二张目标。地面着色器在 gl_FragCoord 处采样。
- "Raw 3D" 模式：同一个场景，全分辨率，带 MSAA。

### 场景

- 一块边缘参差的台面：草在上，土在中，岩石在下。
- 一块沥青场地，按 10 px/m 逐纹素画：6 米弧线以内是青绿（转角处的线是直的），陶土色的禁区，白线，罚球圈和合理冲撞区的圆，裂缝，磨掉的漆，以及一个镂空喷上去的 "COURT 7"。
- 篮筐：包了护垫的海军蓝立柱、支臂、带方框的篮板、橙色圆环篮圈，以及用线段做的球网，球穿过时会晃。
- 篮筐后面是铁丝网（做过 alpha 测试的菱形纹理）。
- 一座砖砌的街角小店：遮阳篷、亮着的窗户、粉色霓虹 "OPEN"，以及一台自动售货机。
- 一面长墙，上面是一幅原创的日落城市壁画。
- 一条人行道，一张长椅，两个坐着的观众。
- 泛光灯、一盏路灯、低多边形的树、树篱、一个垃圾箱、一座喷泉、一个停着两辆自行车的车架、一个消防栓。
- 鸽子在啄食。球员或者球靠近时，它们会飞走。

### 球员——大约 17 个盒子的程序化骨骼

- 腿用双骨 IK（跑步的步幅、防守滑步、收腿起跳）。手臂也用双骨 IK：运球的手跟着球走，跳投有出手点和鹅颈随挥，上篮伸手，双手扣篮，胸前传球，抢篮板或封盖时伸手，以及庆祝。
- 观众坐着。进球时欢呼。下雨时把伞打开。

### 比赛——街头篮球，2 对 2，半场

- Make it take it：进球的一方继续进攻。弧线内得 1 分，弧线外得 2 分。先到 11 分。有一个胜场计数。
- 在弧顶 check ball：把球传给防守的人，再传回来，才算开始。球权交换之后，必须先把球清出弧线外。
- 进攻 AI：运到点位上；线路空就突破；没人防就急停跳投；到篮下就上篮或扣篮；被逼就传球。无球的人定点站好，或者空切。防守是人盯人：有站位、控制间距、抢断，以及跳起来干扰（盖帽）。
- 球的物理按子步算：在沥青上弹，球体对圆环篮圈和篮板盒子，球网的拖曳，立柱、围栏、墙、台面边缘。
  - 跳投沿一条弹道弧瞄准（大约 50°）。距离越远、干扰越大，速度和瞄准的噪声越大。
  - 上篮被抛到篮圈上方的一个最高点，然后掉进去。
  - 抢篮板要起跳。出界归对方。
- 比分、球权和状态字（"SWISH"、"BLOCKED!"、"TAKE IT BACK" 等等）显示在一块亮着的记分牌上。
- 点击：点持球的人，他就投；点他的队友，就把球传过去；点场地，持球的人就跑到那里。另有 Shoot / Pass 按钮。

### 天气和时间

- Day / Dusk / Night 三套光照，大约用 1.6 秒混过去。夜里打开泛光灯、路灯、霓虹和窗户。
- Dry / Drizzle / Downpour：雨是短短的线段，落地有水花。一个湿润值会升高，再慢慢变干。沥青变暗。水坑从一张预先算好的深度图的低洼处铺开，并镜像整个场景，雨滴的涟漪在水坑里闪。脚和球都会溅水。

### 界面

- 像素显示字体用 Silkscreen，正文用一套干净的字体。浅色和深色主题用 token 切换。
- 控制：Time、Weather（带一条球场湿润度）、Shoot、Pass、New game、Pause、Turn left / right、Pixel art / Raw 3D、像素尺寸、Palette / Dither / Outlines。
- 一块 "How it's drawn" 面板。手机上改成上下堆叠，不要出现横向滚动。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "Corner Court" — a single-file, real-time three.js (r160, ES module via import map from jsDelivr) page: an isometric diorama of an original street basketball half court on a floating city block, rendered as crisp pixel art. UI text in English.

RENDER PIPELINE
- Orthographic camera at ~31° elevation, azimuth 45° + 90° steps (animated; drag sideways or buttons), wheel/pinch zoom; fit the whole slab into the free screen area.
- Render into a small target (screen / pixel size) with no anti-aliasing; snap the camera to whole pixels.
- Post pass:
  - depth outlines (darken a pixel >0.55 m in front of a neighbour);
  - nearest colour of a fixed ~54-colour city palette in OKLab (concrete/asphalt greys, sky and night blues, court teal, terracotta/orange, reds, yellows, leaf greens, skin/wood, dusk purples, neon pink); optional 4×4 Bayer dither;
  - whole-pixel upscale via texelFetch; the background (depth = 1) is the page colour.
- Hard shadows (BasicShadowMap); flat-shaded Lambert low-poly.
- Puddle reflections: render the scene mirrored about the ground (scene.scale.y = -1, ground meshes and rain hidden) into a second target, sampled at gl_FragCoord in the ground shader.
- "Raw 3D" mode: the same scene at full resolution with MSAA.

SCENE
- A ragged-edged slab: grass over soil over rock.
- An asphalt pad painted texel-by-texel at 10 px/m: teal inside the 6 m arc (straight corner lines), terracotta key, white lines, free-throw and restricted circles, cracks, worn paint, a stencilled "COURT 7".
- Hoop: padded navy pole, arm, backboard with its square, orange torus rim, and a line-segment net that sways when the ball goes through.
- Chain-link fence behind the hoop (alpha-tested diamond texture).
- A brick corner shop with an awning, lit windows, a pink "OPEN" neon sign and a vending machine.
- A long wall with an original sunset-city mural.
- A sidewalk with a bench and two seated spectators.
- Floodlights, a streetlight, low-poly trees, hedges, a dumpster, a fountain, a bike rack with two bikes, a hydrant.
- Pigeons that peck and fly off when players or the ball come near.

PLAYERS — procedural rigs of ~17 boxes
- Two-bone IK for legs (running stride, defensive slide, tucked jumps) and arms: dribble hand following the ball, jump-shot set point with release and gooseneck follow-through, layup reach, two-hand dunk, chest pass, rebound/contest reach, celebration.
- Spectators sit, cheer on makes and open umbrellas in the rain.

GAME — streetball 2v2 half court
- Make it take it; 1s inside the arc, 2s beyond; first to 11; win counter.
- Check ball at the top (pass to the defender and back). A change of possession must be cleared beyond the arc.
- Offence AI: dribble to spots, drive when the lane is open, pull-up jumpers when open, layups/dunks at the rim, passes when pressured; the off-ball player spots up or cuts. Man-to-man defence with stance, gap control, steals and contested jumps (blocks).
- Ball physics with substeps: bounces on asphalt, sphere vs torus rim and backboard box, net drag, pole, fences, wall, slab edge.
  - Jumpers aimed on a ballistic arc (~50°) with speed/aim noise growing with distance and contest.
  - Layups lofted to a peak above the rim so they drop in.
  - Rebounds with jumps; out of bounds goes to the other team.
- Score, possession and status messages ("SWISH", "BLOCKED!", "TAKE IT BACK", …) on a lit scoreboard.
- Clicks: the ball handler shoots, his teammate gets a pass, the court sends the handler there. Shoot/Pass buttons.

WEATHER AND TIME
- Day / Dusk / Night lighting presets blended over ~1.6 s; floodlights, streetlight, neon and windows at night.
- Dry / Drizzle / Downpour: rain as short line streaks with splashes. A wetness value rises and slowly dries: the asphalt darkens, puddles spread from low spots in a precomputed depth map and mirror the scene, rain rings flicker in them; feet and the ball splash.

UI
- Pixel display font (Silkscreen) and a clean body font; light/dark themes via tokens.
- Controls: Time, Weather (with a court wetness bar), Shoot, Pass, New game, Pause, Turn left/right, Pixel art/Raw 3D, Pixel size, Palette/Dither/Outlines.
- A "How it's drawn" panel; a stacked mobile layout with no horizontal scroll.
```

</details>
