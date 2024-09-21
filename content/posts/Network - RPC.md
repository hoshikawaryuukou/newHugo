---
title: "Network - RPC"
date: 2022-11-07 21:06:00
draft: false

tags: ["Network"]
---

## RPC (Remote Procedure Call，遠端程序呼叫)
是一種通信協定，多用於分佈式系統的通信。

### 目的
讓客戶端呼叫遠程函式就像呼叫本地函式一樣。將網路通信封裝成函式來使用，那麼客戶端將不需要關心網路協定/模型。

### 流程
1. client 客戶端通過本地呼叫的方式呼叫服務
2. client stub 接收到請求後將參數序列化成能夠進行網路傳輸的訊息體
3. client stub 找到服務地址，並將訊息發送給服務端
4. server stub 收到訊息後進行反序列化
5. server stub 根據反序列化結果呼叫本地服務
6. 本地服務執行並將處理結果返回給 server stub
7. server stub 將結果序列化並發送至 client stub
8. client stub 接收到訊息，並進行反序列化
9. client 得到最終結果

## Ref
- [怎么理解rpc，既然有http请求了为啥还要用rpc？](https://www.zhihu.com/question/524580708/answer/2584782720)
- [谁能用通俗的语言解释一下什么是 RPC 框架？](https://www.zhihu.com/question/25536695)