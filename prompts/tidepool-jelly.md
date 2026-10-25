# 潮池果冻 Tidepool Jelly

- **类型**：交互网页 / 果冻海岸生态
- **技术栈**：Three.js · 自定义着色器 · 正交相机
- **标签**：`threejs` `shader` `果冻` `潮汐` `海洋生物` `生物荧光` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2109015574177075610) · [提示词帖](https://x.com/vib3coded/status/2109016138030141473) · 2026-10-11（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![潮池果冻 Tidepool Jelly](../assets/tidepool-jelly.jpg)

## 提示词（英文原文）

```text
Create “Tidepool Jelly” - an interactive 3D miniature coastal ecosystem where everything feels soft, squishy, and made of translucent jelly.
Show an elevated, cutaway slice of coastline floating against a warm off-white background. Include layered sand and rock beneath the surface, shallow turquoise water, rocky tide pools, rounded pebbles, seashells, and small patches of coastal greenery. Use an orthographic camera with orbit and zoom controls.
Make the water the star of the scene: convincing waves, spreading ripples, reflections, refraction, underwater caustics, and a wet shoreline. Animate a rising and falling tide that fills and drains the pools. Clicking or dragging through water should create localized ripples that fade naturally.
Populate the pools with animated jelly sea creatures: tiny crabs, starfish, sea anemones, snails, mussels, shrimp, and small fish. Give each species distinct movement and behavior. Crabs scuttle around rocks, anemones sway with the current, snails crawl slowly, and fish swim in loose groups. Their bodies should gently wobble and deform as they move.
Let users click a creature to focus the camera and reveal a compact species card. Allow gentle interactions that trigger a squishy reaction, followed by a smooth return to the original shape.
Add a clean, minimal control panel with:
Tide height and automatic tide cycle.
Wave strength and water clarity.
Jelly softness.
Day and night lighting.
Species visibility toggles.
Pause, reset, and a randomize ecosystem button.
At night, introduce subtle bioluminescence in the water and selected creatures.
Use elegant editorial typography, generous whitespace, and restrained UI styling. Place the “Tidepool Jelly” title in the upper-left corner and controls on the right. The scene should dominate the screen.
Build a fully working browser experience using Three.js and custom shaders where useful. Prioritize beautiful water, believable creature movement, tactile jelly materials, and smooth performance. All controls must work. Avoid static mockups, placeholder assets, and oversized interface elements.
```

---

## 提示词（中文）

创建 "Tidepool Jelly"（潮池果冻）——一个交互式 3D 微缩海岸生态系统，其中一切都显得柔软、有弹性，由半透明果冻构成。

展示一块抬高的、剖切开的海岸线切片，漂浮在暖白色背景上。包括水面下分层的沙子和岩石、浅浅的松石绿海水、岩石潮池、圆润的卵石、贝壳和小片海岸植被。使用正交相机，带环绕和缩放控制。

让水成为场景的主角：可信的波浪、扩散的涟漪、反射、折射、水下焦散和湿润的岸线。做一个涨落的潮汐动画，让潮池注满又排干。在水中点击或拖动应产生局部涟漪，并自然消散。

在潮池中放入有动画的果冻海洋生物：小螃蟹、海星、海葵、蜗牛、贻贝、虾和小鱼。给每个物种不同的运动方式和行为。螃蟹在岩石间横爬，海葵随水流摇摆，蜗牛缓慢爬行，鱼成松散的小群游动。它们的身体在移动时应轻轻晃动和变形。

让用户点击某个生物时相机聚焦过去，并显示一张紧凑的物种卡片。允许轻柔的交互，触发有弹性的反应，然后平滑恢复原形。

添加一个干净、极简的控制面板，包括：
- 潮位高度和自动潮汐循环。
- 波浪强度和水的清澈度。
- 果冻柔软度。
- 昼夜光照。
- 各物种的显示开关。
- 暂停、重置，以及一个随机生成生态系统的按钮。

夜晚时，在水中和部分生物身上加入微妙的生物荧光。

使用优雅的编辑式字体排版、充足的留白和克制的 UI 样式。把 "Tidepool Jelly" 标题放在左上角，控件放在右侧。场景应占据屏幕主体。

使用 Three.js 构建一个完全可用的浏览器体验，在需要的地方使用自定义着色器。优先保证漂亮的水、可信的生物运动、有触感的果冻材质和流畅的性能。所有控件都必须可用。避免静态样稿、占位资源和过大的界面元素。
