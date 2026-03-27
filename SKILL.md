---
name: mahjong-ai
description: >
  AI Mahjong Assistant — Sichuan Mahjong (川麻) tile recognition and strategy advisor.
  Send a photo of your mahjong hand, get instant discard recommendations, tenpai/shanten analysis,
  safety scoring, and special hand detection. Supports Sichuan rules (血战到底 Bloody End / Xuezhan Daodi).
  Keywords: mahjong, 麻将, 川麻, tiles, discard, tenpai, shanten, tile recognition, mahjong AI,
  strategy, hand analysis, photo recognition, dots, bamboo, characters, 筒, 条, 万.
  Use when: user sends a mahjong hand photo, asks for mahjong strategy, tile analysis,
  discard advice, shanten calculation, or tenpai analysis.
---

# 麻将 AI 助手 🀄

川麻（四川麻将）AI 出牌顾问。拍照发手牌，分析最优出牌。

## 规则：川麻（血战到底）
- 只有 **筒、条、万** 三门，共 108 张（每种 1-9 各 4 张）
- 每人 **13 张**手牌，摸牌后 14 张选择出牌
- 胡牌条件：4 组面子（顺子/刻子）+ 1 对将（雀头）
- 特殊胡法：七对、龙七对、清一色、对对胡等
- 血战到底：一人胡了继续打，直到剩一人没胡

## 工作流程

### Step 1: 识别牌面（拍照）
收到照片后，用视觉识别：
1. **手牌**（13或14张）
2. **场上已打出的牌**（牌池/河牌）
3. **已碰/杠的牌**

编码格式：
- 万子：1m 2m ... 9m
- 筒子：1p 2p ... 9p
- 条子：1s 2s ... 9s

列出识别结果让用户确认后再分析。

### Step 2: 运行分析
```bash
python3 scripts/mahjong_analyze.py \
  --hand "1m,2m,3m,5m,5m,3p,4p,7p,8p,9p,2s,3s,4s,6s" \
  --discard "1p,2p,5p,5p,9s,9s" \
  --meld "6m,6m,6m"
```

参数：
- `--hand` / `-H`：手牌（必填，13或14张）
- `--discard` / `-d`：场上已打出的牌（可选）
- `--meld` / `-m`：已碰/杠的牌（可选）

### Step 3: 输出建议
- 14张 → 推荐打哪张，附安全度🟢🟡🔴 + 听牌张数
- 13张 → 显示听什么牌 + 剩余张数
- 安全度基于场面已出牌计算（出越多越安全、19边张更安全）

## 川麻特殊规则
- **不能吃**，只能碰/杠/胡
- 血战到底：一人胡了继续打
- 番数：清一色4番、七对4番、龙七对8番、对对胡2番

## 参考
- 详细牌理：见 `references/mahjong_theory.md`

## 🌏 Other Mahjong Variants — Coming Soon

Currently supports **Sichuan Mahjong** (川麻). Future versions will add:

- 🇯🇵 **Riichi Mahjong** (日麻) — Japanese competitive mahjong with riichi, dora, and yaku
- 🇭🇰 **Hong Kong Mahjong** (港麻) — Cantonese rules with winds, dragons, and flowers
- 🇨🇳 **Guobiao / MCR** (国标麻将) — Chinese national competition standard
- 🇨🇳 **Guangdong Mahjong** (广东麻将) — Cantonese variant

Want a specific variant? Open an issue on [GitHub](https://github.com/sceneun1ty/mahjong-ai)!
