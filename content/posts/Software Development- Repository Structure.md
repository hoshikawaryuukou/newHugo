---
title: "Software Development- Repository Structure"
date: 2024-08-12 21:05:00
draft: false

tags: ["Software Development"]
---

## Quick Chat
最近筆者在開發公司的共用套件時，踩了不少坑，尤其是在儲存庫結構方面。

最初選擇了 polyrepo 的結構，但隨著開發的進展，碰到了一些問題：
- 要確保這些獨立的 repo 配置能夠同步。
- 每次發佈都需要逐一更新每個套件，尤其是那些有兩三層依賴的，讓發佈變得非常繁瑣。
- 進行 code review 時，還要不停地在不同 repo 之間切換。

為了改善這些問題，開始研究 monorepo 的結構：
- 使用 pnpm workspace 來構建。
- 雖然 monorepo 有一些權限控管的隱憂，但因為共用套件的開發人數不多，所以目前還不用太擔心協作上的衝突。

## Guide
- [monorepo-vs-polyrepo](https://github.com/joelparkerhenderson/monorepo-vs-polyrepo)
- [你很常聽到 monorepo，但為什麼要用 monorepo?](https://www.explainthis.io/zh-hant/swe/why-use-monorepo)

### monorepo
- [Managing a full-stack, multipackage monorepo using pnpm](https://blog.logrocket.com/managing-full-stack-monorepo-pnpm/)
- [Live types in a TypeScript monorepo](https://colinhacks.com/essays/live-types-typescript-monorepo)
- [Building a Typescript + NodeJS Monorepo in 2024](https://www.gfor.rest/blog/node-ts-monorepo)



<!-- ### Other
- https://blog.logrocket.com/boost-your-productivity-with-typescript-project-references/
- https://daveiscoding.hashnode.dev/nodejs-typescript-monorepo-via-npm-workspaces#heading-separate-source-code-and-build-output
- https://moonrepo.dev/docs/guides/javascript/typescript-project-refs
- https://segmentfault.com/a/1190000039157365
- https://www.javierbrea.com/blog/pnpm-nx-monorepo-01/
- https://juejin.cn/post/7215963267503161403
- https://bit.dev/blog/painless-monorepo-dependency-management-with-bit-l4f9fzyw/?utm_source=pnpm&utm_medium=workspace_page
- https://juejin.cn/post/7181720787400228925
- https://juejin.cn/post/7098609682519949325?from=search-suggest#heading-6
- https://juejin.cn/post/7139502662080266247?from=search-suggest
- https://blog.emmanuelisenah.com/setting-up-a-monorepo-using-pnpm-workspaces-with-typescript-and-tailwind
- https://juejin.cn/post/7136104350912348174
- https://medium.com/dcardlab/nx-vs-turborepo-%E6%80%8E%E9%BA%BC%E5%9C%A8%E5%A4%A7%E5%9E%8B-monorepo-%E5%84%AA%E5%8C%96%E9%96%8B%E7%99%BC%E9%AB%94%E9%A9%97-3354ff78a0cf
- https://github.blog/open-source/git/bring-your-monorepo-down-to-size-with-sparse-checkout/ -->


