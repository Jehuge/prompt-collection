# 花池 Bloom Pool

- **类型**：交互网页 / 3D 泳池与漂浮花朵
- **技术栈**：Three.js · WebGL · 自定义着色器 · Web Audio
- **标签**：`threejs` `webgl` `水面模拟` `浮力` `花朵` `合成音效` `vibe-coding` `ai-测试`
- **测试模型**：ChatGPT-6 Astra vs Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111609680057270501) · [提示词帖](https://x.com/vib3coded/status/2111609863566413948) · 2026-10-18（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 ChatGPT-6 Astra vs Claude Opus 5.5）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![花池 Bloom Pool](../assets/bloom-pool.jpg)

## 提示词（英文原文）

```text
Build “Bloom Pool” — a polished, calming interactive 3D flower pool for the browser. Deliver a self-contained HTML file with embedded assets, responsive desktop and mobile layouts, and a target of 60 fps.

VISUAL DIRECTION
A sunlit Mediterranean pool viewed from poolside perspective, not top-down. Clear turquoise water, warm ivory travertine paving, rounded bullnose coping, tiled underwater walls and floor, and a checkerboard tile band visible above the waterline. Soft palm-frond shadows cross the deck. Sunlight comes from the far-left background, illuminating the petals and scattering bright glints across the water.

Use an elegant editorial interface: large serif “Bloom Pool” title, a short understated caption, generous whitespace, and a compact translucent bottom control dock. Keep the UI in English.

CAMERA & RESPONSIVE LAYOUT
Use a fixed perspective camera with approximately 53° downward pitch on landscape screens and 58° on portrait screens, with a 36–38° field of view. Fit the entire pool inside the available viewport on every resize, keeping its edges above the control dock. Make the pool wider on desktop and deeper on phones. Do not add orbit controls.

WATER RENDERING
Use Three.js/WebGL with custom shaders.
Render the scene to an offscreen color-and-depth target, then composite the water using an inverse-view-projection ray intersection with the world-space water plane.

Include:
- World-space waves and expanding interaction ripples.
- Depth-aware screen-space refraction of submerged petals and tiles.
- Fresnel reflections of the sky, coping and tiled wall band.
- Animated underwater caustics, sun glitter and subtle foam.
- Soft flower shadows and local surface depressions beneath flowers.
- A gentle whirlpool with a visible surface depression.

Avoid duplicated or ghosted flowers at the waterline. Preserve correct occlusion around petals, coping and above-water walls. Pixels outside the pool should show the original scene directly.

FLOWERS & PHYSICS
Use detailed 3D hibiscus, bright hibiscus, lily and plumeria flowers. Petals should look delicate and softly backlit, not like flat sprites. Start with five flowers and allow up to 32.

Flowers fall into the pool, create droplets and ripples, then float with buoyancy, damped bobbing, rocking and slow rotational drift. They interact with the pool boundaries and respond to currents, nearby disturbances and the whirlpool.

INTERACTIONS
- Tap a flower button to drop that species into the pool.
- Spawn flowers from the highest altitude that remains visible on screen: large and close at first, then naturally smaller as they fall.
- Touch mode: drag flowers across the surface; press and hold to push them underwater; release to let them spring back up.
- Lift mode: pick up a flower, carry it above the water and release it to fall and splash.
- Swirl mode: activate a gentle whirlpool that influences floating flowers.
- Clear: remove the flowers with a graceful transition.
- Touching empty water creates ripples.

Use ray–plane intersections for water and elevated carrying positions. Pick flowers using projected bounds that account for camera pitch and apparent size. Mouse and touch must both work naturally.

AUDIO & CONTROLS
Add subtle procedural water ambience and responsive splash sounds through Web Audio. Start muted; enable audio only after a user gesture. Include a clear Sound toggle.

The bottom dock contains four flower selectors, Touch, Lift, Swirl and Clear. Show the active interaction mode clearly. Keep mobile touch targets comfortable and prevent page scrolling during pool gestures.

QUALITY
Use properly licensed or original assets; retain required attribution. No analytics, advertisements or unnecessary remote dependencies.

Verify desktop and phone layouts, including short landscape screens. Test flower spawning, surface dragging, sustained pressing, lifting and dropping, whirlpool forces, clearing and audio. Check for shader errors, broken assets, clipping and horizontal overflow.
```

---

## 提示词（中文）

构建 "Bloom Pool"（花池）——一个精致、令人平静的浏览器端交互式 3D 花朵泳池。交付一个内嵌资源的自包含 HTML 文件，带桌面端和移动端响应式布局，目标 60 fps。

### 视觉方向

一座阳光明媚的地中海风格泳池，从池边视角观看，而不是俯视。清澈的松石绿池水，温暖的象牙色洞石铺地，圆润的牛鼻形（bullnose）池沿压顶，水下铺瓷砖的池壁和池底，水线以上可见一条棋盘格瓷砖带。柔和的棕榈叶影子掠过池边地面。阳光来自左后方远处，照亮花瓣，并在水面上洒下明亮的闪光。

使用优雅的编辑式界面：大号衬线标题 "Bloom Pool"，一句简短低调的说明，充足的留白，以及一个紧凑的半透明底部控制栏。界面保持英文。

### 相机与响应式布局

使用固定的透视相机，横屏时俯角约 53°，竖屏时约 58°，视场角 36–38°。每次窗口尺寸变化时，都把整个泳池适配到可用视口内，让它的边缘保持在控制栏上方。桌面端让泳池更宽，手机上更深（纵向更长）。不要添加环绕控制。

### 水面渲染

使用 Three.js/WebGL 和自定义着色器。把场景渲染到一个离屏的颜色和深度目标，然后通过逆视图投影射线与世界空间水平面求交来合成水面。

包括：
- 世界空间的波浪和扩散的交互涟漪。
- 对水下花瓣和瓷砖做考虑深度的屏幕空间折射。
- 对天空、池沿压顶和瓷砖墙带的菲涅尔反射。
- 动态的水下焦散、阳光闪烁和细微泡沫。
- 柔和的花朵阴影，以及花朵下方水面的局部凹陷。
- 一个轻柔的漩涡，带可见的水面凹陷。

避免在水线处出现重复或重影的花朵。保持花瓣、池沿压顶和水上池壁周围正确的遮挡关系。泳池以外的像素应直接显示原始场景。

### 花朵与物理

使用细致的 3D 扶桑花、亮色扶桑花、百合和鸡蛋花。花瓣应看起来娇嫩、带柔和的背光，而不是扁平的精灵图。初始五朵花，最多允许 32 朵。

花朵落入泳池，溅起水滴和涟漪，然后在浮力作用下漂浮，带阻尼的上下浮动、摇摆和缓慢的旋转漂移。它们与泳池边界相互作用，并对水流、附近的扰动和漩涡作出反应。

### 交互

- 点击花朵按钮，把该品种丢进泳池。
- 从屏幕上仍然可见的最高处生成花朵：一开始又大又近，下落时自然变小。
- Touch 模式：在水面上拖动花朵；按住可以把它们压到水下；松手让它们弹回水面。
- Lift 模式：捡起一朵花，把它带到水面上方，松手让它落下溅起水花。
- Swirl 模式：启动一个影响漂浮花朵的轻柔漩涡。
- Clear：以优雅的过渡移除花朵。
- 触碰空白水面会产生涟漪。

水面和抬升搬运位置都使用射线-平面求交。拾取花朵时使用考虑了相机俯角和视觉大小的投影包围范围。鼠标和触摸都必须自然可用。

### 音频与控制

通过 Web Audio 添加细微的程序化水声环境音和灵敏的水花声。默认静音；只有在用户手势之后才启用音频。包含一个清晰的 Sound 开关。

底部控制栏包含四个花朵选择器，以及 Touch、Lift、Swirl 和 Clear。清楚显示当前的交互模式。保持移动端触控目标舒适，并在泳池手势期间阻止页面滚动。

### 质量

使用有正当授权或原创的资源；保留所需的署名。不要分析统计、广告或不必要的远程依赖。

验证桌面端和手机布局，包括高度较矮的横屏。测试花朵生成、水面拖动、持续按压、抬起和放下、漩涡力、清空和音频。检查着色器错误、损坏的资源、裁切问题和横向溢出。
