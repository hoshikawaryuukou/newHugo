---
title: "Unity - Basic - AndroidJNIModule"
date: 2024-01-28 21:11:00
draft: false

tags: ["Unity", Android]
---

## 前述

這次的業務需求是
> 將 Google Play Install Referrer 接入 Unity

目前有使用到 AndroidJNIModule 中的
- AndroidJavaClass
- AndroidJavaObject
- AndroidJavaProxy

但中途採了不少坑，特此紀錄一下。

## 基本知識
- [UnityEngine.AndroidJNIModule](https://docs.unity3d.com/ScriptReference/UnityEngine.AndroidJNIModule.html)
- [How to Create Android Java Callbacks to C# in Unity](https://vuopaja.com/tutorials/android-java-proxy)
- [UnityからAndroidのクラスや関数を呼び出す](https://zenn.dev/sunmax/articles/e079dd3ba7c487)

### [AndroidJavaClass](https://docs.unity3d.com/ScriptReference/AndroidJavaClass.html)
- 可以實例化 Java 類、調用 Java 類的靜態方法，以及訪問 Java 類的靜態屬性。

### [AndroidJavaObject](https://docs.unity.cn/2022.3/Documentation/ScriptReference/AndroidJavaObject.html)
- 創建 Java 對象的實例。

### [AndroidJavaProxy](https://docs.unity3d.com/ScriptReference/AndroidJavaProxy.html)
- 允許在 Unity C# 腳本中實現 Java 接口。
- 允許我們在 Java 中調用方法，這些方法將調用 C# 類上的 **匹配** 方法。

## 注意
- 函數名匹配 (建議直接看 source code 裡面的值，本此次就遇到 官方文件與 jar 為匹配)
- android.os.Build.VERSION 將意味著要到一個公開類
- android.os.Build$VERSION 將意味著進入一個內部類
