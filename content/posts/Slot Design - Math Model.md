---
title: "Slot Design - Math Model"
date: 2024-09-09 21:11:00
draft: false

tags: ["Slot Design"]
---

## 使用馬可夫鏈來控制波動性

### 定義狀態 
每個狀態代表玩家一次 spin 後的結果。根據遊戲中的贏獎情況將這些狀態定義為:
- No Win (無贏)
- Small Win (小獎)
- Medium Win (中獎)
- Big Win (大獎)
- Free Game (免費遊戲)

### 設計轉換矩陣
| Current State \ Next State | No Win | Small Win | Medium Win | Big Win | Free Game |
| -------------------------- | ------ | --------- | ---------- | ------- | --------- |
| **No Win**                 | 0.70   | 0.20      | 0.05       | 0.03    | 0.02      |
| **Small Win**              | 0.50   | 0.30      | 0.10       | 0.05    | 0.05      |
| **Medium Win**             | 0.60   | 0.20      | 0.10       | 0.05    | 0.05      |
| **Big Win**                | 0.80   | 0.10      | 0.05       | 0.03    | 0.02      |
| **Free Game**              | 0.50   | 0.25      | 0.10       | 0.10    | 0.05      |

### 調整波動性 
要調整遊戲的波動性，可以對轉換矩陣進行修改：

- 高波動性：增加從 No Win 到 Big Win 或 Free Game 的轉換機率，但也要同時增加從 Big Win 回到 No Win 的機率。
- 低波動性：減少極端贏獎的概率，讓玩家經常小贏或中贏，而大獎發生的頻率很低。