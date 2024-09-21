---
title: "Hugo - Hello Blog"
date: 2022-11-05 20:05:00
draft: false

tags: ["Hugo", "Blog"]
---

## Blog
起初筆者覺得使用 Github Repository + Markdown 當作筆記就足矣。但隨著筆記越多越雜，只使用文件夾結構 + 目錄超連結，在查找上越覺得不便，還是需要有一套系統來代勞。Blog/筆記 平台玲瑯滿目，但寄身於平台的風險難以忽視(倒站/政策改變)，網站搬家也讓人很頭疼。之前就知道靜態網站能架在 Github 上，只是一直沒研究，剛好趁這個機會練習一下 Web 前端的技能。最後的方案是 Github Pages + Hugo。

## Hugo
網上的教學也很多，筆者先是快速瀏覽一下幾篇文章再動工，這裡就不手把手介紹，這主要記錄一些筆者遇到的坑。
- [Hugo 貼身打造個人部落格系列](https://ithelp.ithome.com.tw/articles/10235097) 
- [網站開張！在 GitHub Pages 架設 Hugo 靜態網站](https://www.zoeydc.com/zh/posts/2021-05-23-hugo-website_github-pages_custom-domain/)

### 開始
官方的文件 [Official Doc](https://gohugo.io/getting-started/) 已經足夠清楚了，照著 Quick Start 跑完就有一個完整的畫面(以靜態網站來說)，但這裡有幾個注意的點。

- 使用 Binary (Cross-platform) 配置 Hugo 時，有 hugo / hugo_extended 版本，且要手動配置環境變數。extended 支援 Sass/SCSS，這裡沒注意到花了不少時間，想說改個主題佈局怎麼編譯不過，[Hugo Discourse Support](https://discourse.gohugo.io/t/tocss-ressource-not-found-in-file-cache/24858)。
- 設置 [.gitignore](https://github.com/github/gitignore/blob/main/community/Golang/Hugo.gitignore)

### 主題
主題有很多選擇 [Official Link](https://themes.gohugo.io/) / [Github Tag - hugo-theme](https://github.com/topics/hugo-theme)，有的已經打磨得很完善。筆者對這個 Blog 希望以簡潔明快為主，紀錄是第一要務。最終採用這個 [Theme - Cactus](https://github.com/monkeyWzr/hugo-theme-cactus) (變心可換問題不大)，之後肯定會進行一些魔改的，不然自架的意義就小很多了。

選擇上幾點注意
- 避開一些太舊的主題 (跟 Hugo 衝突 / js腳本過舊...)
- 第三方 API 遇到大改動時要排除一下才能建置 ( FB / IG 讓好多主題要改...)

修改上幾點注意
- 不要直接修改主題範本文件，使用 git submodule add 導入主題 
- 要修改的文件從主題範本 複製(文件夾結構要相同) 出來到根目錄，Hugo 會照優先度來處理 [Official Link](https://gohugo.io/templates/lookup-order/)
- Syntax Table [Chroma Playground (v2.2.0)](https://swapoff.org/chroma/playground/)

### 部署
- [Official Link - Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
- 部署後網頁畫面未更新，先等個幾分鐘，再不行就清理瀏覽器快取

## 後話
距離上次摸 html + css 也好一段時間，格式規則都快忘光，改主題撞牆了好一會兒，之後再到處去扒樣式。之後預計要補上
- VSCode 用到的模組
- 站內搜尋 (似乎可以使用 Fuse.js)
- C# syntax highlighting 上的很爛得再想想
