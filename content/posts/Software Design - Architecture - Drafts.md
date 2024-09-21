---
title: "Software Design - Architecture - Drafts"
date: 2022-11-06 20:05:00
draft: true

tags: ["Drafts"]
---

讓我解釋一下原因。作為我工作的一部分，我遇到了大量的團隊，他們告訴我他們正在做所有最新的微服務和API，甚至可能是 "事件驅動"，但他們在市場速度和適應不斷變化的需求的敏捷性方面掙扎。

現實情況是，神奇之處在於功能的分解和關注點的分離，以實現解耦（或輕度耦合--取決於你的定義和方法）架構。正是這種解耦性最終給了你敏捷性，以及允許你分片、分配你的工作、有效地使用異步方法等。

這是大的反思，而不是使用微服務（儘管它們可以幫助保持事情更明顯的干淨；也可以使用真正的事件--而不是我經常看到的請求或命令被掩蓋在偽事件中）。

我還沒有看到有人成功地用基本的代碼單體做到這一點的例子，儘管它在理論上是很有可能的，正如這裡所確認的，它是關於使用的模式。

因此，這很好地驗證了我長期以來對模式、功能（領域）設計的看法和關注，並將這些邊界作為解耦點反映在代碼中。

雖然我在傳統上對微服務做得很成功，而且規模很大，但很高興知道，雖然做起來可能不那麼容易，但從根本上說，即使在單體框架中也可以做到這一點。

-------------------

## Event Sourcing
- 事件代表過去發生的事情, 已經發生並且無法改變的事實——換句話說，它們必須是不可變的
- 事件存儲

事件溯源是一種旨在解決此類問題的架構方法。 
事件溯源不是跟踪當前狀態，而是跟踪導致當前狀態的整個狀態轉換序列。 
這些狀態轉換稱為Events，是系統的“真實來源”，當前狀態（或任何過去的狀態）是從中推斷出來的（因此稱為Event Sourcing）。

### Ref
- [深入浅出Event Sourcing和CQRS](https://zhuanlan.zhihu.com/p/38968012)
- [事件溯源（1）：Event Sourcing的好處](http://teddy-chen-tw.blogspot.com/2022/06/1event-sourcing.html)
- [事件溯源（2）：實作Event Sourced Aggregate](http://teddy-chen-tw.blogspot.com/2022/06/2event-sourced-aggregate.html)
- [1 Year of Event Sourcing and CQRS](https://itnext.io/1-year-of-event-sourcing-and-cqrs-fb9033ccd1c6)
- [基于CQRS的架构在答题PK小游戏中的实践案例](https://juejin.cn/post/6844903653942231053)
- [Domain Events vs. Event Sourcing](https://www.innoq.com/en/blog/domain-events-versus-event-sourcing/)

-------------------

## Event-Driven Design
Event-driven programming

事件（event）是針對應用程序所發生的事情，並且應用程序需要對這種事情做出響應。
事件處理程序（event handler）

事件產生後是不會改變的。既成事實

事件的生產者並不需要關心自己所產生的事件的後續如何，如有沒有成功更新數據庫、有沒有合適的鎖等等問題。
事件消費者（包含監聽和訂閱兩種模式）自身是一個領域模型，它只負責接收事件並響應。


### Guide
- [事件驅動架構設計](https://www.qin.news/event-driven/)

### Business processes and workflows
- [Event Choreography & Orchestration (Sagas)](https://codeopinion.com/event-choreography-orchestration-sagas/)

### Ref
- [How Should My Event Be Designed? Some Thoughts on Event-Based Systems](https://www.gokhan-gokalp.com/en/how-should-my-event-be-designed-some-thoughts-on-event-based-systems/)
- [Event driven design for gaming applications](https://www.epifab.solutions/posts/event-driven-design-for-gaming-applications)

-------------------

## Mod
### 在架構之前
在架構之前筆者希望先依序做到幾件事
- 乾淨的代碼 : 清晰地描述功能
- 關注點分離 : 以合理的邊界拆分功能，做到可插拔/可擴展性

其他任何東西都是<品味>和<選擇>

### 是否要模組化 ?
是否要模組化取決於應用程式有多大
- 延遲加載 : 模組化有助於保持較小的初始包大小，減少您的應用程序的初始加載時間

筆者習慣分成以下幾類
- 核心模塊 (Core Module)
- 共享模塊 (Shared Module)
- 功能模塊 (Feature Module)
  
### Ref
- [Why Is Software Architecture Important?](https://codecoach.co.nz/why-is-software-architecture-important/)
- [Framework 和 Architecture 有何不同?](https://dotblogs.com.tw/regionbbs/2009/06/12/framework_vs_architecture#google_vignette)
- [Organizing by Feature or Component](https://www.scaledagileframework.com/features-and-components/)

-------------------

## Entity Component System (ECS)
- [Unity的ECS的缺点是什么？](https://www.zhihu.com/question/452129116)
- [游戏开发中的ECS架构实用性如何？](https://www.zhihu.com/question/455479955/answer/1900463963)
- [ECS 真的是「未来主流」的架构吗？](https://www.zhihu.com/question/286963885/answer/456710929)
- [Why isn't Godot an ECS-based game engine?](https://godotengine.org/article/why-isnt-godot-ecs-based-game-engine/)