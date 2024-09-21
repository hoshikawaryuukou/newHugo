---
title: "Node.js - Package - Prettier"
date: 2024-09-05 08:11:00
draft: false

tags: ["Node.js"]
---

## Quick Chat
Prettier 是一個代碼格式化工具，用於保持代碼風格一致。

## Guide
- [Prettier · Opinionated Code Formatter](https://prettier.io/)
- [playground](https://prettier.io/playground/)
- [如何配置 prettier](https://juejin.cn/post/7406891999376261146#heading-1)

## Install
```bash
pnpm add -D prettier
```

## VSCode
- 擴充功能 : [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- 啟用 Editor : Format on Save
- 選擇 Default Formatter 為 Prettier - Code Formatter

## Configure
- `.prettierrc` : [Configuration File · Prettier](https://prettier.io/docs/en/configuration.html)
- `.prettierignore` : [Ignoring Code · Prettier](https://prettier.io/docs/en/ignore.html)

## Plugins
- prettier-plugin-organize-imports : 排序/合併/移除未使用的 import 聲明

```json
{
  "plugins": ["prettier-plugin-organize-imports"]
}
```

## Issue
### 當跨平台協同的時候會有結尾符的問題
- [[eslint] Delete CR eslint(prettier/prettier) issue](https://bobbyhadz.com/blog/eslint-delete-cr-prettier#set-endofline-to-auto-in-your-prettierrcjs-file)
- [令人困擾的git autocrlf – Opass Life](https://blog.opasschang.com/confusing-git-autocrlf/)

於 `.prettierrc` 新增參數
```json
{
  "endOfLine": "auto"
}
```
