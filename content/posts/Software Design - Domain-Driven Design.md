---
title: "Software Design - Domain-Driven Design"
date: 2022-12-15 20:05:00
draft: true

tags: ["Software Design"]
---


現實生活中業務中存在的規則和概念，現在以實體和值對象的形式出現在我們的代碼中。
我們正在使用用例來表達我們系統中所有不同的參與者（用戶組）可以在各自的子域中做什麼。


不要在事件裡面使用引用類
因為事件是不可變的，引用可能會使事件改變



- [我對 Domain-Driven Design 的理解（2022 年）](https://blog.aotoki.me/posts/2022/10/21/my-understand-of-domain-driven-design/)

## Book
- [Domain-Driven Design with Java — A Practitioner’s Guide](https://ddd-book.karthiks.in/#preface)
- [实现领域驱动设计-引言](https://gerryge.com/blogs/2021/Implementing_Domain_Driven_Design/01_Introduction.html#%E7%9B%AE%E6%A0%87)

## Validation
- [ContextualValidation](https://martinfowler.com/bliki/ContextualValidation.html)
- [Validation and DDD](https://enterprisecraftsmanship.com/posts/validation-and-ddd/)
- [Domain Model Validation](http://www.kamilgrzybek.com/design/domain-model-validation/)
- [Where does my validation live?](https://blog.frankdejonge.nl/where-does-validation-live/)
- [Form, Command, and Model Validation](https://verraes.net/2015/02/form-command-model-validation/)

## Guide
- [Modelling Reactive Systems with Event Storming and Domain-Driven Design](https://blog.redelastic.com/corporate-arts-crafts-modelling-reactive-systems-with-event-storming-73c6236f5dd7)


## 戰略設計
在這個階段是與"領域專家"深度交流的，目的是要找出系統範圍的多個領域(Domain)，並再切割成多個領域(Sub-Domain)

### Bounded Context
- [Intentional Naivety First Bounded Context Modelling](https://medium.com/nick-tune-tech-strategy-blog/intentional-naivety-first-bounded-context-modelling-62e6211574ec)
- [Structure of a single bounded context](https://stackoverflow.com/questions/13159299/structure-of-a-single-bounded-context)
- [識別每個微服務的領域模型界限](https://learn.microsoft.com/zh-tw/dotnet/architecture/microservices/architect-microservice-container-applications/identify-microservice-domain-model-boundaries)
- 
---

## 戰術設計
將實體進一步分類，並訂定技術架構，提供服務以操作這些實體。

### Value Object
- [DateTime as a Value Object](https://ardalis.com/datetime-as-a-value-object/)
- [Value Objects to the rescue!](https://medium.com/swlh/value-objects-to-the-rescue-28c563ad97c6)
- [Value Object: a better implementation](https://enterprisecraftsmanship.com/posts/value-object-better-implementation/)
- [3 Reasons to Model Identity as a Value Object](https://buildplease.com/pages/vo-ids/)

### Entity





### Aggregate
當修改這些物件狀態時，如果不小心很可能會違反系統的不變量（invariant）或固定規則而導致系統狀態不正確

- [領域驅動設計學習筆記（20）：再談Aggregate Root實作](http://teddy-chen-tw.blogspot.com/search?q=Aggregate)
- [领域驱动设计DDD之聚合](https://juejin.cn/post/6844904008079900679)
- [DDD Beyond the Basics: Mastering Aggregate Design](https://medium.com/ssense-tech/ddd-beyond-the-basics-mastering-aggregate-design-26591e218c8c)



### Domain Event

事務前, 事務後

- [領域事件：設計和實現](https://learn.microsoft.com/zh-tw/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/domain-events-design-implementation)
- [Domain Event Pattern](https://medium.com/akatsuki-taiwan-technology/domain-event-pattern-6781e0eba49a)
- [DDD之事件风暴Event Storming](https://zhuanlan.zhihu.com/p/399103071)


### 案例分析
- [DDD 实战 (1)：从需求到代码实现生鲜电商系统](https://xie.infoq.cn/article/f3b83ee3c28a682fa75d4a63c)


### 為什麼
構建其業務流程（業務領域）具有復雜性的軟件，則 DDD 適合您。
因此，並非每個軟件都適合 DDD（例如，CRUD 應用程序不適合它，因為它們不是很複雜）。

### 做什麼
保持與用戶/客戶（又名領域專家）的聯繫事第一要務。
“軟體可能會以兩種方式失敗，你構建錯誤的東西或者你構建錯誤的東西。”

- 釐清問題領域，即軟件試圖解決的具體問題。
- 將域分解為子域。
- 與領域專家一次專注於一個子領域，並始終使用無處不在的語言來定義工作術語。
- 在子域之間創建有界上下文。每個限界上下文都有不同的團隊、代碼庫和數據庫。
- 對於所有在有界上下文之間共享的橫切關注點（我們稱之為共享內核），每個有界上下文中的所有團隊都應該知道並同意任何更改。

### 避免什麼
- 不是以數據對問題域建模
數據本身是沒有意義的。只有邏輯才能賦予數據意義，同樣的數據在不同的語境下可以有不同的意義。
因此，我們必須從上下文和邏輯而不是數據入手。

- 關注核心概念  而不是實作細節
無處不在的語言、限界上下文和接口/精心設計的軟件契約才是核心
過早開始實現實體等實現細節，那麼結果很可能是一個被大量服務和業務邏輯分散在各處的貧血域。
永遠不要考慮數據庫事務。
相反，始終考慮現實世界的過程，例如行動（行為）及其可能的結果，或者如果發生故障如何補償行動。
總是想像客戶在沒有計算機的情況下運行他的差事/業務（手動執行特定任務）。因此，始終從業務/領域專家的角度思考，並給出清晰的上下文。避免在不同的、非特定的上下文中可能導致不同含義的通用術語。

### 戰略
子領域
核心域(Core domain)
創造競爭優勢

支撐域(Supporting domain)
支撐域可以外購或外包
餐飲業可以把外送業務直接委託FoodPanda、Uber...等外送平台

通用域(Generic domain)






---------------------------------------
討論：為什麼不把支付邏輯移到領域服務中呢？
您可能想知道為什麼付款代碼不在 OrganizationManager 中。這是一件重要的事情，我們永遠不想錯過付款。

然而，重要的是不足以將代碼視為核心業務邏輯。我們可能還有其他用例，在這些用例中，我們不收取創建新組織的費用。例如；

管理員用戶可以使用後台應用程序創建一個新組織，無需支付任何費用。
一個後台工作的數據導入/集成/同步系統也可能需要創建沒有任何支付操作的組織。
如您所見，付款不是創建有效組織的必要操作。它是一個特定於用例的應用程序邏輯。


討論：為什麼應用服務中沒有實現重複標題檢查？
我們可以簡單地說“因為它是核心領域邏輯，應該在領域層中實現”。但是，它帶來了一個新問題“您如何確定它是核心領域邏輯，而不是應用程序邏輯？” （稍後我們將詳細討論差異）。

對於這個例子，一個簡單的問題可以幫助我們做出決定：“如果我們有另一種方式（用例）來創建問題，我們是否仍應應用相同的規則？是否應始終實施該規則”。您可能會想“為什麼我們有第二種方式來創建問題？”




Event Storming 事件風暴

共同理解
找出商業流程中的核心價值、風險與機會

Event 代表已經發生過的事
領域專家所在乎的事件。
如整合第三方物流時，領域專家可能只在乎送達時間而不在乎中間細節的運輸過程。
時間概念
可以加上原因。
如「因為密碼輸入錯誤三次，所以帳號已被鎖住」。
用事件風暴的描述就是「用戶在XX 聚合對像上執行了YY 命令，生成了ZZ 事件」


Command 命令與 Actor 角色
Command 是一個使用者(或軟體)所做出的決定


Aggregate 將 Model 聚合起來
這個 Aggregate Model 可以處理這個 Command 並發出這個 Event」的 Command 與 Event 之間


Bounded Context 找出軟體的邊界


Aggregate 建立一個 Event
Aggregate 使用 Event Publisher 將 Event 發布出去
可能會有三種訂閱方接收到這個 Event
事件儲存訂閱方：將收到的 Event 儲存起來 (可用於實作 Event Sourcing)
簡單訂閱方：在同一個 Bounded Context 的訂閱方，可以用一般的 Observer 模式來實作。
跨系統訂閱方：此項事件會需要被另一個系統或是 Bounded Context 所關注，所以收到 Event 後會轉發到 Message Queue 機制 (Infrastructure 層) 後再轉發 Event 出去給訂閱方。





-------------
- [领域驱动设计实践手册](https://www.zhihu.com/column/c_1208715969939640320)
- [Event Storming Part 3 - 軟體設計](https://ithelp.ithome.com.tw/articles/10220315)
- [Domain Driven Design: A "hands on" Example (Part 3 of 3)](https://www.codeproject.com/Articles/1094772/Domain-Driven-Design-A-hands-on-Example-Part-of)
- [DDD中的聚合和UML中的聚合以及组合的关系](https://www.cnblogs.com/yanglang/p/11081486.html)

## Ref
- [Domain-Driven Design & Unit Tests](https://www.jamesmichaelhickey.com/ddd-unit-tests/)


你可以說我有一個拉條工具作為我的核心domain?
可以如果你是模組開發者的話






---------




DDD 主要關注領域和應用層

業務邏輯分為兩部分：領域邏輯和應用邏輯
領域邏輯由系統的核心領域規則組成
應用邏輯實現特定的應用程序用例

如何判斷確定是 域邏輯 or 應用邏輯 ?
首先提問有沒有另一種方式（用例）來執行這個操作(邏輯)，是否始終實施該規則 ? 
遊戲開始後必定馬上接著回合開始嗎? 能不能中間插個小短劇呢?

一定得 OO 才能 XX 嗎?

## Domain Service
- 包含不能自然地放置在實體或值對像中的域邏輯

## Application Service
- 旨在提供 API 的外觀
- 協調域邏輯的執行並且它們本身不實現任何域邏輯
- 應用程序服務聲明對執行域邏輯所需的基礎設施服務的依賴性

## Service Discussions
- [領域邏輯與應用邏輯](http://teddy-chen-tw.blogspot.com/2019/12/blog-post_10.html)
- [領域專家X](http://teddy-chen-tw.blogspot.com/2020/02/x.html)
- [DDD repositories in application or domain service](https://softwareengineering.stackexchange.com/a/400800)



