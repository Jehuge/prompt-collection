# 毛茸茸西瓜 Fluffy Watermelon

- **类型**：交互网页 / 3D 毛发渲染
- **技术栈**：three.js r147 · WebGL · 壳层毛发 + 针毛
- **标签**：`threejs` `webgl` `shell-fur` `毛发渲染` `kajiya-kay` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs Gemini 4 Argon
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111501344750059978) · [提示词帖](https://x.com/vib3coded/status/2111502058608050536) · 2026-10-18（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs Gemini 4 Argon）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![毛茸茸西瓜 Fluffy Watermelon](../assets/fluffy-watermelon.jpg)

## 提示词（中文）

构建一个单文件自包含 HTML 页面（无构建步骤），展示一个覆盖着长毛的交互式 3D "Fluffy Watermelon"（毛茸茸西瓜），使用 three.js r147 以 WebGL 渲染（UMD 版本：https://cdn.jsdelivr.net/npm/three@0.147.0/build/three.min.js）。所有界面文字为英文。

### 场景与外观

- 全屏 canvas，背景是柔和的西瓜果肉粉色摄影棚：竖直渐变 #ECB3AB → #F7CFC7（中间一条更亮的带）→ #E8A9A0，用作场景背景。
- 一个大的长椭圆西瓜沿 X 轴侧躺：半长 1.38，半径 0.98，钝圆桶状的两端，两端各有小凹窝，腹部略平，表面有细微的凹凸。初始为 3/4 视角（绕 Y 约 -0.32 rad，倾斜 0.1 rad），相机 FOV 30°，取景使西瓜占画面高度约 80%。
- 毛下面的瓜皮花纹：浅绿色（#A8D66B），带 16 条从果柄延伸到花蒂的深绿色（#1C4D1C）条纹，条纹边缘参差呈手指状（正弦蜿蜒 + value noise），底部还有一块浅奶油色的"地斑"（field spot）。每根毛取其根部的颜色，因此条纹透过毛发依然清晰。
- 一端有一小截干枯、带棱的果柄残桩，切口是略微隆起的浅色圆盖，旁边还冒出一根细细的螺旋卷须。
- 一盏来自左上前方的平行光，包裹漫反射（wrap diffuse），沿毛发切线方向的 Kajiya-Kay 各向异性高光，毛根更暗（按毛发高度遮挡），每根毛的亮度略有变化。

### 毛发（最重要：必须清晰锐利，绝不能模糊）

- 毛长 0.2 单位。毛发沿法线长出，然后弯曲：从果柄端梳向花蒂端，沿两侧垂下（两端不要有旋涡），外加轻微重力。
- 底绒：用约 64 层实例化的身体网格壳层做壳层纹理（shell texturing），只延伸到毛长的 50%。在 UV 空间中程序化生成毛发单元（密度缩放到默认视角下一个单元约 3.4 个设备像素），两类毛发（长毛 + 细底绒），毛发在尖端聚成一缕缕，解析抗锯齿覆盖率，alpha 混合，壳层写入深度。在表面被侧向看到的地方让壳层淡出并丢弃微弱的片元，这样轮廓处不会出现点状边缘。
- 针毛（guard hairs）：约 90,000 根独立的、逐渐变细的、面向相机的条带状发丝（实例化，每根 7 段），遵循完全相同的弯曲函数，最小宽度约 0.75 px 以保持锐利。绘制两次：一次在壳层之前，一次在壳层之后（开启深度测试），使微弱的边缘毛发永远不会遮住它们，它们始终清晰地覆盖在最上面。
- 始终以设备完整像素比渲染（上限为 2），**绝不**为了性能降低它。如果帧率慢，先减少壳层数量（最低到 32），再减少针毛数量。

### 交互

- 拖动可自由旋转（轨迹球风格），甩动后带惯性。毛发通过阻尼弹簧滞后于旋转，然后弹回。空闲时毛发中有轻柔的微风；3 秒无输入后，开始缓慢自动旋转。
- 鼠标滚轮 / 双指缩放（平滑推拉）。双击或按 "0" 以缓动动画复位。方向键旋转。
- 自定义光标：原生的抓手光标加上一个跟随指针的 46 px 细深色圆环，拖动时缩小。悬停时会轻轻拨开光标下方的毛，就像在抚摸它。
- 遵守 prefers-reduced-motion（不自动旋转，没有微风）。

### UI 与健壮性

- 左下说明："Fluffy Watermelon" 和一行提示 "Drag to rotate · Scroll to zoom · Double-click to reset"（触屏设备上为 "Drag to rotate · Pinch to zoom"），首次交互后淡出。字体：Google Fonts 的 Onest，配系统字体回退。
- 防范加载时容器尺寸为零：把宽/高至少钳制为 1，并在每一帧从任何非有限的相机距离或旋转状态中恢复。
- 如果 WebGL 上下文丢失或着色器编译失败，在页面上显示一条小提示；如果 WebGL 不可用，显示降级信息。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single self-contained HTML page (no build step) showing an interactive 3D "Fluffy Watermelon" covered in long fur, rendered with WebGL using three.js r147 (UMD build: https://cdn.jsdelivr.net/npm/three@0.147.0/build/three.min.js). All UI text in English.

SCENE & LOOK
- Full-screen canvas on a soft watermelon-flesh pink studio background: vertical gradient #ECB3AB → #F7CFC7 (lighter band in the middle) → #E8A9A0, used as the scene background.
- A big oblong watermelon lying on its side along the X axis: half-length 1.38, radius 0.98, blunt barrel-like ends, small dimples at both ends, slightly flattened belly, subtle surface unevenness. Start in a 3/4 view (about -0.32 rad around Y, 0.1 rad tilt), camera FOV 30°, framed to fill ~80% of the height.
- Rind pattern under the fur: light green (#A8D66B) with 16 dark green (#1C4D1C) stripes running stem to blossom, with ragged finger-like edges (sine meander + value noise), plus a pale cream "field spot" on the underside. Each hair takes the colour of its own root, so the stripes stay crisp through the fur.
- A short, dried, ribbed stem stub at one end with a slightly domed pale cut cap, and a thin curly helical tendril springing from beside it.
- One directional light from upper-left-front, wrap diffuse, Kajiya-Kay anisotropic highlight along the hair tangent, darker roots (occlusion by hair height), slight per-hair brightness variation.

FUR (most important: it must look crisp, never blurry)
- Fur length 0.2 units. Hairs grow out along the normal, then bend: combed from the stem end toward the blossom end and draped down the flanks (no whorls at the ends), plus slight gravity.
- Undercoat: shell texturing with ~64 instanced shells of the body mesh that reach only 50% of the fur length. Procedural hair cells in UV space (density scaled so one cell is ~3.4 device pixels at the default view), two hair populations (long + fine underfur), hairs gathering into locks toward their tips, analytic anti-aliased coverage, alpha blending, shells write depth. Fade shells out where the surface is seen edge-on and discard faint fragments, so no dotted rim appears at the outline.
- Guard hairs: ~90,000 individual tapered, camera-facing ribbon strands (instanced, 7 segments each) that follow exactly the same bend function, with a minimum width of ~0.75 px so they stay sharp. Draw them twice: once before the shells and once after (depth-tested), so faint edge fur never hides them and they always lie crisply on top.
- Always render at the device's full pixel ratio (capped at 2) and NEVER lower it for performance. If frames are slow, reduce the shell count first (down to 32), then the guard-hair count.

INTERACTION
- Drag to rotate freely (trackball style) with inertia after a flick. The fur lags behind the rotation through a damped spring and flops back. Gentle idle breeze in the fur; after 3 s without input, a slow auto-turn.
- Mouse wheel / pinch to zoom (smooth dolly). Double-click or "0" resets with an eased animation. Arrow keys rotate.
- Custom cursor: the native grab hand plus a thin dark 46 px ring that follows the pointer and shrinks while dragging. Hovering gently parts the fur under the cursor, as if stroking it.
- Respect prefers-reduced-motion (no idle spin, no breeze).

UI & ROBUSTNESS
- Bottom-left caption: "Fluffy Watermelon" and a hint "Drag to rotate · Scroll to zoom · Double-click to reset" (on touch devices: "Drag to rotate · Pinch to zoom") that fades after the first interaction. Font: Onest from Google Fonts with system fallbacks.
- Guard against a zero-sized container at load: clamp width/height to at least 1 and, every frame, recover from any non-finite camera distance or rotation state.
- Show a small on-page note if the WebGL context is lost or a shader fails to compile, and a fallback message if WebGL is unavailable.
```

</details>
