---
title: "Software Design - Error Handling"
date: 2022-12-15 20:05:00
draft: true

tags: ["Software Design", "Pattern"]
---



- [Error Handling — Returning Results](https://medium.com/@michael_altmann/error-handling-returning-results-2b88b5ea11e9)
- [FluentResults](https://github.com/altmann/FluentResults)
- [Functional C#: Handling failures, input errors](https://enterprisecraftsmanship.com/posts/functional-c-handling-failures-input-errors/)
- [Flexible Error Handling w/ the Result Class | Enterprise Node.js + TypeScript](https://khalilstemmler.com/articles/enterprise-typescript-nodejs/handling-errors-result-class/)
- [Functional Error Handling with Express.js and DDD | Enterprise Node.js + TypeScript](https://khalilstemmler.com/articles/enterprise-typescript-nodejs/functional-error-handling/)
- [Exceptions for flow control in C#](https://enterprisecraftsmanship.com/posts/exceptions-for-flow-control/)
- [Control flow for invalid actions – Conditionals, try/catch and Booleans](https://programmingduck.com/articles/control-flow-invalid-actions)
- [5 Reasons Why Business Exceptions Are a Bad Idea](https://reflectoring.io/business-exceptions/)
- [When is it OK to use exception handling for business logic?](https://stackoverflow.com/questions/5378005/when-is-it-ok-to-use-exception-handling-for-business-logic)
- [Flexible Error Handling w/ the Result Class | Enterprise Node.js + TypeScript](https://khalilstemmler.com/articles/enterprise-typescript-nodejs/handling-errors-result-class/)
- [https://mikhail.io/2016/01/validation-with-either-data-type-in-csharp/](https://mikhail.io/2016/01/validation-with-either-data-type-in-csharp/)
- [A Small Result Type for C#](http://blog.s-schoener.com/2018-08-18-result-api/)
- [My take on the Result class in C#](https://josef.codes/my-take-on-the-result-class-in-c-sharp/) 
- [Using the result class in C#](https://achraf-chennan.medium.com/using-the-result-class-in-c-519da90351f0)
- [sschoener/Result.cs](https://gist.github.com/sschoener/95eb0a532e210c822b2f55e90b07b1a9)
- [A Small Result Type for C#](https://blog.s-schoener.com/2018-08-18-result-api/)
- [Getting Started With Ardalis.Result](https://blog.nimblepros.com/blogs/getting-started-with-ardalis-result/)
- [Result](https://github.com/ardalis/Result)
- [Error handling: Exception or Result?](https://enterprisecraftsmanship.com/posts/error-handling-exception-or-result/)
- [Pros and cons of using Result<T> (ASP.NET Core)](https://tpetrina.com/blog/2019-10-01-using-result)
- [C# 8 nullables and Result container](https://stackoverflow.com/questions/59702550/c-sharp-8-nullables-and-result-container)
- [Best way to return multiple results from a function in C# [closed]](https://softwareengineering.stackexchange.com/questions/431572/best-way-to-return-multiple-results-from-a-function-in-c)
- [Result object vs throwing exceptions](https://softwareengineering.stackexchange.com/questions/405038/result-object-vs-throwing-exceptions)
- [Flutter Exception Handling with try/catch and the Result type](https://codewithandrea.com/articles/flutter-exception-handling-try-catch-result-type/)
- [Recoverable Errors with Result](https://doc.rust-lang.org/book/ch09-02-recoverable-errors-with-result.html)
- [可恢复的错误 Result](https://course.rs/basic/result-error/result.html)
- [TypeScriptでResult型でのエラーハンドリングを通してモナドの世界を覗いてみる](https://qiita.com/shimopino/items/d194957599dd45e91a5f)
- [TypeScriptの「Result型」のすゝめ](https://speakerdeck.com/kodak4400/typescriptno-resultxing-nosu-me?slide=2)
- [TypeScriptのエラーハンドリングはResult型を使うのが良さそうだと思った話](https://qiita.com/Kodak_tmo/items/d48eb3497be18896b999)
- [ts-results](https://github.com/vultix/ts-results?tab=readme-ov-file#option-example)
- [fp-ts](https://www.npmjs.com/package/fp-ts)
- [neverthrow](https://github.com/supermacro/neverthrow)








-----------------

if a failure is expected behavior, then you shouldn't be using exceptions
如果失敗是預期的行為，那麼你不應該使用異常
異常表示某些超出相關代碼預期行為範圍的事情。
但是，如果您正在對外部輸入進行一些檢查，這是因為您預計某些消息會失敗 - 如果失敗是預期的行為，那麼您不應該使用異常。

CQS 原則相同的方式提高了可讀性。它不僅可以讓您知道方法是命令還是查詢，還可以讓您查看該方法是否可能失敗。
重點在讓你很快從名字的推理出有無副作用
Result 也是一樣的

當然 Result 的弊端就是 你忽略他

那甚麼時候用例外?
寫給別人用
用別人寫的

----------------
# Error Handling

## Keypoint
* If a failure is expected behavior, then you shouldn't be using exceptions.

## Strategy
* 以下是使用 C# 操作
* 並非要找一個萬用解，必須因地制宜

### 返回執行結果
```csharp
// 錯誤碼 魔術數字能避則避
public int DoXXX() => return logic(); // 200/404...

// 結果狀況明確(從方法名即可判斷)考慮使用
public bool DoXXX() => return logic();
public Response DoXXX() => return logic(); // Successful/Error_XXX/Error_XXO
```

### Try / Catch
```csharp
try{ DoXXX(); }
catch (OOXXException ex)
{
   //code specifically for a OOXXException
}
```
標準的例外處理，但應該避免 Exception as control flow




### Tester-Doer
### Try-Parse(Do)
### Result

## Keywords
* Exception as control flow ⚠️
* Exception/Error Handling
* Business Exception

