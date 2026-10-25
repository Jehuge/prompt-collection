# 金库街 Vault Street

- **类型**：交互网页 / 像素风场景
- **技术栈**：three.js r160 · 像素后处理 · 单文件 HTML
- **标签**：`three.js` `像素风` `等距` `银行劫案` `vibe-coding` `ai-测试`
- **测试模型**：Claude Opus 5.5
- **来源**：[@vib3coded](https://x.com/vib3coded) · [原帖](https://x.com/vib3coded/status/2114054716959215724) · [提示词帖](https://x.com/vib3coded/status/2114054890011902110) · 2026-10-25（北京时间） · 试玩：[Claude Opus 5.5](https://claude.ai/artifact/4yCSrSvH2D5mqebPx6DNow)

> 说明：这是 [@vib3coded](https://x.com/vib3coded) 公开分享的提示词（测试模型见上）。界面上的按钮、标题、提示语等文字按原提示词要求保持英文（引号里的英文原样保留）。优先使用英文原文；中文翻译附在后面。

---

## 效果

![金库街 Vault Street](../assets/vault-street.jpg)

## 提示词（英文原文）

```text
Build a single-file, original pixel-art diorama called "Vault Street": a toy-like bank job on a floating isometric town block, rendered with three.js (r160) at low resolution and upscaled with a post shader (depth outlines, OKLab quantisation to a fixed 64-colour palette, optional Bayer dither, a "Raw 3D" toggle). Orthographic camera, drag to rotate, scroll to zoom, whole-pixel snapping. No weapons anywhere: cartoon robbers in striped shirts, beanies and eye masks.

World: a two-lane loop road (Main St / South St) with curbs, sidewalks, zebra crossings and a parking bay cut into the far side of South St. Inside the block: a columned bank ("ACORN SAVINGS") with a dome, a counter with three teller windows behind glass, a rope line, a manager's desk and a round vault door that rolls aside on a track; everything above knee height is one lid that lifts off while the gang are inside (Auto / Off / On). Also a diner and a park with a fountain. North of Main St: a police station with a beacon, a radio mast, a flag and a three-bay lot (two black-and-white cruisers with red/blue light bars, one impound bay), plus a donut shop with a giant donut on the roof and a hardware store. Street lamps with real lights at night, an alarm bell on a post by the bank, trees, a bus shelter. Day / dusk / night; rain with puddle reflections.

Story loop: a brown sedan waits in the bay → two robbers cross and go in → staff and customers put their hands up → one goes behind the counter and opens the vault → a teller trips the alarm (bell rings, station beacon turns) → four officers run to the cruisers; Car 21 heads for the bank, Car 22 goes the other way and turns across both lanes of Main St → robbers run out with "$" sacks, the sedan pulls out and flees round the block with banknotes fluttering from the boot, Car 21 in pursuit → the sedan stops at the roadblock; hands up, or one runs for the park and gets a flying tackle → cuffs, escorted to the station, the loot carried back through the bank's back door → the cruisers back into the lot, the sedan towed into the impound bay → later the gang make bail and drive back to the bay.

Traffic and people: civilian cars keep their distance (people crossing included), pull over for sirens and give up after a while if nothing passes; cruisers go out over the line to pass. Cars wait at a line while anyone reverses out of or pulls into the lot, and lot moves wait for an empty street. Passers-by walk the sidewalks, step round lamps, wait for cars crossing and sometimes use the bank. No deadlocks, no overlapping vehicles.

UI (English): a lit scoreboard (HEISTS · clock + status · ARRESTS, "LOOT RECOVERED $"), a rail with Time & weather, Bank roof, Units (Car 21, Car 22, Brown sedan, the bank with live status; "Start a heist", Pause, "Heists happen on their own"), a Radio log, View controls; click the bank to start a heist; a "How it's drawn" note. Responsive, light and dark themes.
```

---

## 提示词（中文）

构建一个单文件、原创的像素风微缩场景，名叫 "Vault Street"（金库街）：漂浮等距街区上的玩具感银行劫案，用 three.js（r160）低分辨率渲染，再用后处理着色器放大（深度描边、OKLab 量化到固定 64 色调色板、可选 Bayer 抖动，以及 "Raw 3D" 开关）。正交相机，拖动旋转，滚轮缩放，整像素对齐。全程没有武器：卡通劫匪穿着条纹衫、毛线帽和眼罩。

世界：双车道环形路（Main St / South St），有路缘、人行道、斑马线和南街远端切入的停车湾。街区内部：带廊柱的银行（"ACORN SAVINGS"）有穹顶，柜台后三扇玻璃出纳窗、绳索排队线、经理桌，以及一扇可沿轨道滚开的圆形金库门；膝盖以上整块屋顶盖在劫匪进银行时可以掀开（Auto / Off / On）。还有一家餐厅和一座带喷泉的公园。Main St 以北：派出所带信标、无线电桅杆、旗帜和三车位停车坪（两辆黑白巡逻车带红蓝灯条，一个扣押位），外加屋顶有巨型甜甜圈的甜甜圈店和一家五金店。夜景有真正发光的路灯，银行旁柱子上有警铃，还有树和公交候车亭。日 / 黄昏 / 夜；下雨时有水坑反射。

故事循环：棕色轿车等在停车湾 → 两名劫匪过马路进银行 → 员工和顾客举手 → 一人绕到柜台后打开金库 → 出纳触发警报（铃响，派出所信标转动） → 四名警察跑向巡逻车；Car 21 冲向银行，Car 22 反向开并横穿 Main St 双车道设卡 → 劫匪扛着 "$" 钱袋跑出，轿车驶出绕街区逃窜，钞票从后备箱飞出，Car 21 追击 → 轿车在路障前停下；举手投降，或一人冲向公园被飞扑绊倒 → 上手铐，押回派出所，赃款从银行后门送回 → 巡逻车倒回车位，轿车被拖进扣押位 → 稍后劫匪保释出来，又开回停车湾。

交通与行人：民用车保持距离（含过马路的行人），听到警笛会靠边，若长时间没车经过就放弃；巡逻车可以压线超车。有人倒出或驶入停车坪时，其他车在线前等候；停车坪内的移动等街道空了再动。路人走人行道，绕开路灯，等车过斑马线，偶尔进银行。没有死锁，车辆不重叠。

界面（英文）：亮着的记分牌（HEISTS · 时钟 + 状态 · ARRESTS，"LOOT RECOVERED $"）；侧栏有 Time & weather、Bank roof、Units（Car 21、Car 22、Brown sedan、银行实时状态；"Start a heist"、Pause、"Heists happen on their own"）、Radio log、View 控制；点击银行开始劫案；还有 "How it's drawn" 说明。响应式，浅色 / 深色主题。
