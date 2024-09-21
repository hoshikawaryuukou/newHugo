---
title: "Node.js - Package - Husky"
date: 2024-07-05 08:11:00
draft: false

tags: ["Node.js"]
---

## Quick Chat
Husky 是一個用來在 Git 針對特定事件觸發自動執行腳本的工具，它的主要用途是確保在開發過程中執行特定的檢查或操作，例如代碼格式化、Lint 檢查、測試執行等。這些操作通常在開發人員 commit 或 push 代碼之前執行，從而提高代碼質量並避免不合規代碼進入代碼庫。

## Guide
- [Husky Doc](https://typicode.github.io/husky/zh/)
- [每周轮子之 husky：统一规范团队 Git Hooks](https://4ark.me/post/weekly-npm-packages-02.html/)

## Install
```bash
npm install --save-dev husky
```
## Configuration - 初始化
```bash
npx husky init
```
- 會在 `.husky/` 中創建 `pre-commit` 腳本
- 更新 `package.json` 中的 `prepare` 腳本
