---
title: "CSharp - Note"
date: 2023-01-05 21:11:00
draft: false

tags: ["CSharp"]
---

## 語法 
- [C# 的一些冷知识（其一）](https://www.bilibili.com/video/BV1RR4y1r7vj)
- [C# 的一些冷知识（其二）](https://www.bilibili.com/video/BV1EP4y1B7Er)
- [捨棄 - C# 基本概念](https://learn.microsoft.com/zh-tw/dotnet/csharp/fundamentals/functional/discards)
- [C#中 ??、 ?、 ?: 、?.、?[ ] 问号](https://www.bilibili.com/read/cv14801567)

## Type
- [C# 4.0：Covariance 與 Contravariance 觀念入門](https://www.huanlintalk.com/2009/10/c-40covariance-and-contravariance.html)

## Data
- [Different ways to return data in C#](https://www.linkedin.com/pulse/different-ways-return-data-c-ziv-ben-or)
- [ValueTuple](https://dotblogs.com.tw/ASPNETShare/2017/02/24/20170223-ValueTuple)
> ValueTuple 是 value type，所以它使用的記憶體空間使用在 program stack，因此使用不會有 garbage collection

## Format
- [內插字串](https://dotblogs.com.tw/lazycodestyle/2016/06/24/005827)

## Collection
- [C# 回傳內部資料集合的幾種方式，考慮封裝與設計需求](https://dev.twsiyuan.com/2018/02/encapsulating-list-collection-in-c-sharp.html)
- [Iterate over two collections of equal length](https://codereview.stackexchange.com/questions/48661/iterate-over-two-collections-of-equal-length)
```sh
foreach (var (cell, id) in cells.Zip(randomizedIDs, (key, value) => (Cell: key, ID: value)))
{
    idDict[cell] = id;
    cell.selectCallback = Select;
}
```

## Utils

- Random
```sh
var random_list = list.OrderBy(i => Guid.NewGuid()).ToList();
```

## Other
- [工作十余年，还是一直被问 委托和事件 有什么区别？ 真是够了](https://zhuanlan.zhihu.com/p/178307774)


<!-- ## Other
- [源代码生成器Source Generator C#高级教程01](https://www.bilibili.com/video/BV131421879f/?spm_id_from=333.1365.0.0&vd_source=863870bbf22c37b1b09727751205f522) -->

