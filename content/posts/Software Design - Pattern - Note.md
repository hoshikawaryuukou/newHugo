---
title: "Software Design - Pattern - Note"
date: 2024-08-01 21:05:00
draft: false

tags: ["Software Design", "Pattern"]
---

## Factory
- [工厂模式？错！是工厂模式群！](https://www.bilibili.com/video/BV1ZS421X74d)

## Observer / Pub-Sub (Publisher-Subscriber) 
- [Observer vs Pub-Sub pattern](https://hackernoon.com/observer-vs-pub-sub-pattern-50d3b27f838c)
- [Pub sub system pros and cons](https://www.semicolonandsons.com/code_diary/architecture/pub-sub-system-pros-and-cons)

### Observer
觀察者模式中的主題同時身為發布者，觀察者是知道發布者的，但發布者不知道觀察者。

### Pub-Sub (Publisher-Subscriber)
發布者-訂閱者模式中的主題通常由消息代理或事件總線處理，發布者和觀察者不知道彼此的存在。發布者項主題發送訊息，主題再轉發給觀察者。
