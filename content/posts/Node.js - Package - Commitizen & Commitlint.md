---
title: "Node.js - Package - Commitlint & Commitizen"
date: 2024-07-12 08:11:00
draft: false

tags: ["Node.js"]
---

## Quick Chat
Commitlint 是一個用來檢查 git commit 信息格式的工具，它可以配合多種規範使用。

Commitizen 則是一個幫助你格式化 git commit 信息的工具，依照預設的格式進行規範。

## Guide
- [commitlint](https://github.com/conventional-changelog/commitlint)
- [commitlint doc](https://commitlint.js.org/)
- [cz-cli](https://github.com/commitizen/cz-cli)

> 對於 Windows 使用者：確保所有 husky 檔案均已UTF-8編碼。如果使用任何其他格式，則可能會在執行時拋出錯誤，例如無法執行二進位檔案。

## Install Commitlint
```bash
npm install --save-dev @commitlint/{cli,config-conventional}
```

## Configuration - commitlint.config.js
```js
export default { extends: ['@commitlint/config-conventional'] };
```

## Configuration - .husky/commit-msg
```
npx --no-install commitlint --edit $1
```

## Install Commitizen
```bash
npm install -g commitizen
commitizen init cz-conventional-changelog --save-dev --save-exact
```

## Run Commitizen
```bash
git cz
```
