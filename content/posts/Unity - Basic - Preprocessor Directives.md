---
title: "Unity - Basic - Preprocessor Directives"
date: 2023-07-07 21:11:00
draft: false

tags: ["Unity", "CSharp"]
---

## 前述

中文稱作 : 前置處理器指示詞

筆者最近接觸到的遺舊專案中發現裡面大量地使用 條件式編譯 
```csharp
#if DEBUG
    Console.WriteLine("Debug version");
#endif
```

筆者之前有使用也基本只使用 定義區域 (排版效果)
```csharp
#region MyClass definition
    public class MyClass
    {
        static void Main(){...}
    }
#endregion
```

Unity 在處理平台裝置時也蠻常會出現的
```csharp
public class PlatformDefines : MonoBehaviour 
{
  void Start () 
  {
    #if UNITY_EDITOR
      Debug.Log("Unity Editor");
    #endif

    #if UNITY_IOS
      Debug.Log("iOS");
    #endif

    #if UNITY_STANDALONE_OSX
        Debug.Log("Standalone OSX");
    #endif

    #if UNITY_STANDALONE_WIN
      Debug.Log("Standalone Windows");
    #endif
  }          
}
```

## 問題
那前置處理器指示詞有什麼問題呢? (參考日文那個 Ref 有比較明確的 Case)

- 編譯版本至少會是 2^(指示詞的分類數)種，持續的調試和測試變得非常困難。
- Unit Test 中難以使用。
- 編譯檢查不起作用。
- 當巢狀結構出現時可讀性將大為降低。

上述這些狀況都會導致 **延後發現問題的時間 !**

## 方案
這個前置處理器指示詞一直是個蠻有爭議的作法，有一派人士是不使用的(通過使用條件分支、策略模式或依賴注入等其他方式，更可以清晰地表達了代碼的邏輯，提高了程式的可維護性)。

筆者也傾向不使用(業務邏輯不用，其餘的看狀況)。

### Case. Editor
有時後會有需要客製編輯器時，會這樣跟 MonoBehaviour 寫在一起並用 UNITY_EDITOR 處理。但事實上獨立一個檔案放在 **Editor 資料夾** 應該會更好。
```csharp
#if UNITY_EDITOR
...
#endif
```

### Case. RuntimePlatform
```csharp
public void Run() 
{
    if (Application.platform == RuntimePlatform.Android) 
    {
        new ClassForAndroid().Execute();
    } 
    else if ...
}
```

### Case. 減少指示詞的影響範圍(非得使用指示詞)
ConditionalAttribute 官方文件也有推薦此作法。
```csharp
[Conditional("DEBUG")]
private void DebugLog(string message)
{
    Debug.Log(message);
}
```

透過定義介面(需求上允許的話)，來讓影響範圍控制在實例化階段。
```csharp
#if UNITY_EDITOR
var runner = new EditorRunner();
#elif UNITY_IOS
var runner = new IOSRunner();
#elif UNITY_ANDROID
var runner = new AndroidRunner();
#endif
```

## Ref
- [C# 前置處理器指示詞](https://learn.microsoft.com/zh-tw/dotnet/csharp/language-reference/preprocessor-directives)
- [macroのカジュアル多用は危険](https://zenn.dev/mattak/articles/3ef65fd8c9db63)
- [Conditional Compilation](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html)