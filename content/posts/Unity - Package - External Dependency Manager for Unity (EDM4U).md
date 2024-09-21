---
title: "Unity - Package - External Dependency Manager for Unity (EDM4U)"
date: 2023-11-08 21:11:00
draft: false

tags: ["Unity", "Google Service"]
---

## 前言
Google 停止維護 Game Package Registry (GPR) 導致不能直接使用 Package Manager 導入包。必須到封存檔網站下載「.tgz」手動導入。

- [Google Unity 套件](https://developers.google.com/unity/archive?hl=zh-tw#external_dependency_manager_for_unity)
- [Install a package from a local tarball file](https://docs.unity3d.com/Manual/upm-ui-tarball.html)

其他的相關的 Google Service 依賴(AR/Firebase/Google Play等)也可以用此方法導入。

## 設定
`Assets > External Dependency Manager > Android Resolver > Settings`
啟用這三個 Patch 
![EDM4U_01](/images/EDM4U_01.png)

並至 `Player Settings > Publishing Settings` 
啟用以下選項
![EDM4U_02](/images/EDM4U_02.png)

## Auto resolution
`Assets > External Dependency Manager > Android Resolver > Force Resolve`
後會去收集專案**所有 Editor 資料夾**下的 ***Dependencies.xml** 加到 mainTemplate 中
