---
title: "Node.js - Package Manager - pnpm"
date: 2024-09-07 21:11:00
draft: false

tags: ["Node.js"]
---

## Doc
- [pnpm](https://pnpm.nodejs.cn/) 

## Guide
- [为什么现在我更推荐 pnpm 而不是 npm/yarn? ](https://www.cnblogs.com/cangqinglang/p/14448329.html)
- [pnpm、npm、yarn 包管理工具『优劣对比』及『环境迁移』](https://juejin.cn/post/7286362110211489855?searchId=20240731105621AD124E03A93B1AB5027A)
- [从pnpm工具了解整个npm包核心管理原理](https://qborfy.com/today/20230219.html)
- [為什麼 pnpm 比 npm 更快且更省空間？](https://www.explainthis.io/zh-hant/swe/why-is-pnpm-faster)

## Install
```bash
npm i -g pnpm
npm i -g pnpm@latest
pnpm self-update
```

## 管理 Node.js 的執行環境
- pnpm env use --global lts : 安裝並使用 LTS 版本 
- pnpm env use --global {version} : 安裝並使用指定版本
- pnpm env add --global {version} : 僅安裝指定版本
- pnpm env remove --global {version} : 移除指定版本
- pnpm env list : 列舉本地所有版本
- pnpm env list : 列出線上可用的版本

## 管理 packages
- pnpm outdated : 檢查套件是否有更新
- pnpm update --latest : 更新所有依賴至最新
- pnpm store prune : 會清理掉不再被專案引用的包

## Workspace - Monorepo
- [Monorepo与pnpm：前端项目管理的完美搭档](https://juejin.cn/post/7357546247848198182)
- [为什么 pnpm+monorepo 是组件库项目的最佳实践](https://juejin.cn/post/7316409548994625574?searchId=20240731105621AD124E03A93B1AB5027A)
- [Monorepo？來聊聊另一種專案管理架構吧！](https://israynotarray.com/other/20240413/3177435894/)
- [从npm版本依赖到Monorepo大仓项目](https://qborfy.com/today/20230107.html)
- [MonoRepo实战：pnpm+nx搭建MonoRepo项目](https://qborfy.com/today/20230225.html)

### 特色
- 👍 package 使用相同版本 **依賴/設定檔/風格**。
- ⚠️ package 權限控管需仰賴其他工作流。

### 配置 root package.json 
以下指令產生一個基本的 `package.json`
```bash
pnpm init
```

### 在專案中限用 pnpm
⚠️ 但目前 npm hook - preinstall 未如預期運作。
```json
{
  "scripts": {
    "preinstall": "npx only-allow pnpm"
  }
}
```

### 配置 pnpm-workspace.yaml
該檔案聲明這是一個 Monorepo 專案。工作區下的 package 會有各自的 `package.json`，並且執行 `pnpm install` 時自動安裝所有 package 的相依套件。

```yaml
packages:
  - 'packages/*'
```
- `packages` 字段列出了工作區包含的 package 位置。


### 專案基本結構
```
- Git
  - pnpm-workspace.yaml
  - package.json
  - packages
```

### workspace 指令/參數
- pnpm add -wD `<pkg>` : 添加依賴於工作區
- pnpm remove -wD `<pkg>` : 移除依賴從工作區
- pnpm install : 安裝所有依賴
- pnpm `<commnad>` : 執行命令
- pnpm --filter `<package_selector>` `<command>` : 執行 package 命令
