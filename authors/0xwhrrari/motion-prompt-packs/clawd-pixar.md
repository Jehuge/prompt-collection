# Clawd 版皮克斯片头 Pixar to Clawd

- **类型**：motion / character film
- **技术栈**：Blender 5 · Cycles GPU · Opus 5.5 · 12s · 24fps · 1440p 渲染 / 1080p 交付 · 循环
- **标签**：`motion` `blender` `cycles` `opus-5.5` `clawd` `character-film` `prompt-pack` `0xwhrrari`
- **来源**：[@0xwhrrari](https://x.com/0xwhrrari) · [原帖](https://x.com/0xwhrrari/status/2113254058815582614) · [PDF 回复](https://x.com/0xwhrrari/status/2113254062468563280) · [Google Drive](https://drive.google.com/file/d/1FBkYiVOV7268zeJ1vPuTsQ_WLTaw_Mvr/view) · [系列文章 Motion Engineering](https://x.com/i/article/2105626165704572928) · [系列帖](https://x.com/0xwhrrari/status/2105643919119696297) · PDF 2026-10-22

> 说明：粉丝整理自 [@0xwhrrari](https://x.com/0xwhrrari)（rari）公开的 Clawd Motion Lab / Opus 5.5 Prompt Pack。下面的英文是从原 PDF 抽出的 copy-ready 提示词，只把排版换行拼回句子，没有改词。优先使用英文原文；中文「译文」是简短说明（不是逐句翻译），附在英文提示词后面。Follow-up、逐帧时间轴和渲染步骤以同目录 PDF 为准。

## 效果

![clawd-pixar](clawd-pixar.jpg)

## 画面提示词（English）

Paste it as is into Claude Code running Opus 5.5 at effort high, with Blender 5, Python (numpy, scipy, pedalboard, pillow) and ffmpeg installed. It models the letters from a font, rigs the lamp, animates everything in numpy, renders headless on the GPU and reads its own stills.

```text
BRAND
HERO: Clawd, the Claude Code mascot as one smooth toy: body 12x8x6 units, two side nubs, four short legs, two black eye slits, soft rounded bevels, terracotta D97757, 0.26 m wide
BAND: a famous animation-studio logo intro: a black void, a seamless satin floor, five big white extruded letters P I X A R standing on it, and a balanced-arm desk lamp (round base, two pairs of rods with springs, a conical shade with a bulb) that hops in and is the only practical light. No real logo files: our own heavy grotesque (Archivo Black), our own lamp
RESULT: the letters become C L A W D in terracotta with "ANIMATION STUDIOS" under them; the lamp gets switched off, sleeps through it, wakes up and hops off in a huff
SET: letters 0.42 m tall, 0.16 m deep, rounded bevels; the lamp's head level with the letter tops; the floor fades to black 3.8 m out, no horizon
FORMAT: Blender 5 Python, Cycles GPU, 2560x1440 rendered, 1920x1080 delivered, 24 fps (film rate, like the original), 12.0 s = 288 frames at 120 BPM (one beat = 12 frames), loops through black. One timeline.py holds every hop, swap and sound event in seconds; the scene and the sound both read it.
BEATS (seconds):
0-2 the logo intro, played straight: the lamp hops in from frame right, four hops along the floor in front of the letters, stops by the X and tilts its shade up at the I, a little nod
2.5-3 the lamp crouches to leap onto the I; Clawd drops from above the frame (his shadow first) and lands exactly on the push switch on the back of its shade: click, the light dies, the filament glows down
3.2-4.5 switched off, the lamp falls asleep under his weight: the joints fold, the shade comes to rest on the floor, he rides it down; push in: he looks down, then a slow head turn to the lens, the lamp's own beat; it snores. Rigid joints only, never squash the metal
4.5-7 he hops along the letter tops, one per beat; each landing squashes the letter and it pops back as the next letter of CLAWD (P to C, I to L, X to A, A to W, R to D), the pop launches him to the next; the neighbours slide to the new spacing; a front flip onto the D
7.3-8.5 he sits on the D, his eyes light up into two beams, they sweep the floor from right to left across the word, then turn into the lens: a flash
8.5-9.3 the end card: "ANIMATION STUDIOS" fades in under the word, happy eyes (the beam already made the sleeping lamp stir at 7.95)
9-11.5 the lamp twitches awake, unfolds with a clank, switches itself back on with a sputter, turns and glares up at Clawd, then hops off frame right in a huff; Clawd watches it go
11.5-12 fade to black; the first frame starts the hop-in again
CAMERA: the original's framing: low (0.4 m), centred, 35-38 mm, a slow dolly; push to 43 mm on the head turn; pull wide so the whole word stays in frame during all five swaps (you have to see it change); hold wide on the card.
LOOK: feature-animation lighting: the lamp spot as the key with a soft pool, a soft key 42 degree spread, faint top and fill, cool rims; white plaster letters, enamel lamp with steel rods; 0.5 shutter blur, f/3.2-5.6, AgX; Clawd measures D97757 on the lit body; leaps under 2.6 m/s.
CHECKS: 24 half-res stills as two contact sheets first, measure exposure (p99, clipped %) and the orange, then two full-res frames timed, then the full render.
```

## 声音提示词（English）

画面来自第 2 页的提示词；声音是同一份 timeline.py 再驱动的第二条提示词。

```text
Add sound. Synthesize everything in Python with numpy, scipy and pedalboard: no samples, no words, no borrowed melody. 48 kHz stereo WAV, 12.0 s, read every event from timeline.py, land each hit on its frame and pan it by where it happens.
Music, F major: soft strings and a tiptoe pizzicato (Karplus-Strong) with a celesta note on every lamp landing; two questioning celesta notes as it looks at the I; string tremolo while it crouches. Everything stops dead on the click: 1.4 s of near silence with one snore, one celesta ding on the head turn. Then a bouncy 120 BPM pizzicato bed on F Dm Bb C7 with a shaker, every letter pop plays the next note of C D E F G, a snare roll and a cymbal swell under the eye beams, and the full hit on the flash: timpani, crash, F major brass and strings, a celesta arpeggio on the card. A sad trombone (C B Bb A, the last one wobbling) as the lamp hops off.
Effects: spring sproings and small clanks on the lamp hops, a slide whistle for the fall, a chunky push-switch click with a falling power-down hum, a spring creak as it folds asleep and a snore, boings and squishes and bloops on every letter, a power-up whoom and hum for the beams, creaks, a click and a sputter as it wakes, a grumpy bassoon "hmph" for the glare.
Master: headroom first, then a gentle compressor and a limiter at -1.5 dBFS; aim for about -14 LUFS.
```

## 换皮示例（English，PDF 原文）

只改 BRAND 块。下面是 PDF 里给出的替换例子。

```text
BRAND (an example swap, not rendered)
HERO: the same
BAND: a famous film-studio intro: a night sky, clouds drifting past a tall golden title on a pedestal, searchlights sweeping; our own lettering, no logo files
RESULT: the searchlights catch Clawd climbing the title; every step he takes turns a letter terracotta until it reads his name
SET: the same rules: the title in frame for every swap, one swap per beat
```

## 译文

片头先按你记得的样子演两秒：台灯从右边跳进来，抬头看字母 I。Clawd 从画面上方落下，正好踩灭灯罩背后的开关。灯灭，台灯用关节睡着，他转头看镜头，再沿着五个字母一拍一个跳，把 PIXAR 换成同样五个字母的 CLAWD。眼睛打出光柱，片尾卡写出 ANIMATION STUDIOS。台灯醒来，瞪他一眼，气冲冲跳走，淡出后循环回到第一帧。

## 原 PDF

[clawd-pixar.pdf](clawd-pixar.pdf)
