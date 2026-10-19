# 毛茸茸西瓜游乐场 Fluffy Watermelon Playground

- **类型**：交互网页 / 可切割毛绒玩具
- **技术栈**：three.js r147 · 壳层毛发 + 针毛 · 刚体物理
- **标签**：`threejs` `webgl` `shell-fur` `切割` `刚体` `毛绒玩具` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2111829421040488960) · [提示词帖](https://x.com/vib3coded/status/2111829905553969329) · 2026-10-18（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来测试 AI 模型的提示词（帖子展示的是 Claude Opus 5.5 的结果）。这是在 [fluffy-watermelon](fluffy-watermelon.md) 基础上的升级版（作者让 Claude Opus 5.5 在原作上继续加功能），但提示词本身是完整独立的。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。英文原文附在文末。

---

## 效果

![毛茸茸西瓜游乐场 Fluffy Watermelon Playground](../assets/fluffy-watermelon-playground.jpg)

## 提示词（中文）

构建一个名为 "Fluffy Watermelon Playground"（毛茸茸西瓜游乐场）的单文件自包含 HTML 页面（无构建步骤）：一个交互式 3D 玩具，一个毛茸茸的大西瓜可以被一把可见的刀切成任意多块毛茸茸的碎块，这些碎块可以像有弹性的毛绒玩具一样被抓住、拖动和扔来扔去。使用 three.js r147（UMD：https://cdn.jsdelivr.net/npm/three@0.147.0/build/three.min.js）配合自定义 ShaderMaterial。所有界面文字为英文。字体：Onest（Google Fonts），配系统字体回退。

### 外观

- 全屏 canvas，西瓜果肉粉色摄影棚背景：竖直渐变 #ECB3AB → #F7CFC7（屏幕中部一条更亮的带）→ #E8A9A0。
- 西瓜：沿 X 轴躺着的长椭球（半长 1.38，半径 0.98），钝圆桶状两端，两端各有小凹窝，腹部略平，细微凹凸。一小截干枯带棱的果柄残桩，切口是浅色隆起圆盖，外加一根细细的螺旋卷须。
- 毛下面的瓜皮颜色：浅绿 #A8D66B，带 16 条从果柄延伸到花蒂的深绿色（#1C4D1C）条纹，边缘参差呈手指状（正弦蜿蜒 + value noise），底部有一块浅奶油色地斑。
- 一盏来自左上前方的平行光：包裹漫反射，沿毛发切线的 Kajiya-Kay 各向异性高光，毛根更暗，每根毛亮度略有变化。

### 毛发（必须清晰锐利，绝不能模糊）

- 毛长 0.2 单位。毛发沿法线长出，然后从果柄端梳向花蒂端并沿两侧垂下（两端呈放射状，没有旋涡），带重力、空闲微风，以及跟随碎块旋转的滞后/摆动。
- 底绒：约 64 层实例化的表面壳层，只延伸到毛长的 50%。UV 空间中程序化毛发单元，默认视角下约 3.4 个设备像素大小，两类毛发（长毛 + 细底绒），在尖端聚成一缕缕，解析抗锯齿覆盖率，alpha 混合，壳层写入深度。每根毛取其根部的颜色，所以条纹保持清晰。在瓜皮上，侧向看到的地方让壳层淡出并丢弃微弱片元（轮廓处没有点状边缘）。
- 针毛：约 90,000 根独立的、逐渐变细的、面向相机的条带（实例化，7 段），遵循相同的弯曲函数，最小宽度约 0.75 px，从根部起可见。绘制两次：在壳层之前和之后（开启深度测试，不写深度）。
- 始终以设备完整像素比渲染（最大 2），绝不降低。如果帧率慢，先减少壳层数量（最低到 32），再减少针毛数量。

### 切割（碎块数量不限）

- 一个 "Knife" 开关按钮（右上）。开启刀具后，光标变成一把可见的 3D 主厨刀：带弧形刀尖的钢刃、钢制刀枕、带三颗铆钉的深色木柄，用 Phong 材质照明。它跟随指针，略位于碎块前方。刀尖指向你挥动的方向（向左或向右），向下切时略微下沉；刀刃始终朝下，所以刀永远不会上下颠倒。刀背向观众倾斜。每次挥动后面跟着一条渐隐的白色轨迹。
- 一次挥动定义一个切割平面，该平面包含挥动线和视线方向。它切开刀刃在屏幕上经过的每一块（必须真正把碎块切开，而不是擦过）。最多 24 块，每块最多 8 刀。按 Esc 放下刀。
- 每块碎块 = 原始西瓜几何体 + 一组裁切平面（全部通过 uniform 在着色器中丢弃）、过滤到它那一侧的瓜皮三角形和针毛，以及每个切过它的平面对应的一个毛茸茸切面。
- 切面：通过对解析的身体形状做光线步进（128 个角度）找到横截面轮廓，构建一个极坐标圆盘网格，并把它向外**延伸**一圈，跨过瓜皮毛发的厚度（0.11 单位），这样从侧面看时，切面毛发和瓜皮毛发之间不会露出空隙。较早切出的面会被较新的平面修剪。
- 内部颜色每切一刀就绘制一次到一张 384×384 纹理中：深红色瓜心 #E62640 过渡到 #FD666B，带颗粒感，浅色瓜皮带，薄薄的绿色外皮，跨过毛发厚度的一圈深绿色边，以及瓜子：在约 60% 半径处的壳面上绕长轴排成 16 行，黑色，夹杂几颗浅色的。
- 切面毛发使用同样的壳层 + 针毛技术，密度与瓜皮上一样，针毛在底绒的下方和上方都绘制，并且底绒在掠射角下保持可见（只有完全侧向时才淡出），使毛发永远不会悬浮在一块光秃秃的板上。毛发颜色取自每根毛根部的果肉贴图。
- 新的两半继承父块的运动，外加一个轻柔的分开推力和一个小跳。果柄留在包含它的那一块上。

### 物理（毛绒玩具）

- 重力 22，隐形桌面，一个大圆形场地（半径 6.5），在地面上显示为一圈淡淡的环；边缘有一道柔软的圆形围栏。每帧 3 个子步。
- 每块碎块是一个刚体：质心、包围半径、质量 ∝ R³、用于接触的采样点（瓜皮 + 切面）。在最深点处与地面接触，重击时恢复系数 0.5，带摩擦、位置校正，静止后休眠。
- 碎块之间永远不会互相穿透：用每块的采样点测试另一块的实际形状（解析身体半径 + 它的所有裁切平面，为毛发留 0.07 的余量）。在最多 4 个最深接触点上用冲量求解（恢复系数 0.45），包含角运动效应和位置校正，双向处理。
- 毛绒式挤压与拉伸：受到撞击时（地面、围栏、其他碎块），碎块沿撞击方向以撞击侧为支点被压扁，然后用阻尼弹簧（k=160，c=7）弹回，保持体积；高速飞行时沿速度方向略微拉长。作为单独的包装变换施加，使物理本身保持刚体。
- 不拿刀时：拖动一块碎块来搬运它（它沿一个面向相机的平面移动，会推开其他碎块）；移动中松手，以最近约 90 ms 的速度把它扔出去（上限 30），并加上翻滚。拖动空白背景让相机绕桌面环绕；滚轮或双指缩放；方向键环绕。
- 每块碎块下方有柔和的接触阴影，随高度变大并变淡。
- 相机自动跟随所有碎块的中心并拉远，使每块都保持在画面中。

### UI 与健壮性

- 右上："Knife" 开关和 "New watermelon"（第一刀之后出现；落下一个新的完整西瓜）。左下："Fluffy Watermelon" 和一行随模式变化的提示（"Drag a piece to throw it · Drag the background to look around · Press Knife to slice" / "Swipe across the watermelon to slice it · Esc puts the knife down" / "Missed. Swipe right across a piece."），并针对触屏设备调整。刀关闭时使用自定义 46 px 圆环光标。
- 防范加载时容器尺寸为零（把宽/高钳制为 ≥1），并在每一帧从任何非有限的相机或物体状态中恢复。
- 如果 WebGL 上下文丢失或着色器编译失败，显示一条小提示；WebGL 不可用时显示降级信息。遵守 prefers-reduced-motion（没有微风）。

---

<details>
<summary>英文原文（English original）</summary>

```text
Build a single self-contained HTML page (no build step) called "Fluffy Watermelon Playground": an interactive 3D toy where a big, furry watermelon can be sliced with a visible knife into as many furry pieces as you like, and the pieces can be grabbed, dragged and thrown around like springy plush toys. Use three.js r147 (UMD: https://cdn.jsdelivr.net/npm/three@0.147.0/build/three.min.js) with custom ShaderMaterials. All UI text in English. Font: Onest (Google Fonts) with system fallbacks.

LOOK
- Full-screen canvas on a watermelon-flesh pink studio background: vertical gradient #ECB3AB → #F7CFC7 (lighter band mid-screen) → #E8A9A0.
- Watermelon: oblong ellipsoid lying along X (half-length 1.38, radius 0.98), blunt barrel-like ends, small dimples at both ends, slightly flattened belly, subtle bumps. Short dried ribbed stem stub with a pale domed cut cap, plus a thin curly helical tendril.
- Rind colour under the fur: light green #A8D66B with 16 dark green (#1C4D1C) stripes running stem to blossom, with ragged finger-like edges (sine meander + value noise), plus a pale cream field spot on the underside.
- One directional light from upper-left-front: wrap diffuse, Kajiya-Kay anisotropic highlight along the hair tangent, darker roots, slight per-hair brightness variation.

FUR (must look crisp, never blurry)
- Fur length 0.2 units. Hairs grow along the normal, then comb from the stem end toward the blossom end and drape down the flanks (radial at the ends, no whorls), with gravity, an idle breeze, and lag/sway that trails the piece's spin.
- Undercoat: ~64 instanced shells of the surface reaching only 50% of fur length. Procedural hair cells in UV space sized to ~3.4 device pixels at the default view, two populations (long + fine underfur), locks that clump toward the tips, analytic anti-aliased coverage, alpha blended, shells write depth. Each hair takes the colour of its own root, so stripes stay crisp. On the rind, fade shells out where seen edge-on and discard faint fragments (no dotted rim at the outline).
- Guard hairs: ~90,000 individual tapered camera-facing ribbons (instanced, 7 segments) that follow the same bend function, minimum width ~0.75 px, visible from the root. Draw them twice: before the shells and after them (depth-tested, no depth write).
- Always render at the full device pixel ratio (max 2), never lower it. If frames are slow, first reduce the shell count (down to 32), then the guard-hair count.

SLICING (unlimited pieces)
- A "Knife" toggle button (top right). With the knife on, the cursor becomes a visible 3D chef's knife: steel blade with a curved tip, steel bolster, dark wooden handle with three rivets, lit with Phong materials. It follows the pointer slightly in front of the pieces. The tip points the way you swipe (left or right) and dips a little when cutting downward; the cutting edge always faces down, so the knife is never upside down. The spine leans toward the viewer. A white fading trail follows each swipe.
- A swipe defines a cutting plane containing the swipe line and the view direction. It cuts every piece the blade passes over on screen (it must really split the piece, not graze it). Up to 24 pieces, up to 8 cuts per piece. Esc puts the knife down.
- Every piece is the original melon geometry plus a list of clip planes (all of them discarded in the shaders via uniforms), the rind triangles and guard hairs filtered to its side, and one furry cut face per plane it was cut by.
- Cut face: find the cross-section outline by ray-marching the analytic body shape (128 angles), build a polar disc mesh, and EXTEND it by one extra ring across the thickness of the rind's fur (0.11 units), so no empty gap shows between the cut fur and the rind fur when viewed from the side. Faces from older cuts are trimmed by newer planes.
- Inside colour is painted once per cut into a 384×384 texture: deep red core #E62640 blending to #FD666B, grainy, pale rind band, thin green skin, a dark green rim across the fur thickness, and seeds: 16 rows around the long axis on a shell at ~60% of the radius, black with a few pale ones.
- Cut-face fur uses the same shell + guard-hair technique, as dense as on the rind, guard hairs drawn under and over the undercoat, and the undercoat stays visible at grazing angles (fade only when exactly edge-on) so the hairs never float above a bare slab. Hair colour comes from the flesh map at each hair's root.
- New halves inherit the parent's motion plus a gentle push apart and a little hop. The stem stays with whichever piece contains it.

PHYSICS (plush toy)
- Gravity 22, invisible table, big round arena (radius 6.5) shown as a faint ring on the floor; a soft round fence at its edge. 3 substeps per frame.
- Each piece is a rigid body: centre of mass, bounding radius, mass ∝ R³, sample points (rind + cut faces) for contacts. Floor contacts at the deepest points with restitution 0.5 on hard hits, friction, positional correction, sleep when settled.
- Pieces never pass through each other: test every piece's sample points against the other piece's actual shape (analytic body radius + all its clip planes, padded 0.07 for the fur). Resolve with impulses at up to 4 deepest contacts (restitution 0.45), angular effects, and positional correction, both directions.
- Plush squash & stretch: on impacts (floor, fence, other pieces) the piece flattens along the hit direction with a pivot on the hit side and springs back with a damped spring (k=160, c=7), volume preserved; it stretches slightly along its velocity when flying fast. Applied as a separate wrapper transform so physics stays rigid.
- Without the knife: drag a piece to carry it (it follows a plane facing the camera, pushes other pieces away); release while moving to throw it with the speed of the last ~90 ms (cap 30), adding tumble. Drag the empty background to orbit the camera around the table; wheel or pinch zooms; arrow keys orbit.
- Soft contact shadow under each piece that grows and fades with height.
- The camera automatically follows the centre of all pieces and pulls back so every piece stays in frame.

UI & ROBUSTNESS
- Top right: "Knife" toggle and "New watermelon" (appears after the first cut; drops a fresh whole melon). Bottom left: "Fluffy Watermelon" and a hint that changes with the mode ("Drag a piece to throw it · Drag the background to look around · Press Knife to slice" / "Swipe across the watermelon to slice it · Esc puts the knife down" / "Missed. Swipe right across a piece."), adapted for touch devices. Custom 46 px ring cursor when the knife is off.
- Guard against a zero-sized container at load (clamp width/height to ≥1) and recover from any non-finite camera or body state every frame.
- Show a small note if the WebGL context is lost or a shader fails to compile; a fallback message if WebGL is unavailable. Respect prefers-reduced-motion (no breeze).
```

</details>
