# 毛绒螃蟹 Plush Crab

- **类型**：交互网页 / 软体物理玩具
- **技术栈**：WebGPU · XPBD 软体 · 壳层毛发 · surface nets
- **标签**：`webgpu` `xpbd` `软体模拟` `shell-fur` `sdf` `material-studies` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5 vs Claude Sonnet 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2108190478889824662) · [提示词帖](https://x.com/vib3coded/status/2108190686424039639) · 2026-10-08（北京时间）

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 用来横向测试 AI 模型的提示词（同一提示词交给 Claude Opus 5.5 vs Claude Sonnet 5.5）。提示词里提到的「Material Studies 毛绒系列」是作者此前同系列的作品，源码未公开；没有原作时可让 AI 按文中描述从头搭建。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![毛绒螃蟹 Plush Crab](../assets/plush-crab.jpg)

## 提示词（英文原文）

```text
Create a self-contained interactive WebGPU page "Plush Crab" in the existing Material Studies plush series
(No. 020, fig. 20), matching the series' editorial layout: serif masthead, specimen control panel, live
readouts, collapsible "Inside the experiment" notes, English UI, works on mobile, graceful no-WebGPU fallback.

THE TOY: a cute plush crab sitting on a studio table. A wide, puffy domed shell with a flat seat and a soft
brow; two eyes on short stalks, each a fuzzy eyeball with a round white felt patch and a glossy safety eye;
an embroidered smile and soft blush cheeks; pale spots scattered over the top of the shell; a paler
underside; stitched seams where legs are sewn on. Real-time shell-texture fur (many shells, alpha-to-coverage,
MSAA) that lags behind jiggles and can be combed. Palettes: Coral (default), Sand, Blue (with red claw tips).

BODY: one SDF meshed with surface nets, simulated as an XPBD soft body (hex lattice, shape matching +
tetrahedral volume) under gravity and friction; it breathes, rights itself, can be grabbed, squashed,
lifted and thrown, and lands softly.

LEGS AND CLAWS: eight walking legs and two arms are rods with a plastic "wire" inside — posed toward
blended targets (sit, stand, hide, wave, hang), and bent legs keep the new shape until "Straighten".
Each arm ends in a chunky claw with two fat fingers that hang from the arm tip in the claw's own frame;
opening and closing is a single angle. Legs get pale joint bands and toes; claw fingers get dark tips.

BEHAVIOUR: "Scuttle" walks sideways (keeps its side to the goal) with an alternating gait and footholds;
"Snip snip" raises both claws and snaps them a beat apart (count snips in a readout); "Hide" pulls the legs in
and covers its eyes with the claws, then peeks out; "Wave claws" raises them high. With the Finger tool it
scuttles toward a held-out finger, turns to face it, reaches with its claws and gives a gentle pinch (toast);
poking the shell makes it hide. Held up in the air, legs dangle and paddle. Idle: small scuttles, snips, waves.

CONTROLS: tools Hand / Finger / Comb; sliders Stuffing, Pile, Wire; buttons Scuttle, Snip snip, Hide,
Wave claws, Straighten, Smooth fur, Reset; ¼ speed, Mesh, Pause. Readouts: Mass, Volume (% of rest),
Steps, Snips. Single HTML file, no external models or textures.
```

---

## 提示词（中文）

创建一个自包含的交互式 WebGPU 页面 "Plush Crab"（毛绒螃蟹），属于现有的 Material Studies 毛绒系列（No. 020，fig. 20），匹配该系列的编辑式布局：衬线刊头、标本控制面板、实时读数、可折叠的 "Inside the experiment" 说明，界面为英文，支持移动端，没有 WebGPU 时优雅降级。

### 玩具本体

一只坐在摄影棚桌面上的可爱毛绒螃蟹。宽大、鼓鼓的圆顶蟹壳，带平坦的"座面"和柔软的眉骨；两只长在短眼柄上的眼睛，每只是一个毛茸茸的眼球，配圆形白色毛毡贴片和有光泽的安全眼；绣出来的微笑和柔和的腮红；蟹壳顶部散布浅色斑点；腹面颜色更浅；腿缝上去的地方有缝线。实时壳层纹理毛发（多层壳、alpha-to-coverage、MSAA），晃动时会滞后，并且可以梳理。配色：Coral（珊瑚色，默认）、Sand（沙色）、Blue（蓝色，配红色钳尖）。

### 身体

一个 SDF，用 surface nets 生成网格，模拟为 XPBD 软体（六面体晶格，形状匹配 + 四面体体积），受重力和摩擦作用；它会呼吸、自己翻正，可以被抓住、压扁、举起和扔出，并柔软地落地。

### 腿和钳子

八条步足和两只螯臂是内含塑料"铁丝"的杆——朝混合目标姿势摆放（坐、站、躲、挥手、悬挂），弯过的腿会保持新形状，直到按下 "Straighten"（拉直）。每只螯臂末端是一只粗壮的钳子，两根胖胖的钳指在钳子自己的坐标系中从臂端垂下；开合由单一角度控制。腿上有浅色关节环和脚尖；钳指尖端为深色。

### 行为

- "Scuttle"：横着走（保持侧面朝向目标），交替步态并有落脚点；
- "Snip snip"：举起两只钳子，相隔一拍地开合（在读数中统计 snips 次数）；
- "Hide"：把腿收进来，用钳子捂住眼睛，然后偷看；
- "Wave claws"：把钳子高高举起挥动。
- 使用 Finger 工具时，它会横着爬向伸出的手指，转身面对它，用钳子够过去轻轻夹一下（弹出提示 toast）；戳蟹壳会让它躲起来。被举到空中时，腿会悬垂并划动。空闲时：小段横爬、开合钳子、挥手。

### 控制

工具 Hand / Finger / Comb；滑块 Stuffing（填充）、Pile（绒毛）、Wire（铁丝硬度）；按钮 Scuttle、Snip snip、Hide、Wave claws、Straighten、Smooth fur、Reset；¼ speed、Mesh、Pause。读数：Mass、Volume（静止体积的百分比）、Steps、Snips。单个 HTML 文件，不使用外部模型或纹理。
