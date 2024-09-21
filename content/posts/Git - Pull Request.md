---
title: "Git - Pull Request"
date: 2023-07-14 13:11:00
draft: false

tags: ["Git"]
---

> 有的環境也稱 Merge Request 

## 情境
開發產品時一般會挑選固定一個分支做為可以上線的正式版本分支(master)，需注意的是在進行多人協同開發時，讓每個人都可以 Commit 到專案正式上線的分支不是個好的做法。

可以透過 pull request 方式控管權限，由負責管理這個專案的人收到其他開發者的 pull request 並確認無誤後便可進行合併，來確保產品分支處於隨時都是可上線的狀態。

參與開源專案時，在創建 pull request 之前，建議先在本地分支上運行 git rebase 命令，確保你的更改基於最新的進度以降低審查者的理解難度。

## Ref
- [與其它開發者的互動 - 使用 Pull Request（PR）](https://gitbook.tw/chapters/github/pull-request)