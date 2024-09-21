---
title: "Software Design - Pattern - ViewModel"
date: 2023-08-27 20:05:00
draft: false

tags: ["Software Design", "Pattern"]
---

## 前述

此篇的實作參考到以下文件 (提到不少 Presentation layer 設計原則)
> [Android Developers 文件/指南/UI 層](https://developer.android.com/topic/architecture/ui-layer?hl=zh-tw)

該文件的更新頻率算高且會與時俱進，筆者印象中其架構設計從 MVVM -> Domain/Application Driven 設計，可以看出主流架構有產生變化。之後的討論雖然使用 ViewModel 但不會詳細介紹 MVVM 的細節，如果對 MVX 系列不熟，可以先讀筆者之前的文章 **<<通用設計 - Pattern - MVP>>** 裡面的 References。


## 探索

回到正題，筆者在最近的業務上遇到
> 如何在 **服務端未完成** 的情況下，讓 Client 獲得完整的體驗流 ?

以下用交叉反問的方式來分析問題

Q: 沒有服務端那資料來源哪來 ?    
A: 使用假資料    

Q: 當表現層依賴的是 IService Interface 使用假資料時需要實作什麼 ?    
A: 只需要實作一個 FakeService 來產生假資料即可    

Q: 當想要將業務與表現解耦時，很常使用中介者的手法來黏合兩者，如果使用標準的 MVP 實做，Presenter 實際做了哪些事呢 ?    
A: 監聽 View 事件/ 與 Service 互動/ 管理畫面狀態/ 呼叫 View 刷新    

Q: Presenter 似乎有點多事情 !    
A: 其實需要視情況而定，情況簡單時直接向 View 倒資料也是完全可以接受的。但當情況複雜時可以選擇導入 ViewModel 來管理狀態。事實上表現層所要呈現的 UI 狀態未必是只跟 Service 的回傳有關，可能需要這樣的控制 條件A(Service) + 條件B(Local) + 條件C(User Runtime) -> 狀態D    

Q: 也就是將 UI 狀態封裝於 ViewModel 裡管理 !    
A: 對於畫面需求可以定義於 IVewModel 介面，這樣就隔離了 Service(隱藏於 ViewModel 實作中)，畫面就可以獨立於 Service 開發，細節將於下一結討論    


## Mediator

![Mediator](/images/Mediator.png)

✽ FlowController 這裡視為進入點即可

(左邊)
- 採用標準的 MVP
- FlowController/Presenter 需做狀態管理 

(右邊)
- 採用 MVP 混用 ViewModel
- ViewModel 代替 Presenter 作為邏輯與畫面的中介
- FlowController/Presenter 依賴同為 Presentaion 的 IViewModel，這樣表現層邏輯就可以不依賴 Service 獨立開發，等之後在實作對應的 ViewModel 且能根據不同的狀態源(體驗版/正式版)

ViewModel 的優勢情境
- 單一職責: 明確的狀態管理單位
- 單向資料流: 排除了對 View/IView 的依賴，使用觀察者模式，供外部訂閱數據/變化
- 能對應狀態需要被共用的狀態: 得力於狀態被獨立出來，可被多個單位給使用


## Example

✽ 觀察者模式採用 UniRx 實作

以一個井字遊戲為例，情境如下

定義 IAppViewModel

```csharp
public interface IAppViewModel
{
    // 選單/設定/遊戲 的啟動狀態
    IReactiveProperty<bool> MenuActiveRP { get; }     
    IReactiveProperty<bool> SettingActiveRP { get; }  
    IReactiveProperty<bool> GameActiveRP { get; } 
}
```

定義 IGamePlayViewModel

```csharp
public interface IGamePlayViewModel
{
    // 回合數狀態
    IReactiveProperty<int> TurnRP { get; }

    // 點選成功事件
    IObservable<SelectResult> Selected { get; }

    // 點選失敗事件
    IObservable<string> SelectFailed { get; }
}
```

使用 AppFlowController 根據 IAppViewModel 去開關對應的 Presenter

```csharp
public class AppFlowController : IDisposable
{
    private readonly IAppViewModel appVM;
    private readonly GamePlayPresenter gamePlayPresenter;
    ...

    private readonly CompositeDisposable disposables = new();

    public AppFlowController(IAppViewModel appVM, GamePlayPresenter gamePlayPresenter, ...)
    {
        this.appVM = appVM;
        this.gamePlayPresenter = gamePlayPresenter;
        ...
    }

    public void Start()
    {
        disposables.Clear();
        appVM.GameActiveRP.Subscribe(OnGameActiveRP).AddTo(disposables);
        ...
    }

    public void Dispose()
    {
        disposables.Clear();
    }
}
```

使用 GamePlayPresenter 根據 IGamePlayViewModel 去更新遊戲畫面

```csharp
public class GamePlayPresenter
{
    private readonly IGamePlayViewModel vm;
    private readonly GamePlayView view;

    private readonly CompositeDisposable disposables = new();

    public GamePlayPresenter(IGamePlayViewModel vm, GamePlayView view)
    {
        this.vm = vm;
        this.view = view;
    }

    public void Enable()
    {
        disposables.Clear();
        vm.TurnRP.Subscribe(OnTurnNumberChanged).AddTo(disposables);
        vm.Selected.Subscribe(OnSelected).AddTo(disposables);
        vm.SelectFailed.Subscribe(OnSelectFailed).AddTo(disposables);
        view.Show();
    }

    public void Disable() 
    {
        view.Close();
        disposables.Clear();
    }
}
```
