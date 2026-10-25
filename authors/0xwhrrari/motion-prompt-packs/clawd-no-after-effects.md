# 没有 After Effects No After Effects

- **类型**：motion / character film
- **技术栈**：HTML UI slabs · Puppeteer · Blender 5 · Cycles · Opus 5.5 · 12s · 30fps · 1920×1080
- **标签**：`motion` `blender` `html` `puppeteer` `opus-5.5` `clawd` `after-effects-style` `prompt-pack` `0xwhrrari`
- **来源**：[@0xwhrrari](https://x.com/0xwhrrari) · [原帖](https://x.com/0xwhrrari/status/2112166940081004693) · [PDF 回复](https://x.com/0xwhrrari/status/2112166943125872780) · [Google Drive](https://drive.google.com/file/d/1-VZJxR-VpR1rY4FyymcMDIq742fkQYLT/view) · [系列文章 Motion Engineering](https://x.com/i/article/2105626165704572928) · [系列帖](https://x.com/0xwhrrari/status/2105643919119696297) · PDF 2026-10-19

> 说明：粉丝整理自 [@0xwhrrari](https://x.com/0xwhrrari)（rari）公开的 Clawd Motion Lab / Opus 5.5 Prompt Pack。下面的英文是从原 PDF 抽出的 copy-ready 提示词，只把排版换行拼回句子，没有改词。优先使用英文原文；中文「译文」是简短说明（不是逐句翻译），附在英文提示词后面。Follow-up、逐帧时间轴和渲染步骤以同目录 PDF 为准。

## 效果

![clawd-no-after-effects](clawd-no-after-effects.jpg)

## 画面提示词（English）

Paste it as is into Claude Code running Opus 5.5 at effort high, with Blender 5, Node with puppeteer and ffmpeg installed. It writes the interface as HTML, the scene as Python, renders headless on the GPU and checks its own stills.

```text
BRAND
HERO: Clawd, the Claude Code mascot as one smooth toy: body 12x8x6 units, two side nubs, four short legs, two black eye slits, soft rounded bevels, no voxel grid, terracotta D97757
APP: a pixel-faithful After Effects-style workspace, dark theme: menu bar, toolbar (Home, Selection ... Rectangle, Pen, Type ... Puppet), Project, Composition, Info, Preview, Effects & Presets searched for "glow", and a Timeline with five layers and open Position and Scale rows. Real layout and labels, no logos
RESULT: the comp Clawd builds: "MADE WITH CLAUDE", an orange spark, a pen swoosh, a glow, the subtitle OPUS 5.5
SET: every panel is a floating slab over a dark warm studio; the UI glows like a screen
FORMAT: Blender 5 Python, Cycles GPU, 1920x1080, 30 fps, 12.0 s at 120 BPM. Build the interface in HTML and screenshot it with puppeteer into a 3840x2160 texture; draw the comp and the timecode on a canvas, one PNG per frame. One timeline.py holds the layout in UI pixels and every event; the HTML, the Blender scene and the sound all read it.
BEATS (seconds):
0-1.5 Clawd is a flat clawd.png layer in the comp, selection handles around him; he knocks twice from inside
1.5-2.0 peels off the screen as a flat card and pops into 3D; the viewer glass cracks, shards fly
2.5-3.5 lands on Type, Rectangle and Pen: each press types the title, pops the spark, draws the swoosh
4.5-5.5 flips across to Effects > Glow, a Glow chip pops up, he kicks it into the comp: glow on
6.0-7.5 four hops along the Position row; each stamps a keyframe and the comp jumps to that pose
8.0-9.6 hops on the playhead, it rewinds to 0, he surfs it to the end while the comp plays
10-12 Preview > Play; every other panel powers down and falls away; Clawd waves next to the finished comp
CAMERA: starts wide on the whole workspace, follows every hop at Clawd height with shallow focus, whips to each button, ends on the comp alone.
LOOK: UI as emission under black glossy glass; keep the lights out of the UI reflections so nothing blows out; bloom, 0.5 shutter blur, AgX; the body must read D97757.
CHECKS: render the UI texture and a comp contact sheet first, then 18 stills at half res before the full render.
```

## 声音提示词（English）

画面来自第 2 页的提示词；声音是同一份 timeline.py 再驱动的第二条提示词。

```text
Add sound. Synthesize everything in Python with numpy, scipy and pedalboard: no samples, no words. 48 kHz stereo WAV, 12.0 s, read every event from timeline.py and land each hit on its frame.
Music: a cute lo-fi beat at 120 BPM. Before the pop only a soft pad and ticking hats; the beat drops on the pop: kick, snare, hats, a rubbery bass on F G Am C, glassy FM keys on the off-beats, a kick pump on the bed. On Play a C major brass stab, then the chord rings out to a 0.5 s fade.
Effects: two glass knocks, a sticker peel, a pop with breaking glass and a sub boom; a boing on every take-off and a soft pomf on every landing, whooshes on the big leaps; a chunky keycap click and a UI blip on each tool, a key tap for every typed letter, a bloop for the spark, a pen scribble; a thwack for the kick, a whoosh for the chip and a magic shimmer with bells for the glow; rising glockenspiel dings C E G C for the keyframes; tape-rewind chirps, a skate roll and scrub ticks for the playhead; a power-down zap and a whoosh for each falling panel; yay chirps and sparkles at the end.
Master: a compressor and a limiter at -1 dBFS.
```

## 换皮示例（English，PDF 原文）

只改 BRAND 块。下面是 PDF 里给出的替换例子。

```text
BRAND (an example swap, not rendered)
HERO: the same
APP: a Premiere-style editor: Source, Program, Project bin, an Effects panel searched for "warp", a timeline with V1 V2 A1 tracks and clips
RESULT: a cut-down trailer: three clips snapped together, a title, a warp transition
SET: the same
```

## 译文

Clawd 一开始是合成窗口里的一张扁平 PNG。他从屏幕上揭下来，变成 3D，靠跳上按钮做完整条动态图形：Type、Rectangle、Pen、Glow、四个关键帧，再骑着播放头把成片播完。然后按 Play，其他面板一块块断电掉下去，只留下他做的画面。

## 原 PDF

[clawd-no-after-effects.pdf](clawd-no-after-effects.pdf)
