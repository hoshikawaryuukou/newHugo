---
title: "Documentation - README"
date: 2024-06-18 21:11:00
draft: false

tags: ["Documentation"]
---

## Quick Chat
最近筆者從 Unity 轉向了 Node.js，因此花了大量時間在 npm 上尋找合適的套件。大部分的 README 都寫得很清晰，但也有少數寫得難以理解。

README 是 Repository 的門面，這是毋庸置疑的。創建一個好的自述文件，可以向用戶（包括使用者和開發者）顯示基本信息，但不應該用他們可能不需要的內容來淹沒他們。

筆者認為應該從一開始就認真對待 README，而不是在最後(專案收尾之際)才一股腦地將資訊灌入，這樣會降低其品質。

## Guide
- [你知道對專案來說，README.md 有多麼重要嗎？ ── 工程師血淚史](https://medium.com/dean-lin/%E4%BD%A0%E7%9F%A5%E9%81%93%E5%B0%8D%E5%B0%88%E6%A1%88%E4%BE%86%E8%AA%AA-readme-md-%E6%9C%89%E5%A4%9A%E9%BA%BC%E9%87%8D%E8%A6%81%E5%97%8E-%E5%B7%A5%E7%A8%8B%E5%B8%AB%E8%A1%80%E6%B7%9A%E5%8F%B2-c0fb0908343e)
- [README 的藝術](https://github.com/hackergrrl/art-of-readme/blob/master/README-zh-TW.md)

## Markdown + Vscode 
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [Markdown Preview Github Styling](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-preview-github-styles) 

## Template
- [README-Template.md](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
- [GitHub README Templates](https://www.readme-templates.com/)

## Strategy 

### 為誰而寫 
必須意識讀文件的人分成使用者和開發者，README 在佈局上要有明確的邊界。
- 以使用者角度
  - Tutorial
  - Reference 
- 以開發者角度
  - 環境設定/測試/部署/發布方法
  - 開發流程/編碼規範等 

### 避免 README 過長 
這個視專案而定，當 README 內容越來越多時可以考慮將其拆分至其他文檔，而 README.md 則改做為文檔的索引頁。
- README.md
- RELEASELOG.md
- CHANGELOG.md
- CONTRIBUTING.md
- ./docs/Tutorials/xx.md
- ./docs/Examples/xx.md

### 避免 Header 過度使用 
原本寫作時會下意識的使用不少的三級標題 `### Header`
``` 
## Header2

### Header3
分段...

### Header3
分段...
```

但這次觀察 READMEs 的過程，看到不少以下這種不多做一些分段的寫法

``` 
## Header2
直接承接本文段落...
```

原本以為會很難閱讀，但實際上閱讀時都是順著讀下來，所以好像不會有負面影響。反倒是原先 Header3 過多造成畫面有點割裂。
