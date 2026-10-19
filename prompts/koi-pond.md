# 锦鲤池 Koi Pond

- **类型**：交互网页 / 俯视水面模拟
- **技术栈**：Three.js · WebGL · Web Audio
- **标签**：`threejs` `webgl` `水面模拟` `焦散` `锦鲤` `合成音效` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2108926847442378848) · [提示词帖](https://x.com/vib3coded/status/2108927154650038409) · 2026-10-10（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![锦鲤池 Koi Pond](../assets/koi-pond.jpg)

## 提示词（中文）

用 Three.js + WebGL 构建一个漂亮的全屏交互式锦鲤池。采用俯视视角，清澈的松石绿池水、阳光、池底的动态焦散，以及可信的纵深感。

在底部放一个优雅的半透明选择面板，里面有四种锦鲤：Kohaku（红白）、Showa（昭和三色）、Golden Ogon（黄金）和 Platinum（白金）。点击卡片会把那条鱼放进池塘。从卡片上拖出一条鱼，可以让用户精确选择放下的位置。

让每次入水都令人满足：带水滴的水花、水面短暂的凹陷，以及扩散的涟漪。然后鱼应潜入水面以下。使用折射和深度线索，让锦鲤看起来明显位于水下。

创建细致的 3D 锦鲤，有眼睛、鳞片、鳍和飘逸的尾巴。身体、尾巴和鳍的动画要协调一致。每条鱼应独立改变方向和速度，靠近边界时平滑转向，并避开其他鱼。

让用户可以在水面上触摸和拖动来产生涟漪。添加下雨和一个可移动的漩涡，漩涡的水流会影响鱼。包含 Calm（平静）、Clear pond（清空池塘），以及一个用于录屏时隐藏界面的控件。

用 Web Audio 生成入水水花声、柔和的音乐性水滴声、轻柔的游动水声、雨声和漩涡声。通过 Sound 按钮开启音频，静音时平滑淡出，浏览器标签页隐藏时暂停。

所有标签和按钮保持英文。布局对移动端响应式。优化渲染和动画，在几十条鱼时也保持流畅。

交付一个完整可用的网站，视觉精致、交互可用。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a beautiful, full-screen interactive koi pond using Three.js + WebGL. Use a top-down view with clear turquoise water, sunlight, animated caustics on the pond floor, and a convincing sense of depth.

Place an elegant translucent selection panel at the bottom with four koi varieties: Kohaku, Showa, Golden Ogon, and Platinum. Clicking a card releases that fish into the pond. Dragging a fish from its card lets the user choose exactly where to drop it.

Make each landing feel satisfying: a splash with droplets, a brief depression in the water surface, and expanding ripples. The fish should then dive beneath the surface. Use refraction and depth cues so the koi clearly look submerged.

Create detailed 3D koi with eyes, scales, fins, and flowing tails. Animate their bodies, tails, and fins together. Each fish should independently change direction and speed, turn smoothly near boundaries, and avoid other fish.

Let users touch and drag across the water to create ripples. Add rain and a movable whirlpool whose current affects the fish. Include Calm, Clear pond, and a control to hide the interface for screen recording.

Use Web Audio to create landing splashes, soft musical droplets, gentle swimming water sounds, rain, and a whirlpool sound. Enable audio through a Sound button, fade it smoothly when muted, and pause it when the browser tab is hidden.

Keep all labels and buttons in English. Make the layout responsive for mobile. Optimize rendering and animation for smooth performance with several dozen fish.

Deliver a complete, working website with polished visuals and functional interactions.
```

</details>
