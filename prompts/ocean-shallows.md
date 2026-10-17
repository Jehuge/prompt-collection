# 浅海 Ocean Shallows

- **类型**：交互网页 / 3D 海洋模拟
- **技术栈**：Three.js r128（cdnjs）· WebGL · 单文件 HTML
- **标签**：`threejs` `webgl` `shader` `水面模拟` `焦散` `海洋生物` `创意编程` `vibe-coding`

> 说明：下方是中文翻译版提示词。页面本身的界面文字仍要求使用**英文**（例如按钮名称和计数文字 "4 rays · 5 jellies" 保持原样）。英文原文附在文末。

---

## 提示词（中文）

用 Three.js r128（通过 cdnjs 引入）构建一个单文件 WebGL 页面，标题为 "Ocean Shallows"：以俯视视角呈现一片铺满整个屏幕的热带海域，左上角有一小段弯曲的沙滩。

### 水面

- 基于 GPU 的高度场（height-field）涟漪模拟，屏幕边缘为吸收边界（不反射波纹）。
- 折射效果与流动的焦散（caustics）。
- 朝岸边滚动的长涌浪，以及细碎的阳光闪烁。
- 按水深着色：靠近沙滩为浅松石绿，离岸处为深蓝宝石色。
- 在沙滩上，海浪破碎，化作带泡沫的冲流（swash）和蕾丝状泡沫冲上沙面，然后回退，留下有光泽的湿沙。
- 一棵摇曳的棕榈树（树干和叶片）的影子投在沙滩和浅水区上。

### 海床（预烘焙）

- 带波纹的沙地和海草草甸。
- 珊瑚头和礁石，带接触阴影。
- 珊瑚碎石、海星、贝壳和海胆。

### 生物

- 一个磨砂玻璃质感的底部栏（dock）放着五张生物卡片。每张缩略图都由真实的 3D 模型渲染而成：蝠鲼（Manta）、斑点鹞鲼（Spotted Eagle Ray）、蓝斑魟（Blue-spotted Stingray）、海月水母（Moon Jelly）、太平洋黄金水母（Sea Nettle）。
- 点击卡片，生物会沿抛物线被扔进海里，并带有水花、波纹圈和飞溅的水滴。
- 拖动卡片可以把生物悬停在水面上方，然后放到任意位置。

### 鳐鱼类

- 使用实例化（instanced）的扁平双层片状身体，翅膀沿翼展方向弯曲。蝠鲼和鹞鲼拍动胸鳍；魟鱼的圆盘状身体做波浪式起伏。
- 每种都有尾巴和各自的花纹：
  - 蝠鲼：黑色背部带白色肩斑，有头鳍（cephalic fins），白色腹部带深色斑点。
  - 鹞鲼：深色背部带白色斑点和圆环，长鞭状尾巴。
  - 魟鱼：棕褐色带电光蓝斑点，有喷水孔（spiracles）和条纹尾巴。
- 鳐鱼转弯时会侧倾，在沙地上投下阴影，被触碰时会逃开，靠近水面时会留下尾迹。
- 蝠鲼和鹞鲼有时会跃出水面并在空中翻转。
- 魟鱼会趴在沙地上休息，受惊时扬起一团泥沙。

### 水母

- 伞盖脉动（快速收缩、缓慢舒张），推动水母沿伞盖轴线前进。
- 半透明的菲涅尔（fresnel）着色。
- 随洋流漂移，并会被漩涡吸引。
- 海月水母：四个粉色马蹄形生殖腺、辐射管和一圈触手边缘。
- 太平洋黄金水母：琥珀色伞盖带铁锈色条纹，长长的拖尾触手和褶皱的奶油色口腕。将这些触手和口腕绘制为面向相机的条带（camera-facing ribbons）：运动时向后飘动，静止时垂直下垂，被提到空中时会滴水。

### 控制

Rain（下雨）、Whirlpool（漩涡，可拖动改变位置）、Calm（平静）、Clear sea（清空海洋）、Sound（声音：与冲流同步的合成海浪声，外加水花声和叮咚声）、Hide UI（隐藏界面）。添加键盘快捷键 R / W / C / M / H。

### 界面

界面语言为英文，字体使用 Fraunces + Nunito Sans，移动端响应式布局，显示生物计数器（"4 rays · 5 jellies"），生物数量上限 48 个，并根据性能自适应渲染质量。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single-file Three.js r128 (cdnjs) WebGL page titled "Ocean Shallows": a top-down view of a tropical sea filling the whole screen, with a small curved beach in the top-left corner.

Water:
- GPU height-field ripple simulation with absorbing screen edges.
- Refraction and moving caustics.
- Long swell rolling toward the shore, plus fine sun glitter.
- Depth-based color: pale turquoise near the beach, deep sapphire offshore.
- On the beach, waves break, rush up the sand as foamy swash with lace foam, then drain back and leave glossy wet sand.
- The shadow of a swaying palm (trunk and fronds) falls across the beach and the shallows.

Seabed (baked):
- Rippled sand and seagrass meadows.
- Coral heads and boulders with contact shadows.
- Coral rubble, starfish, shells and sea urchins.

Creatures:
- A frosted-glass dock holds five creature cards. Each thumbnail is rendered from the real 3D model: Manta, Spotted Eagle Ray, Blue-spotted Stingray, Moon Jelly, Sea Nettle.
- Tap a card to throw the creature on an arc into the sea, with a splash, rings and droplets.
- Drag a card to hold the creature above the water, then drop it anywhere.

Rays:
- Instanced flat two-sheet bodies whose wings bend along the span. Mantas and eagle rays flap; the stingray's disc undulates.
- Each has a tail and its own pattern:
  - Manta: black back with white shoulder patches, cephalic fins, white belly with dark spots.
  - Eagle ray: dark back with white spots and rings, long whip tail.
  - Stingray: tan with electric-blue spots, spiracles and a striped tail.
- Rays bank in turns, cast shadows on the sand, flee from touches and leave wakes near the surface.
- Mantas and eagle rays sometimes breach and flip in the air.
- Stingrays rest on the sand and puff silt when startled.

Jellyfish:
- Pulsing bells (fast contraction, slow relaxation) push them along the bell axis.
- Translucent fresnel shading.
- They drift with ocean currents and get pulled by the whirlpool.
- Moon jelly: four pink gonad horseshoes, radial canals and a fringe of tentacles.
- Sea nettle: amber bell with rust stripes, long trailing tentacles and frilly cream oral arms. Draw these as camera-facing ribbons that stream behind its motion, hang straight down and drip when it is held in the air.

Controls: Rain, Whirlpool (drag to move it), Calm, Clear sea, Sound (synthesized surf timed to the swash, plus splashes and plinks), Hide UI. Add keyboard shortcuts R / W / C / M / H.

UI: English, Fraunces + Nunito Sans fonts, responsive mobile layout, a creature counter ("4 rays · 5 jellies"), a 48-creature cap and adaptive render quality.
```

</details>
