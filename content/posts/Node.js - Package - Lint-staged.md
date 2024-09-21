---
title: "Node.js - Package - Lint-staged"
date: 2024-07-11 08:11:00
draft: false

tags: ["Node.js"]
---

## Quick Chat
lint-staged 可以只對 git staged 的檔案執行 lint 檢查，進而提升檢查效率。

## Guide
- [lint-staged](https://github.com/lint-staged/lint-staged#installation-and-setup)

> 值得注意的是跟 Prettier 搭配使用，必須確保 ESLint 在 Prettier 前面先執行。

## Install
```bash
npm install --save-dev lint-staged
```
## Configuration - package.json
```json
{
  "scripts": {
    ...
  },
  "lint-staged": {
    "*.{ts,js}": [
      "eslint"
    ]
  }
}
```

## Configuration - .husky/pre-commit
```
npx lint-staged
```