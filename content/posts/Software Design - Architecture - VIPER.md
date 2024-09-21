---
title: "Software Design - Architecture - VIPER"
date: 2024-01-19 21:05:00
draft: false

tags: ["Software Design", "Architecture"]
---

## 簡述
VIPER (View-Interactor-Presenter-Entity-Router)
- [iOS VIPER架構實踐(一)：從MVC到MVVM到VIPER](https://juejin.cn/post/6844903491941433351)
- [VIPER，更清晰的架构，解决复用和测试问题的利器系列1：VIPER架构演进史](https://blog.csdn.net/tyndale1993/article/details/80777324)

有很多種實作流派，下圖是我比較偏好的模式呈現

![VIPER](/images/VIPER.png)


VIPER 借鏡了 CA (Clean Architecture) 的思想為 MVC 提供一個新的設計方案
- Entity 對應原本的 Model
- Controller 責任過重 -> 將業務邏輯移至 Interactor 並提高重用性
- Controllers 之間耦合 -> 將導航邏輯移至 Router
- Presenter 作為 Binder 將 View / Interactor / Router 整合

## 啟發
VIPER 是筆者學習架構路上很重要的一個過渡，有以下兩點的思想轉變

### 顆粒度更細的單一職責
Interactor 封裝業務的概念在純 MVX 中是無法直接體會到，因此對之後學習 CA 時起了很大的緩衝，不然對於 Usecase 的設計應該會很不適應。

### 重視 Navigation
在學習 CA 中始終沒題到 feature/componet module 之間是如何互動的，也是在回頭複習 VIPER 時才重新意識到 Router 的重要性。當沒有特別規劃 Navigation 時很容易會造成 module 之間的耦合。

