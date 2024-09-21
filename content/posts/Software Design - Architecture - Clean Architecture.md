---
title: "Software Design - Architecture - Clean Architecture"
date: 2023-02-04 20:03:00
draft: false

tags: ["Software Design", "Architecture"]
---

以下 Clean Architecture 簡稱 CA

這裡還是先引用 Uncle Bob 的分層圖 
[The Clean Code Blog - The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
![CA Layers](https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg)

筆者認爲可擴展性是系統架構的重要考量。畢竟應用程式會演化，必須不斷更新與修改系統以滿足新的需求，而 CA 是其中一種實現方針。筆者在這裡不會寫出詳細的介紹，想了解的可以參考 Ref 整理的連結或是 CA 相關書籍。

本文著重於促使筆者思考方式改變的幾個重要觀念。

## 依賴關係
- 相依性: 向內圈依賴，且盡量避免跨層依賴 (有些例外之後說明)。
- Dependency Inversion Principle (DIP): 內圈定義介面，外圈實作。

基於這兩個規則所帶來的是
- 單向依賴流 : 紊亂的依賴流可能造成牽一髮動全身的窘境。尤其是當 Domain 去依賴到細節時。
- 延後實作 : UseCase/Adapter 都是依賴於應用層所開出的介面。因此業務/畫面能獨立開發，不用互相等待(理想狀態)。

而筆者在實作時的基本型架構通常如下圖(比較接近 CA 書中的另外一張圖，我這裡做了簡化)，Adapter 只分成 Input/Output Port。
![Clean Architecture Basic](/images/CleanArchitectureBasic.png)

- Domain: 領域邏輯
- UseCase: 應用邏輯
- Domain + UseCase: 業務邏輯
- InputPort: 用例功能使用方介面
- OutputPort: 用例功能支援方介面
- Adapter: 將外部與用例功能接合的膠水代碼

不過架構會針對不同情況做調整，細節參考另一篇文章

架構設計 - Clean Architecture and Modularization

此外在原著中的定義描述 
- Entities 使用 enterprise wide business rules
- UseCases 使用 application specific business rules 

業務邏輯 | 商業邏輯 | 領域邏輯，如果你常在爬文，這幾個詞彙被混用的非常厲害，不同專業領域都有自己的一套說法。筆者的分法是參考 [Link](http://teddy-chen-tw.blogspot.com/2019/12/blog-post_10.html)。

## 依賴關係 (跨層)

![Clean Architecture DataAccess](/images/CleanArchitectureDataAccess.png)

發生於 Data Access 的部分，DataAccess 介面簽名上是看的到 Entity 的。筆者參考很多評論覺得這是可以接受的，因為 **"上下文單純"**，Data Access Impl 只處理持久化物件與 Entity 之間的轉換，不做其他操作。

## Use Case
用例是應用程式的說明書，可以很清楚的看到整個應用程式能做那些事，設種設計風格也稱作 **尖叫的架構 (Screaming Architecture)**。

筆者直接感受到的好處是當業務發生變化時可以很快知道要改哪裡。
- 定義 **做什麼** 而不是 **如何做**，透過介面隱藏實作細節
- 業務流集中於一個地方，決定輸入/輸出

以下有一些 FAQ 

- 用例可以依賴其他用例嗎?
  - 可以但盡量避免，共用的用例筆者會盡量保持 Internal。

- 用例與領域的界線開始變得很模糊，且彼此滲透。
  - 隨者應用需求不斷演化，也需重新評估 Domain(分割或合併)。此外當業務複雜度足夠高時，可以考慮導入 DDD(Domain-Driven Design)，領域事件/聚合也許能幫助 Domain 更加內聚。

- InputPort 有必要嗎? 依賴方向本來就向內
  - 當用例需要被抽象時是需要的，如果沒有那種需求不做也無妨。但為了統一般筆者基本上還是會寫。

- 用例似乎有很多種風格的寫法
  - 確實常見的有 2 種: Service方法集 / CQRS風格

## Adapter
筆者之前對套件更換這件事是感到非常棘手的，好像每次更換都有劇烈的不適，直到知道透過 DIP + Adapter 可以把不安定要素(Presentation/Database/Service)安置在應用程式的最外緣。完全改變實現是非常容易的，因為它對業務邏輯沒有影響。

## Ref

### Overview 
概述，這些文章在對於從未知入門的人來說，圖表與條列項，可以為他們先指出一些方向。
- [Software Architecture - Clean Architecture](https://atomiv.org/knowledgebase/software-architecture/clean-architecture)
- [Clean Architecture](https://learning-notes.mistermicheels.com/architecture-design/reference-architectures/clean-architecture/)

### Guide
以下參考著重在觀念引導，再加上實例輔助，必須說這些參考文都要包含"自己的理解"閱讀價值才得以顯現。
- [Getting Started With Clean Architecture for Android [Part 1]](https://www.cobeisfresh.com/blog/getting-started-with-clean-architecture-for-android-part-1)
- [Clean Architecture on Frontend](https://dev.to/bespoyasov/clean-architecture-on-frontend-4311)
- [Clean Architecture の勘所は『鎖国』だ。](https://qiita.com/t2-kob/items/02a76572693130c9a66e)
- [Unityを利用した大規模なゲーム開発にクリーンアーキテクチャを採用した話](https://developers.wonderpla.net/entry/2021/02/18/121932)

### Discussion 
以下參考著重觀念釐清，初期探索採坑的地方與一些討論串。
- [Clean Architecture Guide (with tested examples): Data Flow != Dependency Rule](https://proandroiddev.com/clean-architecture-data-flow-dependency-rule-615ffdd79e29)
- [Why data layer has a dependency on the domain layer?](https://github.com/android10/Android-CleanArchitecture/issues/136)
- [Do Interactors in "clean architecture" violate the Single Responsibility Principle?](https://softwareengineering.stackexchange.com/a/364727)
- [Layer for Managers and Services that require Android Context](https://github.com/android10/Android-CleanArchitecture/issues/151)
- [Why you need Use Cases/Interactors](https://proandroiddev.com/why-you-need-use-cases-interactors-142e8a6fe576)
- [What is the use of DTO instead of Entity?](https://softwareengineering.stackexchange.com/questions/373284/what-is-the-use-of-dto-instead-of-entity)
- [Clean Architecture: Use case containing the presenter or returning data?](https://softwareengineering.stackexchange.com/questions/357052/clean-architecture-use-case-containing-the-presenter-or-returning-data)
- [How to make the controller framework independent in Clean Architecture?](https://softwareengineering.stackexchange.com/questions/420323/how-to-make-the-controller-framework-independent-in-clean-architecture)
- [Clean architecture - where to put input validation logic?](https://stackoverflow.com/questions/57603422/clean-architecture-where-to-put-input-validation-logic)
- [How to pass the android dependent data from data-layer to presentation-layer](https://github.com/android10/Android-CleanArchitecture/issues/182)

### Notes
一些 CA 的閱讀心得。
- [Clean architecture for the rest of us](https://pusher.com/tutorials/clean-architecture-introduction/#adapters)
- [Clean Architecture - notebook](https://twydev.github.io/software%20design/software%20architecture/clean-architecture/)
- [serodriguez68/clean-architecture](https://github.com/serodriguez68/clean-architecture)

### Repo
- [igorwojda/android-showcase](https://github.com/igorwojda/Android-Showcase#domain-layer)