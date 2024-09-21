---
title: "Software Design - Principle - Dependency Inversion Principle (DIP)"
date: 2022-11-15 20:05:00
draft: false

tags: ["Software Design", "Principle"]
---

依賴倒置原則 Dependency Inversion Principle，以下皆簡稱 DIP。

## 為什麼需要

先來看定義    
- 高層次的模塊不應該依賴於低層次的模塊，兩者都應該依賴於抽象接口
- 抽象接口不應該依賴於具體實現。而具體實現則應該依賴於抽象接口

文謅謅的，但重點似乎是抽象。不如直接看個狀況劇:

> 有一個 Project A 需要使用播廣告的功能。分別採 2 個做法

### 直接依賴
![DIPNO](/images/DIPNO.png)

直覺的做法。Project A 直接依賴於廣告模組(UnityAds)，這裡模組 Project A 被迫去了解 UnityAds 的實作細節(怎麼初始化/下載廣告/播廣告)。

目前沒甚麼問題，運作得很好... 但很快問題就來了。UnityAds 因為某些原因不能用了! (假設後臺被打了什麼的)。於是找了另一個廣告模組(AdMob)，想要如法炮製，但有幾點可能會不好受。
- 要改的地方很分散 (廣告被 Project A 多處使用)
- Project A 需要處理不同的 API格式 (了解細節，單例、Callback、事件...)
- 導致原先依賴 UnityAds 的模組需要重新編譯 (造成浪費時間)

原因是**直接依賴**外部模組導致的，相對於你的系統 UnityAds 是個外人，是不穩定的，去依賴一個不穩定的東西，也會導致自己變得不穩定。

### 依賴倒置
![DIPValid](/images/DIPValid.png)

- 仔細想一下，Project A 直接依賴 UnityAds 是必要的嗎?
- 需求是播 UnityAds 的廣告? 還是播廣告?

為了實現穩定廣告服務的依賴源，我們將其抽象化
```csharp
public interface IAdService
{
    void Initialize();
    void Load();
    void Show();
}
```

但 UnityAds 與 AdMob 又不能直接實作這個介面怎麼辦，可以用配接器模式(Adapter Pattern)寫個轉接頭，想辦法讓外部細節符合 IAdService 的需求。現在需要廣告服務的部分均透過 IAdService來操作，不需再知道外部廣告模組的細節。

## 無效的 DIP

![DIPInvalid](/images/DIPInvalid.png)

雖然 Project A 依賴了介面，但那介面是 Ad Module 所提供的，仍然是直接使用外部細節。這個陷阱在於 Interface 的位置，這在學習前期坑了我好大一跤，當時倒置了一堆無用接口...

## 注意
做 DIP 是為了未來替換時降低傷害，如果沒有替換需求則未必要採用。
