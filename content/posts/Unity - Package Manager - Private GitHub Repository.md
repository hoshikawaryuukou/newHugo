---
title: "Unity - Package Manager - Private GitHub Repository"
date: 2023-12-24 21:11:00
draft: false

tags: ["Unity", "UPM"]
---

## 情境

想分享私有庫但又不想去更改團隊或人員權限，Github 提供 Fine-Grained Token 能做到客製化的權限控制

## 操作

1. 至 GitHub  <<**帳戶設定**>>（非儲存庫設定）
2. Developer Settings  ->  Personal Access Tokens -> Fine-Grained Tokens
3. 生成 Token (**Read-Only Permission** for the repo **Content**).

```bash 
"com.yourusername.yourpackage": "git+https://x-oauth-basic:<token>@<repo>?path=<folder>"
```

## Ref
- [Install Unity Package from a private GitHub repository](https://medium.com/@dasannikov/install-unity-package-from-a-private-github-repository-9a40066b335f)