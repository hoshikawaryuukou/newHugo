---
title: "Unity - Service - Google Play Install Referrer"
date: 2024-01-25 22:11:00
draft: false

tags: ["Unity"]
---

## 簡述

[Play Install Referrer](https://developer.android.com/google/play/installreferrer?hl=zh-tw)

- Play Install Referrer API : 非 Kotlin / Java 用戶使用
- Play Install Referrer Library : 將上者封裝更方便 Kotlin / Java 使用

透過該服務能對 App 的下載與使用者進行歸因分析，用於評估推廣服務得成效，進而提升推廣效果與報酬率。

- 舊版 Play Install Referrer 在使用者下載應用程式後透過廣播傳送包含歸因參數的訊息。然而廣播的不可靠性和安全性問題，目前不再建議使用這個版本。
- 新版 Play Install Referrer 直接訪問本機 Google Play 應用程式商店中的記錄，索取 referrer 值，因此更加可靠。


## 快速上手

Unity 專案: 將依賴加在 maintemplate.gradle
```
dependencies {
    implementation("com.android.installreferrer:installreferrer:2.2")
}
```

因為官方 API 文件寫的不全，建議到以下網站直接下載 aar 查看 jar 來對接 API
- [Google's Maven Repository](https://maven.google.com/web/index.html?q=install#com.android.installreferrer:installreferrer:2.2)
- [Maven Repository](https://mvnrepository.com/artifact/com.android.installreferrer/installreferrer/2.2)

使用服務的工作流為如下
1. 建立連線
2. 等待 callback 連線成功
3. 索取 referrer
4. 關閉連線

## Referrer 格式
```
https://play.google.com/store/apps/details?id=${package name}&referrer=${parameter}
```

- [Play Campaign URL Builder](https://ga-dev-tools.google/campaign-url-builder/play/)
- [廣告活動參數](https://developers.google.com/analytics/devguides/collection/android/v4/campaigns?hl=zh-tw#campaign-params)

## Referrer 狀態

將手機連著 android studio 開啟 Logcat，透過連結前往商店發現有 4 種情境
  
- 未安裝 點連結
> Finsky 
> com.android.vending 
> Capture referrer for **package name** 

- 已安裝 點連結
> Finsky 
> com.android.vending 
> Dropped referrer for **package name** because dropped_already_captured

- 已安裝 但有版本差異
> Finsky 
> com.android.vending 
> Dropped referrer for **package name** because dropped_already_installed

- 移除app 會移除 referrer
> 但沒有 Finsky 相關 log

## 模擬測試

透過**Google Play Console 封閉式測試**是比較正規的測法，但如果沒有現成的產品，也可以借別人(架上的)的 package name 來測試
- 下載別人的產品但**不要載完(要取消)**，這時 referrer 還會保留
- 將本地測試的專案 package name 改成別人的 package name，就能使用到保留的 referrer 

## Ref
- [Android 下載歸因— GA與Play Install Referrer庫](https://juejin.cn/post/7305182777438683162)
- [android 整合Play Install Referrer](https://blog.csdn.net/HUandroid/article/details/119249924)
- [uerceg/play-install-referrer-unity (obsolete)](https://github.com/uerceg/play-install-referrer-unity)
- 
