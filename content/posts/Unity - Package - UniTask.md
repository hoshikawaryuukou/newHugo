---
title: "Unity - Package - UniTask"
date: 2024-02-10 21:11:00
draft: false

tags: ["Unity"]
---

## 前述

UniTask - Unity 中實現效能最好的 async/await 的函式庫
- [Cysharp/UniTask](https://github.com/Cysharp/UniTask)

Unity 中預設的非同步實現是 - [Coroutine 協程](https://docs.unity3d.com/2022.3/Documentation/Manual/Coroutines.html)，但協程有以下缺點
- 無法使用回傳值，需使用 callback 來解決。
- 異常處理很困難，因為不能在 try-catch 區塊內使用 yield。
- 需透過 MonoBehaviour.StartCoroutine 才能啟動。

UniTask 相較於 C# 原生的 Task 做了以下改進
- 刪除了 Task 在 Unity 不需要的功能。
- 非 MonoBehaviour 裡也能實現非同步。
- 記憶體/ GC / Unity PlayerLoop 等方面做最佳化。
- UniTaskTracker 提供編輯器上可視化追蹤 await 狀態，這對於檢查是否有洩漏很有用。

UniTask 官方文件的基本功能寫得相當清楚，並附上一些入門介紹
- [UniTaskを使おう！](https://hackmd.io/@-xLrSnFfROOeIeRnENCWcQ/Bke4eFcrd)
- [UniTask機能紹介](https://qiita.com/toRisouP/items/4445b6b9bf00e49eb147)

以下紀錄幾個重點主題

## Awaiter
UniTask 已經實作了相當豐富的 Awaiter 擴充，有需要自訂的可以參考以下規範
- [.NET 中什么样的类是可使用 await 异步等待的？](https://blog.walterlv.com/post/what-is-an-awaiter.html)

## Thread
- UniTask.SwitchToThreadPool 允許後續處理在執行緒池中進行。
- UniTask.SwitchToMainThread 切換到主執行緒，不會等待下一幀。
- 也可以使用 UniTask.Yield 切換到主執行緒，但它總是等待一幀。

但目前尚未有使用到的情境，之後有遇到再嘗試。
- [UniTaskを使えば並列処理で外部機器からデータを簡単に取得できますの紹介](https://qiita.com/matchyy/items/44986c3fee410e29e2e5)

此外使用執行緒池，將無法與 WebGL 等平台相容。未來應該也會避開使用。

## Cancellation
Cancel 算是在使用 Task-based 機制時最須留意的事項。UniTask 一旦被取消，且還在 await 的話，那麼 await 後面的程式碼就不會被執行。因此盡可能將 CancellationToken 傳遞給非同步方法。如果不能傳遞，則手動判斷。
```csharp
private async UniTask<string> ReadTxtAsync(string path, CancellationToken token)
{
    return await UniTask.Run(() => 
    {
        // 執行前檢查
        token.ThrowIfCancellationRequested();

        var str = File.ReadAllText(path);

        // 執行後檢查
        token.ThrowIfCancellationRequested();
        return str;
    });
}
```

當 Cancel 跟 MonoBehaviour OnDestroy 時機掛勾時，能透過 GetCancellationTokenOnDestroy 來取得對應的 CancellationToken。

在 WebGL 這種對性能要求比較高的情境，建議使用 SuppressCancellationThrow 函數，来避免 OperationCanceledException 抛出。

這裡有詳細探討與建議作法
- [【C#】async/awaitのキャンセル処理まとめ](https://qiita.com/toRisouP/items/60673e4a39319e69fbc0)


## Completion
- [【UniTask】UniTaskCompletionSourceを使って好きなタイミングで結果を確定させるUniTaskを生成する(ついでにUniTask.Voidの紹介)](https://www.hanachiru-blog.com/entry/2021/07/10/221719)
- [Cancel a CompletionSource with a cancellation](https://github.com/Cysharp/UniTask/issues/81#issuecomment-635752670)


## Timeout
- 建議使用 TimeoutController
- 不要忘記與現有的結合 CancellationToken 
- 避免使用 AttachExternalCancellation

## Extra
Unity 官方也將在 Unity 2023.1 之後逐步完善 async/await 機制
- [Await support](https://docs.unity3d.com/2023.2/Documentation/Manual/AwaitSupport.html)
- [【Unity 2023.1】 C# async/await 正式サポート？ Awaitable を使ってみよう！](https://www.youtube.com/watch?v=B2jiquau_TQ)
