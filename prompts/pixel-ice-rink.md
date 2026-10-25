# 像素冰场 Pixel Ice Rink

- **类型**：交互网页 / 像素风场景
- **技术栈**：WebGL · 单文件 HTML
- **标签**：`threejs` `webgl` `像素艺术` `冰球` `vibe-coding` `ai-测试`
- **测试模型**：未注明
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2113217041985401339) · [提示词帖](https://x.com/vib3coded/status/2113217928120221741) · 2026-10-22（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（具体测试模型未注明）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![像素冰场 Pixel Ice Rink](../assets/pixel-ice-rink.jpg)

## 提示词（英文原文）

```text
Build "Pixel Ice Rink" — a single-file, real-time three.js (r160, ES module via import map from jsDelivr) page: an isometric diorama of a floating outdoor ice rink, rendered as crisp pixel art in the style of "3D rendered as pixel art". UI text in English.

RENDER PIPELINE
- Orthographic camera at ~31° elevation, azimuth 45° + 90° steps (animated turns, drag sideways or buttons), wheel/pinch zoom. Fit the whole floating slab into the free screen area (clear of the title, a top-centre scoreboard and a right control rail).
- Render the scene into a tiny target (screen / pixel size, ~480×300 on desktop) with no anti-aliasing. Snap the camera so the world origin lands on a whole pixel (static things never shimmer).
- Post pass on a full-screen quad:
  - depth-based outlines: darken a pixel that stands >0.55 m in front of a neighbour;
  - map every pixel to the nearest colour of a fixed ~49-colour winter palette in OKLab (snow/ice greys, ice blues, reds, lamplight/wood/skin, pines, dusk peach/rose/mauve/lilac, brass/ochre);
  - optional light 4×4 Bayer dither;
  - upscale with texelFetch so each art pixel is an exact block of device pixels. The background (depth = 1) is the page colour.
- Hard sun shadows (BasicShadowMap, 2048). Lambert flat-shaded low-poly materials.
- Planar ice reflection: render the scene mirrored (scene.scale.y = -1 about the ice plane, ground, ice, particles and lamp posts hidden) into a second target. Sample it in the ice shader at gl_FragCoord. Gloss = small base + extra where the ice is wet, reduced where it is worn.
- A "Raw 3D" mode renders the same scene at full resolution with MSAA, for comparison.

SCENE
- A floating slab of snow over earth over rock, each extruded from a ragged rounded rectangle.
- A 24×12 m rink with 3 m corners: white boards with a yellow kick plate and red cap, built as band segments with gaps for two bench doors and a double resurfacer gate (hinged doors that swing open).
- Ice markings painted texel-by-texel into a 10 px/m canvas: red centre and goal lines, blue lines, circles, face-off dots, creases.
- Red-post goals with alpha-tested grid nets; players' benches; a lit scoreboard drawn with 3×5 pixel digits.
- A log warming hut with lit windows and chimney smoke; a garage for the resurfacer; lamp posts with point lights; string lights at night.
- Snowy stacked-cone pines, snowbanks, a snowman.

PLAYERS — procedural rigs of ~16 boxes
- Placed every frame from heading, lean, crouch and turn roll. Two-bone IK for the legs (skating stride with push-out and toe-out, gliding, sideways hockey stop) and for the arms holding a stick.
- Stick poses: carry/stickhandle, slap-shot wind-up and strike, pass sweep, celebration with stick raised.
- Goalies: pads, blocker and glove, crease positioning, butterfly drop on incoming shots.

GAME
- Two-on-two pick-up hockey plus goalies. Steering with arrival, separation and board/net avoidance; hockey stops when reversing hard.
- Carrier AI weaves to the slot, shoots when the lane is open, passes when pressured. Defenders pressure goal-side and poke-check; the nearest skater chases a loose puck.
- Puck physics with substeps: friction, board bounces, posts, solid nets with goal detection through the mouth, goalie saves (deflect or catch and play out), blocks by skates.
- Face-offs, goal celebrations, score, shots and a game clock on the scoreboard. Clicking the ice drops a puck.

ICE WEAR
- An RG DataTexture over the rink (20 px/m). Blades write scratches as they glide; stops gouge wider marks and throw spray particles that settle as wear; falling snow settles too.
- "Resurface the ice": players skate off through the bench doors; the resurfacer drives out of its garage through the gate and does shrinking rounded-rectangle laps (swinging in front of the nets), wiping its swath and leaving wet, reflective ice that dries over time. Then the players return for a face-off. Show an "ice worn %" bar.

UI
- Pixel display font (Silkscreen) with a clean body font.
- Light and dark themes via tokens; the background is a near-white or near-black page.
- Controls: Day / Dusk / Night (lighting presets blended over ~1.6 s), Snow Off / Light / Heavy, Resurface, Drop a puck, Pause, New game, Turn left / right, Pixel art / Raw 3D, Pixel size slider, Palette / Dither / Outlines toggles.
- A "How it's drawn" panel explaining the pipeline. Stacked mobile layout with no horizontal scroll.
```

---

## 提示词（中文）

构建 "Pixel Ice Rink"（像素冰场）——一个单文件、实时的 three.js 页面（r160，通过 import map 从 jsDelivr 引入的 ES 模块）：一座漂浮在空中的户外冰场，等距微缩场景，按 "3D rendered as pixel art" 的方式渲染成边缘清楚的像素画。界面文字用英文。

### 渲染管线

- 正交相机，俯仰角（elevation）约 31°，方位角 45°，再按 90° 一步步转（转向有动画；可以横向拖动，也可以用按钮）。滚轮或双指缩放。把整块漂浮的台面放进空出来的屏幕区域（不要挡住标题、顶部正中的记分牌，以及右边的控制栏）。
- 场景先画进一张很小的目标（屏幕尺寸除以像素尺寸，桌面上大约 480×300），不做抗锯齿。吸附相机，让世界原点落在整像素上（静止的东西不会闪）。
- 在全屏四边形上做后处理：
  - 按深度描边：一个像素比旁边的邻居靠前超过 0.55 m 时，把它变暗；
  - 每个像素映射到一套固定的、大约 49 色的冬季调色板里、在 OKLab 中最近的颜色（雪和冰的灰、冰蓝、红、灯光 / 木头 / 皮肤、松树绿、黄昏的桃 / 玫瑰 / 淡紫 / 丁香、黄铜和赭石）；
  - 可选一层很轻的 4×4 Bayer 抖动；
  - 用 texelFetch 放大，让每一颗艺术像素正好对应一块设备像素。背景（深度 = 1）就是页面的颜色。
- 硬边的太阳阴影（BasicShadowMap，2048）。材质是 Lambert、平面着色的低多边形。
- 冰面的平面反射：把场景镜像再画一次（绕冰面令 scene.scale.y = -1，藏起地面、冰、粒子和灯柱），画进第二张目标。冰的着色器在 gl_FragCoord 处采样。光泽 = 一个很小的底值，冰面湿的地方再加，磨损的地方再减。
- "Raw 3D" 模式把同一个场景按全分辨率、带 MSAA 画出来，用来对比。

### 场景

- 一块漂浮的台面：上面是雪，中间是土，下面是岩石。每一层都从一个边缘参差的圆角矩形挤出。
- 冰场 24×12 m，四个角的半径 3 m。白色挡板，下面一条黄色踢脚板，上面一条红色压顶。挡板做成一段一段的带状，留出两扇球员席的门，以及浇冰车的一扇双开门（铰链门会甩开）。
- 冰面标线按 10 px/m 逐纹素画进一张画布：红色的中线和球门线、蓝线、圆圈、争球点、守门员限制区（crease）。
- 红色门柱，球网是做过 alpha 测试的网格。球员席。一块亮着的记分牌，数字是 3×5 的像素字。
- 一座原木取暖小屋，窗户亮着，烟囱冒烟。浇冰车的车库。带点光源的灯柱。夜里有串灯。
- 积雪的、由锥体叠起来的松树，雪堆，一个雪人。

### 球员——大约 16 个盒子的程序化骨骼

- 每一帧按朝向、前倾、下蹲和转弯时的侧倾来摆。腿用双骨 IK（滑冰的步幅：向外蹬、脚尖外八、滑行、侧向的冰球急停）。手臂也用双骨 IK，手里拿着球杆。
- 球杆的姿势：带球 / 控杆，击射的后引和击打，传球时的扫杆，举杆庆祝。
- 守门员：护腿、挡板和手套，在限制区里卡位，来球时做蝶式下跪。

### 比赛

- 二对二的捡场冰球，加上守门员。转向用到达（arrival）、分离（separation），并躲开挡板和球网。猛地反向时做冰球急停。
- 持球的人盘带到槽位（slot）。射门线路是空的就射，被逼就传球。防守的人站在更靠近球门的一侧施压，并用球杆戳抢。冰球自由的时候，离得最近的滑冰者去追。
- 冰球物理按子步算：摩擦、撞挡板反弹、门柱、实体球网（从门洞穿过去就算进球）、守门员扑救（拨开，或者接住再传出来）、被冰鞋挡住。
- 争球、进球庆祝、比分、射门数和比赛时钟都在记分牌上。点击冰面可以放下一只冰球。

### 冰面磨损

- 一张铺在冰场上的 RG DataTexture（20 px/m）。冰刀滑过就写下划痕。急停会凿出更宽的痕迹，并甩出冰屑粒子，落下去变成磨损。降雪也会积在上面。
- "Resurface the ice"：球员从球员席的门滑出去。浇冰车从车库开出来，穿过大门，一圈一圈跑逐渐缩小的圆角矩形（在球门前面拐弯），把经过的那一条擦掉，留下湿的、会反光的冰，然后慢慢变干。球员再回来争球。显示一条 "ice worn %" 的条。

### 界面

- 像素显示字体用 Silkscreen，正文用一套干净的字体。
- 浅色和深色主题用 token 切换。背景是接近白或接近黑的页面。
- 控制：Day / Dusk / Night（光照预设大约用 1.6 秒混过去）、Snow Off / Light / Heavy、Resurface、Drop a puck、Pause、New game、Turn left / right、Pixel art / Raw 3D、像素尺寸滑块、Palette / Dither / Outlines 开关。
- 一块 "How it's drawn" 面板，解释这条管线。手机上改成上下堆叠，不要出现横向滚动。
