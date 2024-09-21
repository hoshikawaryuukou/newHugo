---
title: "Software Design - Pattern - Data Transfer Object (DTO)"
date: 2022-12-11 21:11:00
draft: false

tags: ["Software Design", "Pattern"]
---

## 什麼是 DTO？

Data Transfer Object (數據傳輸對象) 是定義如何在應用程序之間發送數據的對象。它僅用於發送和接收數據，本身不包含任何業務邏輯。

## 為什麼使用 DTO？

### 輕鬆收發
在沒有任何邏輯的基礎上，可以僅使用序列化與反序列化就保證對象的完整性和可傳遞性。

### 避免過度暴露訊息

對分層或模組來說，彼此間應盡量降低耦合。下圖以公園廁所報修為案例。

![DTO Example](/images/DTO.png)

這個資料流由**鄉公所**傳到**基層人員**手上，中間經過兩個邊界 

* 鄉公所 | 工程公司 => DTO (公文)
* 工程公司 | 基層人員 => DTO (簡訊)

每個單位的關注點不同，在意的資料也會不同，DTO 做為邊界兩方做最小程度的媒介，隱藏的不該被關注(敏感)的事 
* 印章對工程公司並不是必要資訊
* 詳細的時間格式是對基層人員並不是必要資訊

在實作上常被用於轉換 DomainModol -> DomainDto

## 注意事項
類別數量增加，請自行評估使用情形

## Ref
- [Cutting Edge - Pros and Cons of Data Transfer Objects](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/august/pros-and-cons-of-data-transfer-objects)
- [The DTO (Data Transfer Object)](https://examples.javacodegeeks.com/the-dto-data-transfer-object/)
- [Data Transfer Objects](https://aspnetboilerplate.com/Pages/Documents/Data-Transfer-Objects)
- [Clean Architecture : why not using the entity as request model of the use case (interactor)](https://stackoverflow.com/questions/52812337/clean-architecture-why-not-using-the-entity-as-request-model-of-the-use-case)
- [Difference between Entity and DTO](https://stackoverflow.com/questions/39397147/difference-between-entity-and-dto)