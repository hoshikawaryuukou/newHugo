---
title: "Unity - Basic - Android Build"
date: 2024-02-03 21:11:00
draft: false

tags: ["Unity", "Android"]
---

## Settings

- gradleTemplate.properties : 專案的全域 Gradle 配置。
- AndroidManifest.xml ：用於向 Android 構建工具、Android 作業系統和 Google Play 描述應用的基本資訊。
- launcherManifest.xml 定義應用的啟動配置資訊
- mainTemplate.gradle：自定義 Android 專案的 Gradle 構建過程，包括添加依賴項、修改編譯設定、配置簽名資訊等。
- launcherTemolate.gradle ：包含有關如何構建 Android 應用程式的指令
- baseProjectTemplate.gradle：所含的配置會在其他所有範本/Gradle 專案之間共用

## Ref
- [Unity 不通過Android studio 打包接SDK](https://www.jianshu.com/p/9058daafa130)