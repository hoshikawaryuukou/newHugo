---
title: "Software Design - Navigation"
date: 2022-11-16 21:11:00
draft: false

tags: ["Software Design"]
---

以下 Feature 指的是一個功能獨立的模組，Feature A 將簡稱 A。

## 問題
> 應用程式中有一個由 A 到 B 的**導航**，那這個**導航**是誰的責任? 

以下先討論 2 種狀況。

### A 直接依賴 B
簡單粗暴的強耦合破壞了 A 的獨立性。當流程發生變化時，可能需要到各個 Feature 去修改。
```
Feature A -> Feature B
```
### A 引入導航器間接依賴 B
這作法將導航操作收斂到某個類中，但 A 仍然隱含的知道 B，這同樣破壞了 A 的獨立性。
```
Feature A -> INavigator.Route(View.FeatureB) // Enum
or
Feature A -> INavigator.Route("FeatureB") // 魔術字串
or
Feature A -> INavigator.RouteFeatureB()
```
<br>

重新思考導航這件事
- Feature 應該知道自己是能夠 **被導航** 或是 **能導航到哪** 嗎?
- 到底 A 能導航到 B 這件事是誰決定的?

應該隱約地感覺到了吧，導航並不屬於 A 也不屬於 B，**導航是一個獨立操作**，需要一個額外的單位來負責。此外這個單位多是屬於 App 級別的(因為該層級有對其他模組的正當訪問性，畢竟是負責做統合的)。

## Navigation

有以下核心概念
 - Feature 對導航一無所知 (因此也不知道其他 Feature 的存在)
 - Feature 只是向外**告知自己的狀態**(透過介面/觀察者/事件...)
 - 並使用 **中介者模式 (Mediator pattern)** 來處理 Features 之間的關係

也就是將模組的依賴關係轉成下方這張圖
![Navigator](/images/Navigator.png)

以 FeatureA 定義介面並呼叫，Navigator 實作介面為例 (觀察者/事件 相對好實作，相信大家有能力自己應用。介面的寫法比較繞，所以特別寫出來)
```csharp
//注意命名空間! 
namespace App.Features.FeatureA.Presentation
{
    public interface IClassicGameNavigator
    {
        UniTaskVoid NavigateBack();
    }

    public class GameController
    {
        private readonly IFeatureANavigator navigator;

        ...

        private void Exit()
        {
            navigator.NavigateBack();
        }
    }
}

//注意命名空間! 導航是自己獨立的模組
namespace App.Navigators
{
    public class FeatureANavigator : IFeatureANavigator
    {
        private readonly IFeatureLoader featureLoader;

        ...

        public async UniTaskVoid NavigateBack()
        {
            await featureLoader.Unload(FeatureKeys.FeatureA);
            await featureLoader.Load(FeatureKeys.Lobby);
        }
    }
}
```

### Extra

有注意到 Loading Screen (Transition 也是導航的一部分) 是誰在控制的嗎? 如果是 A 或 B，那現在也許有個更適合的位置!
```csharp
namespace App.Navigators
{
    public class AppNavigator
    {
        private readonly IFeatureLoader featureLoader;
        private readonly ILoadingScreen loadingScreen;

        public AppNavigator(IFeatureLoader featureLoader, ILoadingScreen loadingScreen)
        {
            this.featureLoader = featureLoader;
            this.loadingScreen = loadingScreen;
        }

        public async UniTaskVoid NavigateToLobby()
        {
            await loadingScreen.FadeInAsync();
            await featureLoader.Load(App.FeatureKeys.Lobby);
            await loadingScreen.FadeOutAsync();
        }
    }
}
```

## 總結
- 找一個單位為導航負責
- 流程發生變化時易於修改(集中/可組合)
- 建議配合 DI 操作，將實例化複雜度排除在流程控制外

## Repo
使用相同概念的庫，星數都破千可以安心嘗試/觀摩。
- [RxFlow](https://github.com/RxSwiftCommunity/RxFlow)
- [XCoordinator](https://github.com/QuickBirdEng/XCoordinator)

## Reference
這種模式有很多名字 Coordinator/ FlowController/ Navigator，但觀念都雷同。連結都值得閱讀，多半都有作者們的想法與反思，也許閱讀後會有新的理解。此外大家的開發環境不同，需要自行做些調整(精簡或強化)。建議照順序閱讀以下連結。
- [The Coordinator](https://khanlou.com/2015/01/the-coordinator/)
- [In-App Navigation with Coordinators](https://hannesdorfmann.com/android/coordinators-android/)
- [Architecting iOS apps: Coordinators](https://blog.kulman.sk/architecting-ios-apps-coordinators/)
- [Coordinator and FlowController](https://github.com/onmyway133/blog/issues/106)
- [Coordinators Essential tutorial. Part I](https://medium.com/blacklane-engineering/coordinators-essential-tutorial-part-i-376c836e9ba7)
- [Coordinators on Android: how to build flows quickly with reusable screens](https://monzo.com/blog/coordinators-on-android-building-flows-quickly-with-reusable-screens)
- [MVVM + Coordinators + RxSwift and sample iOS application with authentication](https://wojciechkulik.pl/ios/mvvm-coordinators-rxswift-and-sample-ios-application-with-authentication)
- [How to pass data between views using Coordinator pattern in Swift](https://benoitpasquier.com/data-between-views-using-coordinator-pattern-swift/)
- [Navigators Part 1: a Flow-Based Architecture for Android](https://medium.com/@greg_63957/navigators-part-1-a-flow-based-architecture-for-android-b66df2fa6e79)
- [【画面遷移はUIKitに】SwiftUIにおけるFlowControllerを解説！](https://rookie-programmer.jp/?p=25)

### Extra
- [Introducing Nibel: A Navigation Library for Adopting Jetpack Compose in Fragment-Based Apps](https://medium.com/turo-engineering/introducing-nibel-a-navigation-library-for-adopting-jetpack-compose-in-fragment-based-apps-541c7b2f3f84)