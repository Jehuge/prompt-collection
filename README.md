# 提示词收集

收集我在视频里用过、实测能跑出效果的 AI 编程提示词（vibe coding）。每个提示词一个文件，优先收录英文原文，并附中文翻译，复制即可直接丢给 AI 使用。

## 声明

本仓库由粉丝整理，收集大神 [@vib3coded](https://x.com/vib3coded) 公开分享的 vibe coding / AI 测试提示词与效果展示，以及 [@0xwhrrari](https://x.com/0xwhrrari)（rari）公开分享的 Opus 5.5 motion 短片 Prompt Pack。

两位作者的作品都很多，分散在时间线上，一篇一篇找起来很费劲，所以整理成库，方便自己和大家学习、对照、复现。这里收录的提示词、效果图与 PDF，都尽量对应到原帖，方便溯源。

提示词、效果图与 PDF 均来自公开帖子或作者附上的公开网盘链接，版权归原作者所有。本仓库为非官方粉丝合集，不营利、不声称代表 [@vib3coded](https://x.com/vib3coded) 或 [@0xwhrrari](https://x.com/0xwhrrari) 本人。

我们尊重原作者。若作者或权利人认为本仓库收录内容构成侵权，请联系我们，我们会尽快下架相关内容。

作者主页：[@vib3coded](https://x.com/vib3coded) · [@0xwhrrari](https://x.com/0xwhrrari)

## 索引

| 名称 | 效果 | 类型 | 技术栈 | 文件 |
| --- | --- | --- | --- | --- |
| 发射果冻 Launch Jelly | ![launch-jelly](assets/launch-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · 单文件 HTML | [prompts/launch-jelly.md](prompts/launch-jelly.md) |
| 金库街 Vault Street | ![vault-street](assets/vault-street.jpg) | 交互网页 / 像素风场景 | three.js r160 · 像素后处理 · 单文件 HTML | [prompts/vault-street.md](prompts/vault-street.md) |
| 风向袋机场 Windsock Field | ![windsock-field](assets/windsock-field.jpg) | 交互网页 / 像素风场景 | three.js r160 · 像素后处理 · 飞行物理 · 单文件 HTML | [prompts/windsock-field.md](prompts/windsock-field.md) |
| 粉笔四方 Chalk Square | ![chalk-square](assets/chalk-square.jpg) | 交互网页 / 像素风场景 | three.js r160 · 像素后处理 · 球物理 · 单文件 HTML | [prompts/chalk-square.md](prompts/chalk-square.md) |
| 离岸果冻 Offshore Jelly | ![offshore-jelly](assets/offshore-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · 单文件 HTML | [prompts/offshore-jelly.md](prompts/offshore-jelly.md) |
| 海滩二号 Beach Two | ![beach-two](assets/beach-two.jpg) | 交互网页 / 3D 海滩场景 | WebGL / 单页网页玩具 | [prompts/beach-two.md](prompts/beach-two.md) |
| 像素冰场 Pixel Ice Rink | ![pixel-ice-rink](assets/pixel-ice-rink.jpg) | 交互网页 / 像素风场景 | WebGL · 单文件 HTML | [prompts/pixel-ice-rink.md](prompts/pixel-ice-rink.md) |
| 百香果果冻 Passion Fruit Jelly | ![passion-fruit-jelly](assets/passion-fruit-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML | [prompts/passion-fruit-jelly.md](prompts/passion-fruit-jelly.md) |
| 街角球场 Corner Court | ![corner-court](assets/corner-court.jpg) | 交互网页 / 3D 场景 | WebGL · 单文件 HTML | [prompts/corner-court.md](prompts/corner-court.md) |
| 毛绒龙虾 Plush Lobster | ![plush-lobster](assets/plush-lobster.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 | [prompts/plush-lobster.md](prompts/plush-lobster.md) |
| 西瓜果冻切割 Melon Jelly Cutters | ![melon-jelly-cutters](assets/melon-jelly-cutters.jpg) | 交互网页 / 可切割软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 刀具切割 | [prompts/melon-jelly-cutters.md](prompts/melon-jelly-cutters.md) |
| 喷泉果冻 Geyser Jelly | ![geyser-jelly](assets/geyser-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · 单文件 HTML | [prompts/geyser-jelly.md](prompts/geyser-jelly.md) |
| 桃子果冻 Peach Jelly | ![peach-jelly](assets/peach-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 刚体果核 · 单文件 HTML | [prompts/peach-jelly.md](prompts/peach-jelly.md) |
| 浅海 Ocean Shallows | ![ocean-shallows](assets/ocean-shallows.jpg) | 交互网页 / 3D 海洋模拟 | Three.js r128 · WebGL · 单文件 HTML | [prompts/ocean-shallows.md](prompts/ocean-shallows.md) |
| 毛绒鸽子 Plush Pigeon | ![plush-pigeon](assets/plush-pigeon.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · 布料 | [prompts/plush-pigeon.md](prompts/plush-pigeon.md) |
| 别墅果冻 Villa Jelly | ![villa-jelly](assets/villa-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · 刚体浮力 · 单文件 HTML | [prompts/villa-jelly.md](prompts/villa-jelly.md) |
| 毛绒鲨鱼 Plush Shark | ![plush-shark](assets/plush-shark.jpg) | 交互网页 / 软体物理玩具 | WebGPU · 软体物理 · 单文件 HTML | [prompts/plush-shark.md](prompts/plush-shark.md) |
| 毛绒鲸鱼 Plush Whale | ![plush-whale](assets/plush-whale.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · surface nets | [prompts/plush-whale.md](prompts/plush-whale.md) |
| 环礁果冻 Atoll Jelly | ![atoll-jelly](assets/atoll-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · boids · 单文件 HTML | [prompts/atoll-jelly.md](prompts/atoll-jelly.md) |
| 毛绒螃蟹 Plush Crab | ![plush-crab](assets/plush-crab.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · surface nets | [prompts/plush-crab.md](prompts/plush-crab.md) |
| 果冻锦鲤池 Jelly Koi Pond | ![jelly-koi-pond](assets/jelly-koi-pond.jpg) | 交互网页 / 果冻软体场景 | 3D（未指定库）· 程序化几何 · 单文件 HTML | [prompts/jelly-koi-pond.md](prompts/jelly-koi-pond.md) |
| 海盗果冻 Pirate Jelly | ![pirate-jelly](assets/pirate-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · 刚体 · 粒子系统 | [prompts/pirate-jelly.md](prompts/pirate-jelly.md) |
| 毛绒双髻鲨 Plush Hammerhead | ![plush-hammerhead](assets/plush-hammerhead.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · surface nets | [prompts/plush-hammerhead.md](prompts/plush-hammerhead.md) |
| 毛绒奶牛 Plush Cow | ![plush-cow](assets/plush-cow.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · WebAudio | [prompts/plush-cow.md](prompts/plush-cow.md) |
| 城堡果冻 Castle Jelly | ![castle-jelly](assets/castle-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · 浅水模拟 · SDF · 粒子烟花 | [prompts/castle-jelly.md](prompts/castle-jelly.md) |
| 毛绒枪鱼 Plush Marlin | ![plush-marlin](assets/plush-marlin.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · surface nets | [prompts/plush-marlin.md](prompts/plush-marlin.md) |
| 锦鲤池 Koi Pond | ![koi-pond](assets/koi-pond.jpg) | 交互网页 / 俯视水面模拟 | Three.js · WebGL · Web Audio | [prompts/koi-pond.md](prompts/koi-pond.md) |
| 潮池果冻 Tidepool Jelly | ![tidepool-jelly](assets/tidepool-jelly.jpg) | 交互网页 / 果冻海岸生态 | Three.js · 自定义着色器 · 正交相机 | [prompts/tidepool-jelly.md](prompts/tidepool-jelly.md) |
| 西瓜果冻 Melon Jelly | ![melon-jelly](assets/melon-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML | [prompts/melon-jelly.md](prompts/melon-jelly.md) |
| 毛绒企鹅 Plush Penguin | ![plush-penguin](assets/plush-penguin.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · 粒子布料 | [prompts/plush-penguin.md](prompts/plush-penguin.md) |
| 水块里的热带海湾 Tropical Cove | ![tropical-cove-water-block](assets/tropical-cove-water-block.jpg) | 交互网页 / 3D 水体微缩场景 | Three.js r160 · WebGL · GPU 波动方程 · 单文件 HTML | [prompts/tropical-cove-water-block.md](prompts/tropical-cove-water-block.md) |
| 柑橘果冻 Citrus Jelly | ![citrus-jelly](assets/citrus-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML | [prompts/citrus-jelly.md](prompts/citrus-jelly.md) |
| 螃蟹果冻 Crab Jelly | ![crab-jelly](assets/crab-jelly.jpg) | 交互网页 / 果冻生物 | WebGPU · XPBD 软体 | [prompts/crab-jelly.md](prompts/crab-jelly.md) |
| 柑橘果冻切割器 Citrus Jelly Cutters | ![citrus-jelly-cutters](assets/citrus-jelly-cutters.jpg) | 交互网页 / 可切割软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · SDF 布尔切割 | [prompts/citrus-jelly-cutters.md](prompts/citrus-jelly-cutters.md) |
| 港口果冻 Harbor Jelly | ![harbor-jelly](assets/harbor-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · boids · WebAudio | [prompts/harbor-jelly.md](prompts/harbor-jelly.md) |
| 猕猴桃果冻楔块 Kiwi Jelly Wedge | ![kiwi-jelly-wedge](assets/kiwi-jelly-wedge.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML | [prompts/kiwi-jelly-wedge.md](prompts/kiwi-jelly-wedge.md) |
| 涨潮时的鸟居 Torii at High Tide | ![torii-at-high-tide](assets/torii-at-high-tide.jpg) | 交互网页 / 3D 水体微缩场景 | Three.js r160 · WebGL · SSR · GPU 波动方程 | [prompts/torii-at-high-tide.md](prompts/torii-at-high-tide.md) |
| 瓶中船（体素） Voxel Ship in a Bottle | ![voxel-ship-in-a-bottle](assets/voxel-ship-in-a-bottle.jpg) | 交互网页 / 体素艺术场景 | WebGL（库不限）· 单文件 HTML | [prompts/voxel-ship-in-a-bottle.md](prompts/voxel-ship-in-a-bottle.md) |
| 船闸果冻 Lock Jelly | ![lock-jelly](assets/lock-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 多水体浅水模拟 · 角色动画 | [prompts/lock-jelly.md](prompts/lock-jelly.md) |
| 万圣节幽灵海盗船 Halloween Pirate Ship | ![halloween-pirate-ship](assets/halloween-pirate-ship.jpg) | 交互网页 / 3D 电影感场景 | Three.js · 单文件离线 HTML | [prompts/halloween-pirate-ship.md](prompts/halloween-pirate-ship.md) |
| 南瓜果冻 Pumpkin Jelly | ![pumpkin-jelly](assets/pumpkin-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML | [prompts/pumpkin-jelly.md](prompts/pumpkin-jelly.md) |
| 冰山果冻 Iceberg Jelly | ![iceberg-jelly](assets/iceberg-jelly.jpg) | 交互网页 / 果冻微缩场景 | WebGPU · WGSL · 浅水模拟 · 刚体冰块 · WebAudio | [prompts/iceberg-jelly.md](prompts/iceberg-jelly.md) |
| 整颗橙子果冻 Whole Orange Jelly | ![whole-orange-jelly](assets/whole-orange-jelly.jpg) | 交互网页 / 可切割软体果冻 | WebGPU · WGSL · XPBD 软体 · SDF 切割 · 体积渲染 | [prompts/whole-orange-jelly.md](prompts/whole-orange-jelly.md) |
| 菠萝果冻 Pineapple Jelly | ![pineapple-jelly](assets/pineapple-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 单文件 HTML | [prompts/pineapple-jelly.md](prompts/pineapple-jelly.md) |
| 果冻沙袋 Jelly Bag | ![jelly-bag](assets/jelly-bag.jpg) | 交互网页 / 软体物理玩具 | three.js r160 · WebGL2 · 形状匹配软体 · WebAudio | [prompts/jelly-bag.md](prompts/jelly-bag.md) |
| 南瓜测试 The Pumpkin Test | ![the-pumpkin-test](assets/the-pumpkin-test.jpg) | 交互网页 / 物理小游戏 | Three.js（内联打包）· 刚体碎裂 · Web Audio | [prompts/the-pumpkin-test.md](prompts/the-pumpkin-test.md) |
| 雾中喀斯特 Karst in the Mist | ![karst-in-the-mist](assets/karst-in-the-mist.jpg) | 交互网页 / 3D 水体微缩场景 | Three.js r160 · WebGL · SSR · 体积雾层 | [prompts/karst-in-the-mist.md](prompts/karst-in-the-mist.md) |
| 毛绒西瓜 Plush Watermelon | ![plush-watermelon](assets/plush-watermelon.jpg) | 交互网页 / 软体物理玩具 | WebGPU · XPBD 软体 · 壳层毛发 · 布料四肢 | [prompts/plush-watermelon.md](prompts/plush-watermelon.md) |
| 毛茸茸西瓜 Fluffy Watermelon | ![fluffy-watermelon](assets/fluffy-watermelon.jpg) | 交互网页 / 3D 毛发渲染 | three.js r147 · WebGL · 壳层毛发 + 针毛 | [prompts/fluffy-watermelon.md](prompts/fluffy-watermelon.md) |
| 花池 Bloom Pool | ![bloom-pool](assets/bloom-pool.jpg) | 交互网页 / 3D 泳池与漂浮花朵 | Three.js · WebGL · 自定义着色器 · Web Audio | [prompts/bloom-pool.md](prompts/bloom-pool.md) |
| 章鱼果冻 Octopus Jelly | ![octopus-jelly](assets/octopus-jelly.jpg) | 交互网页 / 果冻生物 | WebGPU · XPBD 软体 · 粒子链腕足 | [prompts/octopus-jelly.md](prompts/octopus-jelly.md) |
| 毛茸茸西瓜游乐场 Fluffy Watermelon Playground | ![fluffy-watermelon-playground](assets/fluffy-watermelon-playground.jpg) | 交互网页 / 可切割毛绒玩具 | three.js r147 · 壳层毛发 + 针毛 · 刚体物理 | [prompts/fluffy-watermelon-playground.md](prompts/fluffy-watermelon-playground.md) |
| 珊瑚泻湖 Reef Lagoon | ![reef-lagoon](assets/reef-lagoon.jpg) | 交互网页 / 俯视海洋模拟 | Three.js r128 · WebGL · 单文件 HTML | [prompts/reef-lagoon.md](prompts/reef-lagoon.md) |
| 春风站 Harukaze Station | ![harukaze-station](assets/harukaze-station.jpg) | 交互网页 / 低多边形微缩场景 | Three.js · MeshToonMaterial · OutlineEffect | [prompts/harukaze-station.md](prompts/harukaze-station.md) |
| 牛油果果冻 Avocado Jelly | ![avocado-jelly](assets/avocado-jelly.jpg) | 交互网页 / 软体果冻 | WebGPU · WGSL · XPBD 四面体软体 · 刚体果核 | [prompts/avocado-jelly.md](prompts/avocado-jelly.md) |

## @0xwhrrari · Motion Prompt Packs

[@0xwhrrari](https://x.com/0xwhrrari)（rari）的 Clawd Motion Lab 短片提示词，四条都带原 PDF。系列方法见 [Motion Engineering: Build a Video Studio Around Opus 5.5](https://x.com/i/article/2105626165704572928)（[原帖](https://x.com/0xwhrrari/status/2105643919119696297)）。文件在 [`authors/0xwhrrari/motion-prompt-packs/`](authors/0xwhrrari/motion-prompt-packs/)。

| 名称 | 效果 | 类型 | 技术栈 | 文件 |
| --- | --- | --- | --- | --- |
| Clawd 版皮克斯片头 Pixar to Clawd | ![clawd-pixar](authors/0xwhrrari/motion-prompt-packs/clawd-pixar.jpg) | motion / character film | Blender Cycles · Opus 5.5 · 12s · 24fps · 1440p | [clawd-pixar.md](authors/0xwhrrari/motion-prompt-packs/clawd-pixar.md) |
| 没有 After Effects No After Effects | ![clawd-no-after-effects](authors/0xwhrrari/motion-prompt-packs/clawd-no-after-effects.jpg) | motion / character film | HTML UI · Blender Cycles · Opus 5.5 · 12s · 30fps | [clawd-no-after-effects.md](authors/0xwhrrari/motion-prompt-packs/clawd-no-after-effects.md) |
| 霓虹跳跃 Neon Jump | ![clawd-neon-jump](authors/0xwhrrari/motion-prompt-packs/clawd-neon-jump.jpg) | motion / character film loop | Blender Cycles · Opus 5.5 · 14s 循环 · 30fps | [clawd-neon-jump.md](authors/0xwhrrari/motion-prompt-packs/clawd-neon-jump.md) |
| Clawd 做 FL Studio 打拍子 Cooks a Beat | ![clawd-fl-studio](authors/0xwhrrari/motion-prompt-packs/clawd-fl-studio.jpg) | motion / music production UI film | HTML UI · Blender Cycles · Opus 5.5 · 32s · 30fps | [clawd-fl-studio.md](authors/0xwhrrari/motion-prompt-packs/clawd-fl-studio.md) |

## 使用方式

1. 打开对应的提示词文件，优先复制「提示词（英文原文）」；需要中文时再复制后面的「提示词（中文）」。
2. 粘贴给你常用的 AI 编程工具（Cursor、Claude、ChatGPT、Grok 等）。
3. 生成后用浏览器直接打开 HTML 文件即可预览。

上面三步对应 [@vib3coded](https://x.com/vib3coded) 的交互网页提示词。

[@0xwhrrari](https://x.com/0xwhrrari) 的 motion Prompt Pack 在 [`authors/0xwhrrari/motion-prompt-packs/`](authors/0xwhrrari/motion-prompt-packs/)：优先复制英文提示词（画面 / 声音），贴给跑着 Opus 5.5 的 Claude Code（需要提示词里写明的 Blender、Python 或 ffmpeg）；中文译文附后仅作说明。同目录 PDF 是原件。系列说明见 [Motion Engineering](https://x.com/i/article/2105626165704572928)。

欢迎 Star，后续会持续更新更多提示词。
