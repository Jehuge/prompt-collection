# 粉笔四方 Chalk Square

- **类型**：交互网页 / 像素风场景
- **技术栈**：three.js r160 · 像素后处理 · 球物理 · 单文件 HTML
- **标签**：`three.js` `像素风` `四方球` `后院` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 · GPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2113602050172785117) · [提示词帖](https://x.com/vib3coded/status/2113602161607069911) · 2026-10-23（北京时间） · 试玩：[Claude Opus 5.5](https://claude.ai/artifact/K7M7BKXpNRjnCA9Wwn9MZY) · [GPT-6 Astra](https://chalk-square.vercel.app/)

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（测试模型见上）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![粉笔四方 Chalk Square](../assets/chalk-square.jpg)

## 提示词（英文原文）

```text
Build a single-file HTML + three.js (r160) scene called "Chalk Square": four square played with a football in a back yard on a floating island. It is a real 3D scene rendered as crisp pixel art.

Rendering: an orthographic isometric camera (drag to turn in 90° steps, scroll or pinch to zoom). Render into a small low-res target with a depth texture, then upscale with texelFetch to whole screen pixels. Add depth-based outlines and quantize every pixel to a fixed ~60-colour palette in OKLab, with an optional Bayer dither. Toggle "Pixel art / Raw 3D", with a pixel-size slider and Palette / Dither / Outlines checkboxes.

Yard: patched, cracked asphalt with a kerb, grass and dirt around the island edge. Around the asphalt:
- a row of lock-up garages with painted, numbered doors and a flat roof that overhangs them;
- a brick transformer booth with a warning sign;
- a poplar with a bench and a grandmother on it;
- a chin-up bar, a carpet rack with a rug, bushes;
- a lamp on a pole and a lamp over a garage door.
Pigeons walk and peck, and flap up onto the roofs when the ball or a kid comes near. A cat on the garage roof follows the ball with its head.

Chalk: a data texture over the asphalt. It holds the 4.8 m square split into four zones (King, Queen, Jack, Dunce) with letters and a crown, plus hopscotch and doodles. Each texel stores its order along its stroke, so the lines can be redrawn progressively.

Game (8 kids, each with a skill, power and style: power / trick / safe / lob):
- Four kids play, four wait in a queue. The King serves by dropping the ball and kicking it after the bounce.
- The ball must bounce once in your zone, then you kick it into another zone. With the two-touch rule you may first cushion it up.
- You are out for: a ball that lands out, lands in your own zone, bounces a second time, or (if set) lands on a middle line. Otherwise a ball on the line is replayed.
- The kid who is out goes to the back of the queue. Everyone below moves up a zone, and the next kid in line enters at Dunce. A kid fetches the ball and throws it to the King.

Ball and AI: real ball physics (gravity, bounces, rolling, softer bounces in puddles, the walls). Each receiver simulates the ball forward, picks the moment it is at foot height, runs to stand behind it and kicks. Shots are a drive, a lob, or a dink just over the line, aimed away from the target kid; everyone picks on the King. Aim and power errors grow with a fast ball, a stretched contact and lower skill, and occasionally a kick is shanked.

Kids: box-rigged with two-bone IK. Poses: run, ready crouch, a kick that strikes at the ball's height, cushion, hold, throw, clap, argue a call, and a crouched walk while drawing chalk.

Time and weather: Day / Dusk / Night (the lamps light the court), Dry / Rain.
- Rain: streaks, splashes, darker asphalt, puddles that mirror the yard via a mirrored render pass, and the chalk washing out.
- The kids shelter under the garage roof. When the asphalt dries, two of them redraw the square and play resumes.

UI (English, light and dark themes, mobile layout):
- A lit scoreboard with rallies, clock + status, the King's current reign, and the best reign.
- A side rail with: Time & weather (with asphalt and chalk bars); the ladder (King / Queen / Jack / Dunce plus "Next up"); Rules (One/Two touches; Liners: Replay/Out); a feed of calls with "Gang up on the King" and Pause; View.
- Click a kid in the square and everyone aims at them. Original design, no real brands.
```

---

## 提示词（中文）

构建一个单文件 HTML + three.js（r160）场景，名叫 "Chalk Square"（粉笔四方）：漂浮小岛后院里用足球玩四方球。真实 3D 场景，渲染成清晰的像素风。

渲染：正交等距相机（拖动按 90° 步进转向，滚轮或双指缩放）。先画到带深度纹理的小低分辨率目标，再用 texelFetch 放大到整屏像素。加上基于深度的描边，并在 OKLab 里把每个像素量化到约 60 色固定调色板，可选 Bayer 抖动。可切换 "Pixel art / Raw 3D"，有像素大小滑块和 Palette / Dither / Outlines 复选框。

院子：打过补丁、开裂的沥青地，有路缘，岛边是草和泥。沥青周围有：
- 一排带漆号门的联排车库，平屋顶向前悬挑；
- 砖砌变压器亭，带警告牌；
- 一棵杨树，树下长椅上坐着一位奶奶；
- 单杠、晾毯架上挂着地毯、灌木；
- 一根灯杆，以及车库门上方的灯。
鸽子走来走去啄食，球或孩子靠近时扑到屋顶上。车库屋顶上的猫用头跟着球转。

粉笔：覆盖在沥青上的数据纹理。里面是 4.8 m 见方、分成四区（King、Queen、Jack、Dunce）的格子，有字母和皇冠，还有跳房子和涂鸦。每个纹素存着它在笔画上的次序，所以线可以渐进重画。

游戏（8 个孩子，每人有技能、力量和风格：power / trick / safe / lob）：
- 四人上场，四人排队。King 发球：把球放下，弹起后再踢。
- 球必须在你的区内弹一次，再踢进别人的区。两触规则下可以先垫一下。
- 出局情形：球出界、落在自己区、弹第二次，或（若开启）落在中线。否则中线球重赛。
- 出局的孩子排到队尾。下面的人各升一区，下一个排队的孩子从 Dunce 进场。有孩子捡球扔回给 King。

球与 AI：真实球物理（重力、弹跳、滚动，水坑里更软，还有墙）。每个接球者向前模拟球，挑脚高高度的瞬间，跑到球后方再踢。射门可以是抽射、吊球，或刚好过线的轻推，瞄准避开目标孩子；大家都会针对 King。球快、触球别扭、技能低时瞄准和力量误差变大，偶尔还会踢歪。

孩子：箱体骨骼加双骨 IK。姿势：跑、准备蹲、按球高度踢、垫球、持球、扔、鼓掌、争判、蹲着画粉笔。

时间与天气：Day / Dusk / Night（夜间灯照亮球场），Dry / Rain。
- 雨：雨丝、水花、更深的沥青，用水坑镜像渲染第二次，粉笔被冲掉。
- 孩子们躲到车库檐下。沥青干了以后，两人重画格子，比赛继续。

界面（英文，浅色 / 深色主题，移动布局）：
- 亮着的记分牌：回合、时钟 + 状态、King 当前连庄、最佳连庄。
- 侧栏：Time & weather（沥青与粉笔进度条）；阶梯（King / Queen / Jack / Dunce 加 "Next up"）；Rules（One/Two touches；Liners: Replay/Out）；判罚信息流带 "Gang up on the King" 和 Pause；View。
- 点击场上某个孩子，大家都会瞄准他。原创设计，没有真实品牌。
