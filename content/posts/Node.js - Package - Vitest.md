---
title: "Node.js - Package - Vitest"
date: 2024-07-02 08:11:00
draft: true

tags: ["Node.js"]
---

## Guide
- [Vitest](https://vitest.dev/)

## Coverage

這些數值表示了測試覆蓋率的不同方面，具體如下：

1. **% Stmts (Statements Coverage)**：
   - **說明**：表示程式碼中所有執行語句的覆蓋率。這個百分比告訴你測試運行時執行了多少語句。
   - **例如**：如果程式碼中有 100 行執行語句，而測試覆蓋了其中的 80 行，則此覆蓋率為 80%。

2. **% Branch (Branches Coverage)**：
   - **說明**：表示條件分支的覆蓋率（如 if/else、switch/case）。這個百分比告訴你程式碼中所有可能的邏輯分支是否被測試覆蓋。
   - **例如**：如果有 10 個 if/else 條件，但只有 7 個條件分支在測試中執行過，則此覆蓋率為 70%。

3. **% Funcs (Functions Coverage)**：
   - **說明**：表示函數的覆蓋率。這個百分比告訴你測試運行時，程式碼中定義的函數中有多少被調用和覆蓋。
   - **例如**：如果程式碼中有 20 個函數，而測試覆蓋了其中的 15 個，則此覆蓋率為 75%。

4. **% Lines (Lines Coverage)**：
   - **說明**：表示實際被執行的行數覆蓋率。這與 % Stmts 類似，但更精確地計算了具體的行數。
   - **例如**：如果程式碼中有 200 行代碼，而測試覆蓋了其中的 180 行，則此覆蓋率為 90%。

5. **Uncovered Line #s**：
   - **說明**：列出未被測試覆蓋的具體行號。這些是測試未執行到的程式碼行，你可以根據這些行號來調整和增加測試用例，從而提高測試覆蓋率。

這些指標有助於你了解測試覆蓋率的具體情況，並確保你的程式碼在不同方面都得到充分的測試。

## Extra
### 必要時使用括 [弧表示法](https://www.typescriptlang.org/docs/handbook/2/classes.html#caveats) 訪問屬性private
```typescript
expect(inst["_somePrivateProp"]).toBe("foo"); // OK
```




