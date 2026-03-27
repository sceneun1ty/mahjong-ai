# 🀄 Mahjong AI — 川麻 AI 出牌助手

> **拍照发牌，秒出建议，防放炮听最宽。**
>
> **Snap a photo of your hand. Get instant discard advice. Stay safe, maximize waits.**

AI-powered Sichuan Mahjong (川麻 / 血战到底 / Bloody End) assistant. Send a photo of your tiles, and get optimal discard recommendations in under a second — powered by computer vision and mahjong algorithms.

**[OpenClaw](https://openclaw.ai) Skill** — The first mahjong AI on [ClawHub](https://clawhub.ai)

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 📸 **Tile Recognition** | AI vision identifies tiles from photos — dots (筒), bamboo (条), characters (万) |
| 🧮 **Shanten Calculation** | How many tiles away from ready/tenpai (向听数) |
| 🎯 **Tenpai Analysis** | Which tiles you're waiting for + how many remain in the wall |
| 💡 **Discard Recommendation** | Which tile to discard, ranked by wait width and efficiency |
| 🛡️ **Safety Scoring** | 🟢 Safe / 🟡 Caution / 🔴 Danger — avoid dealing into others (防放炮) |
| 🏆 **Special Hands** | Detects flush (清一色), seven pairs (七对), dragon seven (龙七对), all triplets (对对胡) |
| 🎲 **Dingque Advice** | Which suit to declare missing at the start of each round |
| 🔄 **Swap-3 Strategy** | Best 3 tiles to swap after declaring your missing suit |
| 🔍 **Opponent Prediction** | Predict what opponents are building from their discards |

## 🎮 Sichuan Mahjong Rules (川麻 / Xuezhan Daodi)

- **Tiles**: Only 筒 (dots), 条 (bamboo), 万 (characters) — 108 tiles total, no winds or dragons
- **Hand**: 13 tiles per player (draw to 14, then discard)
- **No Chi (吃)**: Only Pon (碰/pong), Kan (杠/kong), Win (胡/hu)
- **Blood War (血战到底)**: Play continues after someone wins — last player standing loses biggest
- **Special Hands**: 清一色 flush, 七对 seven pairs, 龙七对 dragon seven, 对对胡 all triplets

## 📦 Installation

### As an OpenClaw Skill
```bash
# Via ClawHub (coming March 21, 2026)
clawhub install mahjong-ai

# Via Git
git clone https://github.com/sceneun1ty/mahjong-ai.git
cp -r mahjong-ai ~/.openclaw/workspace/skills/
```

### Standalone Usage
```bash
# Analyze a hand (14 tiles = discard advice)
python3 scripts/mahjong_analyze.py \
  --hand "1m,2m,3m,5m,5m,3p,4p,7p,8p,9p,2s,3s,4s,6s" \
  --discard "1p,2p,5p,5p,9s,9s"

# Dingque advice (which suit to drop)
python3 scripts/mahjong_analyze.py \
  --hand "1m,3m,5m,2p,3p,4p,5p,7p,8p,1s,2s,9s,9s" \
  --mode dingque

# Swap-3 strategy
python3 scripts/mahjong_analyze.py \
  --hand "1m,3m,5m,2p,3p,4p,5p,7p,8p,1s,2s,9s,9s" \
  --mode swap3

# Predict opponent's strategy
python3 scripts/mahjong_analyze.py \
  --discard "1m,3m,5m,7m,9m,2m,8m,1p,3s" \
  --mode predict --player "上家"
```

## 🎯 Example Output

```
🀄 手牌（14张）：[万] 1万 2万 3万 5万 5万 [筒] 3筒 4筒 7筒 8筒 9筒 [条] 2条 3条 4条 6条

🗑️ 场上已出（6张）

🎯 出牌建议：
=========================================================
⭐ 打 6条  🟡40  → 听 2筒(3) 5筒(2) (5张)
   打 5万  🟡55  → 听 5筒(3) (3张)
   打 1万  🟢60  → 1向听

💡 建议打 6条 — 听5张最多
```

## 📂 Project Structure

```
mahjong-ai/
├── SKILL.md                    # OpenClaw skill definition
├── DEVLOG.md                   # Development log (Chinese)
├── scripts/
│   └── mahjong_analyze.py      # Core analysis engine (~460 lines)
├── references/
│   ├── mahjong_theory.md       # Sichuan mahjong theory & strategy
│   └── tile_visual_guide.md    # Visual tile identification guide
└── README.md
```

## 🔧 Tile Encoding

| Suit | Code | Example | Chinese |
|------|------|---------|---------|
| 万 (Characters) | `m` | `1m` = 一万 | 万子 |
| 筒 (Dots) | `p` | `5p` = 五筒 | 筒子 |
| 条 (Bamboo) | `s` | `9s` = 九条 | 条子 |

## 📊 Test Results

- ✅ 10 random hands: shanten calculation 100% correct
- ✅ 5 special scenarios: all detected (qingyise, qidui, duiduihu)
- ✅ Real game replay: correctly identified 清一色+杠 win
- ✅ Analysis speed: <1 second

## 🛣️ Roadmap

### ✅ Completed
- [x] Core analysis engine
- [x] Dingque advice
- [x] Swap-3 strategy  
- [x] Opponent prediction
- [x] ClawHub official release 🎉

### 🌏 Other Mahjong Variants — Coming Soon
- [ ] 🇯🇵 Riichi Mahjong (日麻/リーチ麻雀) — Japanese rules with riichi, dora, yaku scoring
- [ ] 🇭🇰 Hong Kong Mahjong (港麻/香港麻雀) — Cantonese rules with winds, dragons, flowers
- [ ] 🇨🇳 Guobiao Mahjong (国标麻将) — Chinese national competition standard (MCR)
- [ ] 🇨🇳 Guangdong Mahjong (广东麻将) — Cantonese variant with chicken hand rules

## 🤝 How It Works with OpenClaw

1. 📸 **Snap** — Take a photo of your mahjong hand and send it to your OpenClaw assistant
2. 👁️ **Recognize** — AI vision identifies every tile in your hand
3. 🧠 **Analyze** — The algorithm calculates shanten, waits, and optimal discards
4. ⚡ **Advise** — Get a ranked recommendation in under 1 second

Works on any OpenClaw-connected platform: WhatsApp, Telegram, Discord, and more.

## 📄 License

MIT

## 👤 Author

**Kevin Liu** ([@sceneun1ty](https://github.com/sceneun1ty))

Built with 🦞 [OpenClaw](https://openclaw.ai) + Claude Opus 4

---

_🀄 The first Sichuan Mahjong AI on ClawHub. Snap, analyze, win. 拍照发牌，秒出建议。_
