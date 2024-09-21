---
title: "Algorithm - Sampling - Alias Method"
date: 2024-08-04 13:11:00
draft: false

tags: ["Algorithm"]
---

別名方法是一種眾所周知的演算法，用於從任意離散機率分佈中進行恆定時間採樣，該演算法依賴於簡單的預先計算的查找表。

## Guide
- [Alias Method: 非均匀随机抽样算法](https://blog.csdn.net/rover2002/article/details/106760664)
- [Darts, Dice, and Coins: Sampling from a Discrete Distribution](https://www.keithschwarz.com/darts-dice-coins/)
- [Weighted Random: algorithms for sampling from discrete probability distributions](https://zliu.org/post/weighted-random/)
- [mackysoft/Choice](https://github.com/mackysoft/Choice?tab=readme-ov-file#speed-measurement)
- [jgrapht-core/src/main/java/org/jgrapht/alg/util/AliasMethodSampler.java](https://github.com/jgrapht/jgrapht/blob/master/jgrapht-core/src/main/java/org/jgrapht/alg/util/AliasMethodSampler.java)

務必先觀看
- 第一篇文章的漸進思考與核心精神
- 第二篇文章最後的 Vose's Alias Method 圖解

## Example
給定的權重 `[0.1, 0.2, 0.3, 0.4]`。

### **按均值縮放權重**：
- 均值為 : 0.25
- 縮放後的權重：`[0.4, 0.8, 1.2, 1.6]`

### **分類權重到 large 和 small 隊列**：
- 初始狀態：`small = [], large = []`
- 權重 `0.4` 小於 1，放入 `small`：`small = [0]`
- 權重 `0.8` 小於 1，放入 `small`：`small = [0, 1]`
- 權重 `1.2` 大於 1，放入 `large`：`large = [2]`
- 權重 `1.6` 大於 1，放入 `large`：`large = [2, 3]`

### **構建別名表**：
- 初始狀態：
  - probs = [0.4, 0.8, 1.2, 1.6]
  - aliases = [null, null, null, null]
  - small = [0, 1]
  - large = [2, 3]

- 處理 small[0] = 0, large[0] = 2：
  - `aliases[0] = 2`
  - `probs[2] = 1.2 + 0.4 - 1 = 0.6`
  - `small.shift() -> small = [1]`
  - 再次分類 `probs[2] < 1` 放入 `small`

- 更新狀態：
  - probs = [0.4, 0.8, 0.6, 1.6]
  - aliases = [2, null, null, null]
  - small = [1, 2]
  - large = [3]

- 處理 small[0] = 1, large[0] = 3：
  - `aliases[1] = 3`
  - `probs[3] = 1.6 + 0.8 - 1 = 1.4`
  - `small.shift() -> small = [2]`
  - 再次分類，`probs[3] > 1` 放回 `large`

- 更新狀態：
  - probs = [0.4, 0.8, 0.6, 1.4]
  - aliases = [2, 3, null, null]
  - small = [2]
  - large = [3]

- 處理 small[0] = 2, large[0] = 3：
  - `aliases[2] = 3`
  - `probs[3] = 1.4 + 0.6 - 1 = 1.0`
  - `small.shift() -> small = []`
  - `large.shift() -> large = []`

- 現在所有 small, large 隊列均已空，構建完成。

### **結果**：
- 最終權重：`probs = [0.4, 0.8, 0.6, 1.0]`
- 最終別名：`aliases = [2, 3, 3, null]`

### **操作**：
- 第一個隨機值 i 用於選擇權重索引。
- 第二個隨機值 r 用於決定是否使用別名。
- case ( i = 3 ) : 
  - aliases[3] 為 null，採樣結果為 3
- case ( i = 1, r = 0.6 ) :
  - aliases[1] 非 null，且 r < probs[1]，採樣結果為 1
- case ( i = 1, r = 0.9 ) :
  - aliases[1] 非 null，且 r > probs[1]，採樣結果為 3 (aliases[1])

## Summary
| **`probs`**          | **`alias`**              | **`small`** | **`large`** |
| -------------------- | ------------------------ | ----------- | ----------- |
| [0.4, 0.8, 1.2, 1.6] | [null, null, null, null] | [0, 1]      | [2, 3]      |
| [0.4, 0.8, 0.6, 1.6] | [2, null, null, null]    | [2]         | [1, 3]      |
| [0.4, 0.8, 0.6, 1.4] | [2, 3, null, null]       | [2]         | [3]         |
| [0.4, 0.8, 0.6, 1.0] | [2, 3, 3, null]          | -           | -           |
