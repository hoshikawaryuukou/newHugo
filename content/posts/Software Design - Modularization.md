---
title: "Software Design - Modularization"
date: 2023-02-22 21:21:00
draft: false

tags: ["Software Design"]
---

## 前述
首先幾篇文章是基於 Clean Architecture 的基礎，建議先閱讀以下連結已具備基礎知識

### The missing chapter
- CA 原著 Chapter 34 - The missing chapter - Actual implementation details of an architecture 
- [連結 34章摘要心得](https://github.com/serodriguez68/clean-architecture/blob/master/part-6-details.md#chapter-34---the-missing-chapter---actual-implementation-details-of-an-architecture)，請先觀看裡面的圖表(重要)

### CA Modularization
- [Multiple ways of defining Clean Architecture layers](https://proandroiddev.com/multiple-ways-of-defining-clean-architecture-layers-bbb70afa5d4a)
- [Package by Component with Clean Modules in Java](https://blog.ttulka.com/package-by-component-with-clean-modules-in-java/)
- [Package by feature or component](https://learning-notes.mistermicheels.com/architecture-design/reference-architectures/package-by-feature-or-component/)

### Vertical Slice
- [Slices vs. Layers](https://www.betterask.erni/news-room/slices-vs-layers/)
- [Restructuring to a Vertical Slice Architecture](https://codeopinion.com/restructuring-to-a-vertical-slice-architecture/?fbclid=IwAR0Ek5KW6_MWQ9K5Rxv6P5BpqatHs5tsjfHZ_B9GZmrkd3YaBoH-HHuNZE4)
- [Vertical Slice Architecture, not Layers!](https://www.youtube.com/watch?v=L2Wnq0ChAIA)

### Modular Monolith
- [Majestic Modular Monoliths](https://lukashajdu.com/post/majestic-modular-monolith/) (強烈建議)
- [Modular Monolith architecture](https://www.kamilgrzybek.com/design/modular-monolith-primer/) (強烈建議讀完這個系列)

-------
**各 Package 策略的圖請參考上方連結 34 章摘要心得**

## Package By Layer
筆者在剛接觸 CA 時有一個很大的迷思是以為 CA Layers 一圈就是一個模組(如果應用程式複雜度不高，確實適用)，所以整個應用程式分三個模組。
- Domain
- Application
- Adapter

一開始功能不多時確實運作得很好，隨著功能的增加，出現了一個問題 **共用**，UseCase 可以操作所有的 Domain 與 Input/Output Port，責任開始變得紊亂(UseCase 知道太多細節)。我們需要一種更能反映業務功能的模組分法，使讓專案能夠重新 **Screaming**，以下是筆者比較常用的兩個演化方向。

## Package By Component
- 僅提供**服務**，沒有 UI 操作。
- 定義 API 以隔離實作細節。

## Package By Feature
- 負責提供**使用者互動情境** (垂直切片)。
- 包含 UI 操作。

--------
筆者在一個應用程式中多是這樣分成以下三類模組

## Core Module
- 一般以 Package By Component 的方式實作。
- 提供應用程式 **內** 共用的服務。

Core 可以是包含業務的 CA 分層，如下圖左邊。
Core 可以是僅將外部服務轉換至內部服務，如下圖右邊。
![Core Module](/images/CoreModule.png)

## Feature Module
- 一般以 Package By Feature 的方式實作。
- 負責提供使用者體驗流。
- 可以使用 Core 提供的操作，必要時也可以引入所需的外部服務(仍需做 DIP)。

![Feature Module](/images/FeatureModule.png)

可能會有一個疑問是 
> UseCase 中使用的介面( Core API )不是 Application 所定義的，這樣的依賴是否為有效 DIP ? 

DIP 的重點在於依賴於**抽象(穩定)**，因此只要 Feature 的活動範圍仍在**此專案**中，依賴 Core API 就是穩定的，外部變化會被擋於 Core 的內部實現中。

實務上甚至可以考慮依賴**組織級的 Core Module**，是整個部門或者公司所共用的功能，基本上是比較泛用的功能才會這樣使用(聲音/廣告/日誌...)。

## App Module
- 依賴於所有模組。
- 應用程式的入口。
- 提供模組間的導航。

![App Module](/images/AppModule.png)


<!-- ## Other
- [The “Real” Modularization in Android](https://betterprogramming.pub/the-real-clean-architecture-in-android-modularization-e26940fd0a23) -->