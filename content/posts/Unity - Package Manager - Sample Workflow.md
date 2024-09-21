---
title: "Unity - Package Manager - Sample Workflow"
date: 2023-04-22 21:11:00
draft: false

tags: ["Unity", "UPM"]
---

## Package Samples
對應有些模組的操作比較複雜繁瑣，有時需要有一些 Sample 做參考。官方 Package Manager 有個 "半套" Sample 工作流，讓人不是很舒服。

[官方文件](https://docs.unity3d.com/2021.3/Documentation/Manual/cus-samples.html)

Sample 資料夾後面加了波浪號 (~) 告訴 Unity 忽略 Samples~ 文件夾中的內容，此類文件夾不使用.meta文件進行跟踪。忽略 Samples~ 對 Package 使用者是好的，畢竟不是每個人都需要。

![Unity_Package_BasicStructure](/images/Unity_Package_BasicStructure.png)

但對 Package 開發者，畢竟 Samples 也是要進版控的，而這樣改名的作法會徒增一些重命名的提交也有點煩躁(除非在修改 Sample 的過程中完全不提交)。原先想說寫個 Samples ↔ Samples~ 切換的腳本就好，會一直有 meta 檔的警告(刪掉/改名都還是在)。

![Unity_PackageManager_MetaWarning](/images/Unity_PackageManager_MetaWarning.png)

[官方作法](https://forum.unity.com/threads/samples-in-packages-manual-setup.623080/#post-4991561) 論壇中的某篇討論才記載他們的做法(倒是加到文件中阿...)

- 在內部確實使用了名為 Samples 的文件夾 (沒有 Samples~ )
- 在推送新包版本之前通過腳本對其進行重命名(透過 CI )

[OpenUPM](https://medium.com/openupm/how-to-maintain-upm-package-part-1-7b4daf88d4c4) 的作者也是使用類似的工作流，總之筆者也調整為上述的方式。

## 透過 GitHub Actions Workflow 調整目錄名

筆者不熟 GitHub Actions/ YAML/ 文件操作，但這種初階的操作就交由 chatgpt 代勞，幫我省去不少實驗成本。這裡的操作只是堪用，應該有更好的方式。

以下是筆者要求的條件

- 想透過 GitHub Actions 中的 workflow 完成 
- 如果 forPackage 分支已存在則將其刪除    
- 從 main 建立新的 forPackage 分支    
- Assets/Modules 的所有子目錄(同時有 "package.json" 與 "Samples"資料夾)，將該子目錄的 "Samples資料夾" 重新命名 為 "Samples~資料夾"    
- 並提交更新    

將產出的 yml 做一點微調即可。主要文件操作的出錯率很高，find 指令似乎是有些眉角，等有空再回頭研究。

## 想要連接到存儲庫的特定分支並下載特定目錄下的內容

最後調整一下訪問的格式即可。

透過 Add package from git URL
> HTTPS_URL_Address?path=Target_Path#Branch

- HTTPS_URL_Address : https://github.com/user/repo.git
- Target_Path : Assets/Modules/Core 該目錄就是有 package.json 那層
- #Branch : 指定分支是可選的
