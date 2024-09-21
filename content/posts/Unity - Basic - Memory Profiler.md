---
title: "Unity - Basic - Memory Profiler"
date: 2023-07-30 21:11:00
draft: false

tags: ["Unity"]
---

## 注意
- 由於Unity 無法將性能分析器本身佔用的記憶體與運行模式的記憶體完全分開。要獲得應用程序的更精確數字和記憶體使用情況，應在要運行應用程序的目標設備和操作系統上分析應用程序。
- 如果需要在記憶體受限的平台上運行應用程序，設備上的總駐留量對於檢查低記憶體警告和由於記憶體耗盡而強制關閉非常有用。作為一般規則，它不應超過設備上可用總物理內存的 70%。
- 偵測 Leaked Managed Shell 的功能在 Memory Profiler 1.1.0-pre.1 

## Ref
- [Memory Profiler](https://docs.unity3d.com/Packages/com.unity.memoryprofiler@1.0/manual/index.html)
- [Memory Profiler | 1.1.0-pre.1 - Unity - Manual](https://docs.unity3d.com/Packages/com.unity.memoryprofiler@1.1/manual/managed-shell-objects.html)
- [Unity でメモリリーク？ Memory Profiler で Leaked Managed Shell をチェックしてみよう！](https://www.youtube.com/watch?v=UIwQmpQTtA4)
- [Inspecting memory with the new Memory Profiler package](https://blog.unity.com/engine-platform/inspecting-memory-with-the-new-memory-profiler-package)
- [Memory Profiler로 애플리케이션의 물리적 메모리 사용량 분석](https://unitysquare.co.kr/growwith/unityblog/webinarView?id=387&utm_source=facebook-page&utm_medium=social&utm_campaign=korea_memoryprofilerapp387)
- [Unity内存分析与优化实践(1.1版本前)](https://blog.csdn.net/Nbin_Newby/article/details/131537227)