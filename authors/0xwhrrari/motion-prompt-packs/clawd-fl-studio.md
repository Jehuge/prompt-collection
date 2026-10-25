# Clawd 做 FL Studio 打拍子 Cooks a Beat

- **类型**：motion / music production UI film
- **技术栈**：HTML UI · Puppeteer · Blender 5 · Cycles · Opus 5.5 · 32s · 30fps · 1920×1080 · 150 BPM
- **标签**：`motion` `blender` `html` `puppeteer` `opus-5.5` `clawd` `fl-studio` `music` `prompt-pack` `0xwhrrari`
- **来源**：[@0xwhrrari](https://x.com/0xwhrrari) · [原帖](https://x.com/0xwhrrari/status/2112536860769800658) · [PDF 回复](https://x.com/0xwhrrari/status/2112536865803014584) · [Google Drive](https://drive.google.com/drive/folders/1VUrPlM7bmyJjB_ylJzp_9y90gQV6Zskf) · [系列文章 Motion Engineering](https://x.com/i/article/2105626165704572928) · [系列帖](https://x.com/0xwhrrari/status/2105643919119696297) · PDF 2026-10-20

> 说明：粉丝整理自 [@0xwhrrari](https://x.com/0xwhrrari)（rari）公开的 Clawd Motion Lab / Opus 5.5 Prompt Pack。下面的英文是从原 PDF 抽出的 copy-ready 提示词，只把排版换行拼回句子，没有改词。优先使用英文原文；中文「译文」是简短说明（不是逐句翻译），附在英文提示词后面。Follow-up、逐帧时间轴和渲染步骤以同目录 PDF 为准。

## 效果

![clawd-fl-studio](clawd-fl-studio.jpg)

## 画面提示词（English）

Paste it as is into Claude Code running Opus 5.5 at effort high, with Blender 5, Node with puppeteer, ffmpeg and Python with numpy, scipy and pedalboard installed. It writes the interface as HTML, the scene and the beat as Python, renders headless on the GPU and checks its own stills.

```text
BRAND
HERO: Clawd, the Claude Code mascot as one smooth toy: body 12x8x6 units, two side nubs, four short legs, black eye slits, soft bevels, terracotta D97757. Three smaller subagent Clawds: the melodist in big headphones, the drummer in shades and a red sweatband, the bassist in a teal beanie with a pompom
APP: a faithful FL Studio-style dark workspace, no logos: menu and transport bar with tempo and song-position LCDs and a scope, Browser, Playlist with tracks and clips, a floating Channel rack with 16-step rows, a Piano roll, a Mixer with meters, faders and an FX chain, File > Export and the render dialog
RESULT: a 150 BPM trap/rage beat in F minor, built live: lead, drums, 808, build, drop
SET: every window is a floating slab over a dark warm studio; the UI glows like a screen
FORMAT: Blender 5 Python, Cycles GPU, 1920x1080, 30 fps, 32.0 s = 20 bars at 150 BPM, a seamless loop: frame 961 is frame 1. Build the interface as an HTML page and screenshot it with puppeteer once per frame into a 3840x2160 texture. One timeline.py holds the layout in UI pixels, the score in 16th steps and every hop; the HTML, the Blender scene and the audio all read it, so each landing hits on its step.
BEATS (seconds):
0-3.2 Clawd stands on clawd_beat.wav in the playlist while a filtered sample plays; on beats 1 to 3 of bar 2 he spawns three subagents, who leap to their windows
3.2-5.6 he mutes the sample; the melodist paints eight lead notes in the Piano roll, each sounding as it lands; Clawd adds Fruity Reverb 2
6.4-9.4 the drummer lights kick and clap steps, rides the hi-hat row with the playhead, then the open hat
9.6-12.4 the Piano roll switches to the 808; the bassist paints it, glides included
12.8-16 build: Clawd rides the Fruity Filter cutoff, the drummer hops a clap roll, the melodist wakes the Saw channel; all four leap into the drop
16-25.6 the drop: each subagent plays its part live by landing on every note and step as it sounds; Clawd bounces on the master fader
25.8-32 File > Export > Wave file, Start; the subagents dive back into Clawd as the bar fills; tape stop, File > New, he drags the fresh clawd_beat.wav into the empty playlist and stands on it, where the film began
LOOP: the exported beat is the sample the film opens on, filtered; the fresh project equals frame 1, and the playhead, the music and the camera all wrap.
CAMERA: follow the active Clawd at about 50 degrees, f/8, smoothed so hops do not shake the frame; wide only for the spawn and the drop; keep the whole export in one shot.
LOOK: UI as emission under dark glossy glass; keep the lights out of the UI reflections; orange and teal rims that pump with the kick in the drop; bloom, 0.5 shutter blur, AgX; the body must read D97757.
CHECKS: render the UI frames first and diff frame 960 against frame 1; then two dozen stills at half res as contact sheets, and fix the camera before the full render.
```

## 声音提示词（English）

画面来自第 2 页的提示词；节拍是同一份 timeline.py 再驱动的第二条提示词。

```text
Add the beat. Synthesize everything in Python with numpy, scipy and pedalboard: no samples, no words. 48 kHz stereo WAV, 32.0 s, a seamless loop: render three loops and keep the middle one. Read every event from timeline.py; a note or step sounds from the moment a subagent lands on it.
Music: 150 BPM trap/rage in F minor on Fm and Db. A bell pluck lead in a 3-3-2 rhythm; a punchy kick on steps 1, 7 and 11, a layered clap on 9, 808-style hi-hats with 32nd and triplet rolls, an open hat; a distorted 808 with a knock and two glides; a build with a clap roll, a noise riser and a lowpass that opens as Clawd rides the cutoff; a drop with detuned 7-voice supersaw stabs and the lead on supersaws, sidechained to the kick; a tape stop when the export ends. The opening sample is the drop itself, lowpassed with crackle.
Effects: pops and chimes for spawns and merges, clicks for every button, menu swishes, render ticks, a sweep for File > New, a whoosh for the dragged file.
Master: headroom into a gentle compressor and a limiter at -1.2 dBFS. Also write per-frame meter levels for the mixer.
```

## 换皮示例（English，PDF 原文）

只改 BRAND 块。下面是 PDF 里给出的替换例子。

```text
BRAND (an example swap, not rendered)
HERO: the same
APP: a Logic Pro-style workspace: Tracks area with regions, Library, Step Sequencer, Piano Roll, a Mixer with channel strips, Smart Controls, File > Bounce > Project and the Bounce dialog
RESULT: a 122 BPM lo-fi house groove: chords, four-on-the-floor, a walking bass, a filtered drop
SET: the same
```

## 译文

Clawd 站在 FL Studio 风格工程里的一段音频上，召出三个小号子代理。四个人靠落在真实控件上做一条 150 BPM 的 trap：钢琴卷帘里的旋律、通道机架上的鼓、808、滤波器推子。Drop 里他们跟着每一个音落地演奏。导出之后子代理合回 Clawd，File > New，他把刚导出的 clawd_beat.wav 拖进空播放列表，循环的开头就是这条采样。

## 原 PDF

[clawd-fl-studio.pdf](clawd-fl-studio.pdf)

参考成片里的合成节拍（同一 Drive 文件夹，约 1.3 MB）：[clawd_beat.mp3](clawd_beat.mp3)
