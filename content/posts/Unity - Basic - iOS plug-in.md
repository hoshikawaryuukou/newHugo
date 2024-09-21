---
title: "Unity - Basic - iOS plug-in"
date: 2023-07-05 21:11:00
draft: false

tags: ["Unity"]
---

## 前述

這次的業務需求是
> 取得 ios 實機的 "地區"，並讓 C# 能拿到 Swift 所返回的字串
 
因為在 ios 的環境下 unity / C# 拿到的值並不正確。此外筆者對 Swift / Objective-C 幾乎零基礎，目前只針對一些教學文件做些修改，之後有機會更熟再回頭深究。

## 實作

- SwiftDeviceInfoPlugin.swift 須放置於 Plugins\iOS 之下

```swift
import Foundation

public class SwiftDeviceInfoPlugin
{
    public static func getRegion() -> String
    {
        return Locale.current.regionCode ?? "Unknown"
    }
}

@_cdecl("getRegion")
public func getRegion() -> UnsafePointer<CChar>? 
{
    let region = strdup(SwiftDeviceInfoPlugin.getRegion())
    return UnsafePointer(region)
}
```

- @_cdecl("getRegion")：這是一個 Swift 標記，表示下面的函數將使用cdecl樣式的名稱綁定。您只需知道此屬性向 C 公開了一個 Swift 函數
- UnsafePointer\<CChar>?，它是一個可為空的指向 C 風格字串（CChar）的指標。這使得 Swift 能夠以與 C 相容的方式提供訪問區域資訊的介面。
- strdup() 用於創建預返回的字串的副本，並在堆上分配其記憶體。

```csharp
public sealed class IOSDeviceInfoProvider : IDeviceInfoProvider
{
    public string GetRegion()
    {
        return new System.Globalization.RegionInfo(GetRegionFromDevice()).ThreeLetterISORegionName.ToUpper();
    }

    [DllImport("__Internal", EntryPoint = "getRegion")]
    static extern string GetRegionFromDevice();
}
```
- [DllImport] : 是一個 System.Runtime.InteropServices 命名空間中的屬性，它告訴 C# 編譯器這個函數是在外部插件中定義的，並且需要從外部導入。
- EntryPoint = "getRegion" 表示在外部插件中將使用名為 callSwift 的函數作為入口點。
- extern 關鍵字表示該函數的實現不是在 C# 代碼中，而是在外部的原生插件中實現的。


## 待補
- 記憶體管理的知識點
- 這次沒用到委派，須找時間理解

## Ref
- [Building plug-ins for iOS](https://docs.unity3d.com/Manual/PluginsForIOS.html)
- [C# から直接 Swift コードを呼び出す](https://www.create-forever.games/unity2021-csharp-swift-call/)
- [Setting Up iOS Framework for Unity From Swift to C#](https://betterprogramming.pub/setting-up-ios-framework-for-unity-9ef4e577db89)