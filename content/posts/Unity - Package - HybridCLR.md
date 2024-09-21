---
title: "Unity - Package - HybridCLR"
date: 2023-04-11 21:11:00
draft: false

tags: ["Unity"]
---

## 先備知識

### Assembly Definition (Asmdef)
Unity 2017.3 以上版本的提供功能，主要解決龐大的程序集編譯時效率問題。

具體內容建議閱讀 [Doc - Assembly definitions](https://docs.unity3d.com/Manual/ScriptCompilationAssemblyDefinitionFiles.html)

### Assembly-CSharp.dll
Unity 預設整合的 dll，專案內未被自定義 Asmdef 劃分的腳本都會被整合到 Assembly-CSharp.dll

---

## 簡述
- [HybridCLR](https://hybridclr.doc.code-philosophy.com/)
- [focus-creative-games/hybridclr](https://github.com/focus-creative-games/hybridclr)
- [focus-creative-games/hybridclr_trial](https://github.com/focus-creative-games/hybridclr_trial)

HybridCLR 筆者已經應用於工作環境好一陣子了(從 2.X 版本開始)，其最讓人驚豔的地方在於，過往的開發流幾乎不用更動(當然要好 Asmdef 的規劃)，僅在打包時調整一下工作流即可。

其極大簡化過往麻煩且效率不彰的熱更流程。xLua 和 ILRuntime 在筆者看來最難受的事是「侵入性」極強，搞得綁手綁腳。大家也都抱怨很久了，但也沒有其他可靠方案，直到 HybridCLR 出現。

## 快速上手
3.0 版本後流程優化得更順暢了，照著 [文件](https://hybridclr.doc.code-philosophy.com/#/beginner/quickstart) 可以很快地感受到其威力。

## 注意
- [请问，Generate All、补充元数据的DLL更新的执行时机的最佳实践？](https://github.com/focus-creative-games/hybridclr/issues/57)
- [怎么卸载热更dll](https://github.com/focus-creative-games/hybridclr/issues/19)
- CLI 規範中只能以 AppDomain 形式卸載所有 dll，不支持卸載單獨的 dll。而 il2cpp 是單例 AppDomain，因此這個要求是不符合規範的。要採用 HybridCLR DHE 的商業方案。不過筆者倒是不太擔心，畢竟 Unity client 通常不是需要常駐的應用，使用者也不太會把應用的每一個功能都點一遍，初估是還可以接受的。