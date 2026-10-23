# 霓虹跳跃 Neon Jump

- **类型**：motion / character film loop
- **技术栈**：Blender 5 · Cycles GPU · Opus 5.5 · 14s 无缝循环 · 30fps · 1920×1080
- **标签**：`motion` `blender` `cycles` `opus-5.5` `clawd` `neon` `loop` `prompt-pack` `0xwhrrari`
- **来源**：[@0xwhrrari](https://x.com/0xwhrrari) · [原帖](https://x.com/0xwhrrari/status/2111804745853894843) · [PDF 回复](https://x.com/0xwhrrari/status/2111804749347475488) · [Google Drive](https://drive.google.com/file/d/1nZYifpY8AqiXFbcpBX1avbVLpj0nzHuZ/view) · [系列文章 Motion Engineering](https://x.com/i/article/2105626165704572928) · [系列帖](https://x.com/0xwhrrari/status/2105643919119696297) · PDF 2026-10-17

> 说明：粉丝整理自 [@0xwhrrari](https://x.com/0xwhrrari)（rari）公开的 Clawd Motion Lab / Opus 5.5 Prompt Pack。下面的英文是从原 PDF 抽出的 copy-ready 提示词，只把排版换行拼回句子，没有改词。中文「译文」是简短说明，不是逐句翻译。Follow-up、逐帧时间轴和渲染步骤以同目录 PDF 为准。

## 效果

![clawd-neon-jump](clawd-neon-jump.jpg)

## 译文

体素吉祥物把一辆红色敞篷跑车开过霓虹隧道，冲进高楼峡谷，把像素墨镜翻下来，从坡道飞过断开的桥。空中只放慢距离、不改重力，时钟慢到 6%。落地砸在节拍上，火花溅开，下一截隧道就是第一帧。整段 14 秒无缝循环。

## 画面提示词（English）

Paste it as is into Claude Code running Opus 5.5 at effort high, with Blender 5 and ffmpeg installed. It writes the scene as Python, renders it headless on the GPU and checks its own stills.

```text
BRAND
HERO: voxel mascot 18x10, body 12x8 at (3,0), arms 2x2 at (1,4) (15,4), legs 1x2 at x 4 6 11 13 row 8, eye slits 0F0F0F 1x2 at (5,2) (12,2), 6 deep, beveled, orange D97757
RIDE: open roadster, low wedge nose, full-width tail light, candy red 6B0A0F clearcoat, three hidden rear thrusters, orange underglow
PROP: pixel "deal with it" shades, white glints, parked on HERO's head
SET: neon tunnel through a megastructure, then a highway in a night canyon of towers, kicker ramp, missing bridge span, wet asphalt
SIGNS: "CLAUDE CODE" on the tunnel wall, giant pixel-HERO billboard, ROAD CLOSED gantry
PALETTE: cyan 14B4FF, magenta FF1A78, ring FF6124, sodium FFB873, sky 0D0612
FORMAT: Blender 5 Python, Cycles GPU, 1920x1080, 30 fps, 14.0 s seamless loop: the world repeats every period P so frame 420 hands off to frame 1. One timeline.py drives picture and sound; 137.14 BPM, 8 bars = 14 s.
BEATS (s):
0 HERO drives at the lens through the tunnel, shades up, rings rushing past
2.1 bursts out into the canyon
4.75 hits the ramp; 4.95 shades flip down
5.25 launch on the beat: thrusters fire, speed ramps to 6% slow-mo
6.0 arc over the gap, arms up, slight roll, billboard behind
8.75 slam on the beat: suspension dips, sparks, camera shake
12.1 shades flip back up; 12.57 into the next tunnel = frame 1
CAMERA: one take locked to the car: front low 3/4, swing wide at the exit, chase on the ramp, orbit over the canyon, front low for the slam, settle on the opening offset.
LOOK: puddles mirror the neon, mist fog, bloom, slight dispersion, shallow DOF on HERO, 0.5 shutter blur; a soft fill rides with the car so the face reads D97757.
CHECKS: preview 9 beat stills at half res before the full render; eyes readable in every front shot; frame 420 to 1 no bigger a jump than any neighbour.
```

## 声音提示词（English）

画面是 Blender 场景；声音是同一份 timeline.py 再驱动的第二条提示词，全部用 numpy 合成。

```text
Add sound. Synthesize everything in Python with numpy, scipy and pedalboard: no samples, no voices, no words. 48 kHz stereo WAV, 14.0 s, read every event from timeline.py and land each hit on its frame. Render three loops and keep the middle one so every tail wraps into the start.
Music: a dark action trap cue at 137.14 BPM in D minor, 8 bars that loop. 808 on the root with glides, hard kick, clap snare on 3, hats with rolls into bar ends, a 16th-note pluck ostinato in a 3-3-2 accent. Bar 3 builds: snare roll, filter sweep, riser into the lip. On the launch a low BRAAAM, then slow-mo: everything low-passed, a pad, heartbeat kicks, a reverse cymbal into the landing. The beat drops back on the slam.
Car: an engine whose pitch follows the speed and dives in the slow-mo, a thin electric whine, a whup for each tunnel ring and tunnel reverb only while inside. Whooshes on the camera swings, a clunk on the ramp, a shing for the shades, a jet roar for the thrusters, a squeaky wheee from HERO, then the slam: sub boom, metal crunch, spark crackle, a short tyre screech.
Master loud, like a trailer: glue compressor and a limiter at -1 dBFS.
```

## 换皮示例（English，PDF 原文）

只改 BRAND 块。下面是 PDF 里给出的替换例子。

```text
BRAND
HERO: your mascot as a pixel grid from its logo, its hex colors
RIDE: voxel hover-bike, white F2F0EA panels, cyan 2EC5D3 vents, two jet pods
PROP: a scarf that flaps behind it, mint 7FD8B6
SET: snowy mountain pass at dawn, an ice tunnel, a broken rope bridge over a gorge
SIGNS: your logo carved in a glacier wall, trail markers
PALETTE: dawn FFC9A8, ice 9FD7F0, rock 3C3A45, snow F6F7FA, sun FF8E5C
```

## 原 PDF

[clawd-neon-jump.pdf](clawd-neon-jump.pdf)
