# 南瓜测试 The Pumpkin Test

- **类型**：交互网页 / 物理小游戏
- **技术栈**：Three.js（内联打包）· 刚体碎裂 · Web Audio
- **标签**：`threejs` `刚体` `碎裂` `万圣节` `合成音效` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111050769960997105) · [提示词帖](https://x.com/vib3coded/status/2111051043719062008) · 2026-10-16（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。结尾的 "publish it as an artifact" 是针对 Claude Artifacts 的要求，其他工具可忽略。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 提示词（中文）

构建 "The Pumpkin Test"（南瓜测试）——西瓜橡皮筋挑战的万圣节版本。一个自包含 HTML 文件：Three.js 内联打包（运行时不用 CDN），界面为英文。

### 玩具

一个雕刻好的南瓜灯（jack-o'-lantern）在夜晚放在门廊上。点击它（或按空格）就在它身上再套一根橡皮筋。每根橡皮筋都会增加压力，直到在一个随机上限处，它炸开。

- 南瓜：一个扁圆、带棱的实体（10 条略不规则的棱，果柄端和花蒂端各有凹窝），定义为每个方向上的半径，便于采样、射线投射和包裹。使用查找表，使重塑一个 97×241 的顶点网格只需约 1 ms。一根弯曲、扭转、带棱脊的果柄。
- 橡皮筋成对落在相对的沟槽里，从果柄旁边越过顶部、从底部下方绕过，并紧绷地跨过凹窝。每根橡皮筋从比南瓜略大的尺寸"啪"地套上去。同一沟槽中的橡皮筋并排放置。拉伸时颜色变浅。颜色：黑、紫、青柠绿、橙和天然棕褐色。
- 随着压力增加：南瓜下垂并向外摊开，套着橡皮筋的沟槽加深，棱鼓起。雕刻的脸从露齿笑慢慢变成歪歪扭扭的苦脸，眼睛睁大并倾斜。里面的蜡烛闪得更厉害。接近上限时，沿鼓起的棱顶裂开发光的裂缝，透出烛光。南瓜颤抖，屏住呼吸片刻，然后炸开。
- 炸开：外壳沿裂开的棱顶分裂成棱瓣（外面是瓜皮，里面是橙色果肉，参差的切面），像花瓣一样向外倒开。果柄盖飞起来，底部滑向一边，留下站立着的茶蜡蜡烛。果肉块、约 55 粒籽、一缕缕瓜瓤、断掉的和完整的橡皮筋、汁液滴和溅在木板上的污渍。七只蝙蝠飞出来。相机震动。一秒后蜡烛伴随一缕烟熄灭，场景变暗。
- 碎片：在接触点与木板接触的刚体（顺序冲量、摩擦、休眠），保持在可见区域内。
- 结束卡片："Well…" / "N bands." / 是哪种南瓜，配一个 "Carve another"（再雕一个）按钮。三种南瓜，上限和敲击声各不相同：薄壁（30–40 根）、雕刻南瓜（44–56 根）、厚壁大田南瓜（58–70 根）。

### 外观

- 瓜皮着色器：橙色，沟槽更深，细条纹、雀斑和绿棕色的肩部。脸是程序化雕刻的（在瓜皮自身坐标中用 SDF 生成眼睛、鼻子和露齿的嘴）。孔洞发出炽热的黄光，在切口处加深为橙色，有一圈被照亮的薄果肉和一圈淡淡的暖色光晕。脸后方的一个点光源照暖前方的木板。
- 舞台：饱经风霜、渐隐入黑暗的门廊木板，落下的枫叶，低低飘动的雾。一盏暖色门廊灯投下阴影，后方是冷色月光。CSS 夜空，带星星、满月和蝙蝠剪影。
- 字体排版：刊头 "The Pumpkin Test" 使用 Grenze Gotisch，"Pumpkin" 为余烬橙色。说明文字用 IM Fell English 斜体。计数器用 JetBrains Mono。刻意的深色单一主题。

### UI

左上刊头配 "How much pressure can it take?"。右上是低调的控件：Knock（敲击，K）、Reset、Sound。底部居中："Bands: N"，一串逐级变化的说明文字（"Tap the pumpkin to add pressure" → "Everything seems fine." → "Probably still fine." → "Jack is under pressure." → "This feels cursed." → "Maybe stop."），以及一条细细的压力条，接近尾声时变成余烬橙色。敲击会描述声音（"Hollow and papery. Thin walls." … "The pitch is climbing." / "Ringing. Any moment."）。每次点击产生一个橡皮筋颜色的波纹环。拖动可以转动南瓜。南瓜带一下弹跳落入场景。

### 声音（合成，Web Audio，无背景环境音）

橡皮筋"啪"声音高随压力上升，瓜皮吱嘎声，每种南瓜各自的敲击音，炸开时湿漉漉的拍击声和橡皮筋崩断声，碎块落地的闷响，蜡烛熄灭声，蝙蝠的啾啾声和扑翅声。

必须能在手机上运行（触摸、底部 HUD）。遵守 prefers-reduced-motion。没有 WebGL 时显示降级页面。暴露一个测试钩子。无头测试：点击、空格、敲击、拖动、下垂和摊开、炸开、结束卡片、"Carve another"、重置、手机布局，以及无控制台报错。交付 HTML 文件并将其发布为 artifact。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build "The Pumpkin Test" — a Halloween take on the watermelon rubber-band challenge. One self-contained HTML file: Three.js bundled inline (no runtime CDN), English UI.

THE TOY
A carved jack-o'-lantern sits on a porch at night. Tap it (or press Space) to stretch another rubber band round it. Every band adds pressure until, at a random limit, it bursts.
- Pumpkin: an oblate, ribbed solid (10 slightly irregular ribs, dimples at the stem and the blossom end), defined as a radius for every direction so it is easy to sample, ray-cast and wrap. Use lookup tables so reshaping a 97×241 vertex grid takes about 1 ms. A curved, twisted, ridged stem.
- Bands lie in pairs of opposite grooves, run over the top beside the stem and under the bottom, and bridge the dimples tautly. Each band snaps on from slightly bigger than the pumpkin. Bands in the same groove sit side by side. They pale as they stretch. Colours: black, purple, lime, orange and natural tan.
- As the pressure builds: the pumpkin sags and spreads, the banded grooves deepen and the ribs bulge. The carved face slowly changes from a toothy grin to a wobbly grimace with wide, tilted eyes. The candle inside flickers harder. Near the limit, glowing cracks open along the crowns of the bulging ribs and leak candle light. The pumpkin trembles, holds its breath for a moment, then bursts.
- Burst: the shell splits along the cracked crowns into rib wedges (rind outside, orange flesh inside, jagged cut walls) that fall open like petals. The stem cap flies up and the bottom skids aside, leaving the tealight candle standing. Flesh chunks, about 55 seeds, strings of pulp, broken and whole bands, juice drops and splats on the boards. Seven bats fly out. The camera shakes. A second later the candle goes out with a curl of smoke and the scene darkens.
- Debris: rigid bodies touching the boards at contact points (sequential impulses, friction, sleeping), kept inside the visible area.
- End card: "Well…" / "N bands." / which kind it was, with a "Carve another" button. Three kinds with different limits and knock sounds: thin-walled (30–40 bands), a carving pumpkin (44–56), a thick-walled field pumpkin (58–70).

LOOK
- Rind shader: orange with darker grooves, fine streaks, freckles and a green-brown shoulder. The face is carved procedurally (SDF eyes, nose and toothy mouth in the rind's own coordinates). The holes glow hot yellow, deepening to orange at the cut, with a thin band of lit flesh and a faint warm halo. A point light just inside the face warms the boards in front.
- Stage: weathered porch boards fading into darkness, fallen maple leaves, low drifting mist. A warm porch lamp casts the shadows, with cold moonlight behind. CSS night sky with stars, a full moon and silhouetted bats.
- Typography: masthead "The Pumpkin Test" in Grenze Gotisch with "Pumpkin" in ember orange. Captions in IM Fell English italic. Counters in JetBrains Mono. Deliberately dark, single theme.

UI
Masthead top-left with "How much pressure can it take?". Quiet controls top-right: Knock (K), Reset, Sound. Bottom centre: "Bands: N", a caption ladder ("Tap the pumpkin to add pressure" → "Everything seems fine." → "Probably still fine." → "Jack is under pressure." → "This feels cursed." → "Maybe stop.") and a thin pressure bar that turns ember-orange near the end. Knocking describes the sound ("Hollow and papery. Thin walls." … "The pitch is climbing." / "Ringing. Any moment."). A ripple ring in the band's colour at each tap. Drag to turn the pumpkin. The pumpkin drops in with a bounce.

SOUND (synthesised, Web Audio, no background ambience)
Band snaps that rise in pitch with pressure, rind creaks, knock tones per kind, a burst with a wet slap and band pops, thuds of landing pieces, the candle going out, bat chirps and wing flutter.

Must work on phones (touch, bottom HUD). Respect prefers-reduced-motion. Show a fallback without WebGL. Expose a test hook. Test headlessly: tapping, Space, knock, drag, sag and spread, burst, the end card, "Carve another", reset, a phone layout and no console errors. Deliver the HTML file and publish it as an artifact.
```

</details>
