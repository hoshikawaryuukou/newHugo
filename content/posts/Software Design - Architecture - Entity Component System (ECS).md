---
title: "Software Design - Architecture - Entity Component System (ECS)"
date: 2024-01-19 21:05:00
draft: true

tags: ["Software Design", "Architecture"]
---

## Ref
- [漫谈Entity Component System (ECS)](https://zhuanlan.zhihu.com/p/270927422)




---

ECS 主張資料與運算邏輯分離，並定義了幾個角色3：

最近開始整理 ECS 的相關實作方式
先簡單釐清一下 ECS 核心概念
定義最早來源為 2007, Operation Flashpoint: Dragon Rising 推出的文件
Entities as ID's
Components as Raw Data
Code stored in Systems, not in Entities or Components
--------------------------------------------------
一個 ECS 架構至少需要有下列基本需求
1. 能動態分配的 Entity
2. 能動態新增、刪除 Component
3. 能根據 Component 匹配對應的 Entity
--------------------------------------------------
由上述的基本需求可以得知
如何管理 Component 變成 ECS 架構中的問題核心
從 Entities as ID's 可以明白
若是將 Component 存放於 Entity 中則違背 ECS 的概念
所以需要將 Component 額外處理
兩種簡易的匹配方式
1. Entity 除了 ID 之外，另使用 Bitset 用於標記 Component
產生問題：Entity 需要多使用 Bitset 存儲資料，以及每次匹配時都需要遍歷所有 Entity，造成額外損耗
2. 在新增、刪除 Component 時，將 Entity 進行分類
產生問題：每次新增、刪除時，動態改變 Entity 的分類會造成額外損耗
--------------------------------------------------
Unity ECS 的匹配方式
Chunk：固定長度的記憶體區段，用於存放相同 Component 組合
Archetype：擁有相同 Component 組合的 Chunk 鏈
Group：對 Archetype 的查詢


----

Entity：一個實體代表一個通用對象。在遊戲引擎上下文中，例如，每個粗糙的遊戲對象都被表示為一個實體1。
Component：一個組件使實體具有特定的方面，並保存模擬該方面所需的數據1。
System：一個系統是一個對所有具有所需組件的實體進行操作的過程1。例如，物理系統可能查詢具有質量、速度和位置組件的實體，並對每個實體的一組組件進行物理計算1。系統可以在運行時改變實體的行為，通過添加、刪除或修改組件1。


這消除了在面向對象編程技術中經常發現的深度和寬度繼承層次結構的模糊問題，這些問題往往難以理解、維護和擴展1。
常見的 ECS 方法與數據導向設計技術高度兼容，並且經常與之結合1。
所有組件的數據在物理內存中連續存儲在一起，使得對許多實體進行操作的系統能夠有效地訪問內存1。
這就是 Entity Component System 的起源和基本概念。希望這對您有所幫助！