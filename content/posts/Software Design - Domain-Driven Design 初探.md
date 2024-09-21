---
title: "Software Design - Domain-Driven Design 初探"
date: 2022-12-15 20:05:00
draft: false

tags: ["Software Design"]
---
必須先聲明筆者仍在學習中，以下屬個人觀點

## 動機
筆者發現在使用 Clean Architecture (CA) 時越來越力不從心，因此開始研究 Domain-Driven Design (DDD)，事出有因，列出幾點問題與對應方式。

#### 重複的程式碼
- 主因是 貧血域模型 (Anemic Domain Model)，表示模型中幾乎只有 Get/Set，這導致了 Domain層 (業務邏輯) 滲透到 Application層 (應用邏輯)，某些對 Domain 的操作重複出現在多個的 Usecase (應用邏輯)。
- 重新分析系統，區分出不同上下文，設計充血域模型，將業務邏輯設計進去。

#### 域模型的一致性問題
- Domain 面對四面八方的操作，顯得很亂且充滿不確定(會不會模型之間的關係因為更改而被破壞)
- 引入聚合(Aggregate)來維持保護邊界內的不變條件。

#### Primitive Obsession  
- 這會造成對模型的不信任，進而寫出一些防禦性程式設計。
- 引入值物件(Value Object)來確保不變性與自我驗證(即不正確就不應該存在)。

以上這幾點是筆者比較有感的。

## 概述與想法
Domain-Driven Design (DDD)，出自 Eric Evans 2003 年出版的一本書，以領域模型為中心來進行系統的分析設計。不是架構也不是技術，是一種方法論，可以搭配不同類型的架構來實現
- Layered Architecture
- Hexagonal Architecture
- Clean Architecture (以下稱 CA ) 
- Command Query Responsibility Segregation (CQRS)

原著中是使用 Layered Architecture 的架構作為示範，但該章的重點是在隔離 Domain，在 Google 的時候有所謂 "DDD 架構圖"，但筆者覺得不太精確，因為 DDD 主要的發力點是在 Domain，應該稱作 "OO架構以DDD實作Domain" 會比較合適。

DDD 的設計流程又分成兩的階段

#### 戰略設計 (Strategic Design)
與"領域專家"積極交流分析的時候。先來個狀況劇:

> 根據 Q1 這個需求開發人員們        
> 開發人員 A: 應該 這樣->這樣->那樣->那樣->那樣     
> 開發人員 B: 應該 這樣->那樣->那樣->這樣     
> ...    
> 領域專家:      
> 喔喔 這個阿 就-> 那樣->這樣     
> 然後簡訊通知就好了，畢竟發生頻率很低

領域專家是每天都在處理這類事務或最瞭解這類情境的人，因此有疑問時詢問領域專家是很重要的，免得外行在那邊猜半天徒增複雜度。開發人員與領域專家互動的終極目標就是共同語言(Uniquitous Language)，透過這個語言進行交流。確保最終設計出來的東西，有達到雙方想要的結果。

#### 戰術設計 (Tactical Design)
架構師/工程師展現設計工法的時候
- Entity
- Value Object
- Aggregate
- Domain Event
- Service
- Design Patterns

## 總結
但產品是會演化的，需求會改變，Domain 會改變，所以戰略設計與戰術設計這兩階段是會不斷迭代。

筆者覺得 戰略設計/戰術設計 完全符合 80/20法則，之前完全不去分析域，一股腦地將戰術設計套進專案中，但還是覺得卡卡的。解決發散的域邏輯，還是較為優先。

開發出來的軟體是能夠準確表達業務規則，以達到程式<=>業務是同構的。筆者感覺這個是 DDD 的根本價值。

## Ref 
- [Domain-Driven Design: Tackling Complexity in the Heart of Software]
- [理解領域驅動設計](https://www.cnblogs.com/CKExp/p/14289377.html)
- [DDD is not architecture](https://blog.onehundredacorns.com/2014/10/13/ddd-is-not-architecture/)