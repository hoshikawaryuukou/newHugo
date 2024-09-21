---
title: "Unity - Basic - DontDestroyOnLoad"
date: 2023-03-20 21:11:00
draft: false

tags: ["Unity"]
---

## 用例
被標記為 DontDestroyOnLoad 的物件場景更改時不會被破壞。

1. 全域管理器：因為整個遊戲期間一直存在。例如，音效管理器、遊戲設定管理器或玩家數據管理器等物件可以在場景切換時保留，以確保它們的功能和數據在各個場景中持續存在。
2. 持久性數據：如果你有需要在多個場景中共享的持久性數據，可以將存儲這些數據的物件標記為  DontDestroyOnLoad。例如，玩家的遊戲進度或全域的配置設置等數據可以在場景切換時保留，以便在不同場景中訪問和更新。
3. UI 元素：某些UI元素，如遊戲狀態面板、計時器或得分顯示，可能需要在多個場景中保留。通過將這些UI元素物件標記為 DontDestroyOnLoad，可以確保它們在場景切換時不會被銷毀，以便在不同場景中持續顯示和更新。

## 問題
1. 記憶體管理問題：使用 DontDestroyOnLoad 將遊戲物件保留在多個場景中可能會導致記憶體洩漏。如果你的遊戲物件不再需要，但沒有被正確銷毀，它們將繼續存在於記憶體中，佔用系統資源，可能導致性能下降。
2. 場景管理問題：DontDestroyOnLoad 會打破場景之間的清晰界限。場景是 Unity 中組織和管理遊戲邏輯的基本單位，每個場景都應該是相對獨立的。通過在多個場景之間保持物件，會增加場景之間的耦合性，導致代碼難以維護和測試。

## Ref
- [Object.DontDestroyOnLoad](https://docs.unity3d.com/ScriptReference/Object.DontDestroyOnLoad.html)