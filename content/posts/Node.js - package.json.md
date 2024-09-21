---
title: "Node.js - package.json"
date: 2024-07-26 21:11:00
draft: false

tags: ["Node.js"]
---

## Quick Chat
可以將 package.json 檔案新增到套件中，以便其他人可以輕鬆管理和安裝。發佈到註冊表的包必須包含一個 package.json 檔案。

- [Creating a package.json file](https://docs.npmjs.com/creating-a-package-json-file)

## Quick Start
根據當前目錄產生預設 package.json  
`npm init -y`

## Fields 
### name
必須是小寫字母和一個單詞，並且可以包含連字符和下劃線

### version 
遵循語義版本控制準則 `x.x.x` 

### type  
指定 module system 要用 
- ES : "module"
- CommonJS : "commonjs"

### main
當套件被作為 CommonJS 模組引入時，預設的入口點。

### module
當套件被作為 ES 模組引入時，預設的入口點。

### types
TypeScript 的類型定義檔案位置，提供 TypeScript 支援。

### exports
是一個較新的欄位，用來細化和取代傳統的 main 和 module 欄位。它允許你為不同的環境（例如 Node.js、ES 模組、瀏覽器）定義不同的入口點和模組格式。它還允許你控制哪些檔案可以被使用者匯入，提供更多的安全性和靈活性。

如果有 exports 欄位，Node.js 會優先使用 exports 來決定如何載入模組，只有在 exports 中沒有相應定義時，才會回退到使用 main、module 和 types 欄位。

```json
{
  "exports": {
    ".": {
      "types": "./build/types/lib.d.ts",
      "require": "./build/cjs/lib.js",
      "import": "./build/esm/lib.js",
      "default": "./build/esm/lib.js"
    }
  }
}
```

- [Multiple exports with types in a Typescript Package](https://www.nullfox.com/multiple-exports-typescript-package-types)

```bash
/my-package
│
├── /dist
│   ├── index.js
│   ├── utils.js
│   └── internal.js
│
└── /lib
    └── helper.js
```

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "exports": {
    ".": "./dist/index.js",
    "./utils": "./dist/utils.js",
    "./lib/helper": "./lib/helper.js"
  }
}
```

⛨ 限制訪問
- 如果 internal.js 沒有在 exports 中明確列出，使用者將無法通過 import "my-package/internal" 來訪問它，這樣保護了內部實現細節不被暴露給外部使用者。

### engines
```json
{
  "engines": {
    "node": ">=20.1.0"
  }
}
```

### files
指定當發布專案時應該包含在內的文件或資料夾，白名單。
```json
{
  "files": [
    "dist/",
    "index.js"
  ]
}
```

⚠️ 黑名單的作法 `.npmignore 文件`，但建議使用 **files 字段**，顯式聲明較為安全。
