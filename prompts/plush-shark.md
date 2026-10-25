# 毛绒鲨鱼 Plush Shark

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · 软体物理 · 单文件 HTML
- **标签**：`webgpu` `软体模拟` `毛绒玩具` `创意编程` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs ChatGPT-6 Astra
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2107773295676227691) · [提示词帖](https://x.com/vib3coded/status/2107773609288646875) · 2026-10-07（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs ChatGPT-6 Astra）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![毛绒鲨鱼 Plush Shark](../assets/plush-shark.jpg)

## 提示词（英文原文）

```text
Build a single-file WebGPU interactive experience featuring a soft, squishy plush shark.

Design the shark with a recognizable silhouette: a rounded body, pointed snout, dorsal fin, side fins, and a powerful tail. Give it a blue fabric exterior, cream belly, glossy black button eyes, stitched gills, and a playful mouth with small felt teeth. Make the fabric visibly fuzzy, with subtle seams and soft shadows.

Interactions:
- Grab and drag any part of the shark. Its body should stretch, squash, wobble, and settle naturally.
- Pull its tail and release to make it dash forward.
- Boop its nose for a cute reaction.
- Brush its fur with a comb tool.
- Feed it little fish and animate it chasing and eating them.
- Let it swim in gentle circles when idle.

Use convincing soft-body physics with volume preservation, springy recovery, and responsive fins and tail. Avoid rigid movement or excessive jitter.

Include controls for stuffing firmness, fur length, swimming speed, and color palettes. Add reset, feed, dash, and wireframe buttons.

Present everything in a polished minimalist interface with a warm off-white background, elegant typography, a compact settings panel, and the title “Plush Shark.”

Deliver one self-contained HTML file with all code and assets embedded. Use WebGPU for rendering, support mouse and touch, and keep the experience smooth and responsive.
```

---

## 提示词（中文）

构建一个单文件 WebGPU 交互体验，主角是一只柔软、可以捏的毛绒鲨鱼。

把鲨鱼设计成辨识度高的轮廓：圆滚滚的身体、尖吻、背鳍、侧鳍和有力的尾巴。外表是蓝色布料，奶油色肚皮，有光泽的黑色纽扣眼睛，缝线鳃纹，以及一张带着小小毛毡牙齿的俏皮嘴巴。布料要有明显的绒毛感，带细微的缝线和柔和的阴影。

### 交互

- 抓住并拖动鲨鱼的任何部位。身体应自然地拉伸、压扁、晃动，然后平静下来。
- 拉住尾巴再松开，让它向前冲刺。
- 轻点（boop）它的鼻子，触发可爱的反应。
- 用梳子工具梳理它的毛。
- 喂它小鱼，并做出它追逐和吃鱼的动画。
- 空闲时让它缓缓绕圈游动。

使用可信的软体物理：保持体积、有弹性的回复，鳍和尾巴反应灵敏。避免僵硬的运动或过度抖动。

提供以下控制项：填充硬度、毛长、游动速度和配色方案。添加重置（reset）、喂食（feed）、冲刺（dash）和线框（wireframe）按钮。

用精致的极简界面呈现一切：暖白色背景、优雅的字体排版、紧凑的设置面板，标题为 "Plush Shark."。

交付一个自包含 HTML 文件，所有代码和资源都内嵌其中。用 WebGPU 渲染，支持鼠标和触摸，保持体验流畅、响应迅速。
