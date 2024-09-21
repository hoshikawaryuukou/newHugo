---
title: "Software Design - Pattern - Model View Presenter (MVP)"
date: 2022-12-10 20:05:00
draft: false

tags: ["Software Design", "Pattern"]
---

## 前述

關注點分離（Separation of Concerns，SoC）: 在軟體開發中，一個模組或組件應該專注於解決特定的問題，而不是同時處理多個功能。每個組件都有自己的職責範圍，並且與其他組件盡可能解耦合。

而 MVC / MVP / MVVM 是關注點分離於前端的經典應用，網上已經有很多不錯的文章，再寫一份類似的整理文章意義也不大，對此感到陌生，不妨閱讀以下連結，會幫助你理解 MV系列的發展。

- [界面之下：还原真实的MV*模式](https://github.com/livoras/blog/issues/11)
- [正确认识 MVC/MVP/MVVM](https://juejin.cn/post/6901200799242649607)
- [站在思想层面看MVX架构](https://juejin.cn/post/6998093259893407757#comment)
- [MVP Pattern: Part 2 Supervising Controller](https://deltatimer.com/260/mvp-pattern-part-2-supervising-controller)
- [Part 2 — Converting Presenters into ViewModels](https://proandroiddev.com/converting-presenters-into-viewmodels-c9279c7516e7)
- [【Unity】MV(R)Pパターンのすすめ](https://annulusgames-lab.blogspot.com/2022/12/unity-ui-mvrp.html)

以下則對筆者實作中比較常用的 MVP 多做一些討論

## 關注點(責任)
在 MVP 的構成下分成三個部分
- Model: 應用程式的核心邏輯。
- View: 應用程式的使用者介面，負責呈現數據和接收使用者的輸入。
- Presenter:  View 和 Model 之間的中介。

### Passive View
這是 MVP 的一種實作風格，也是筆者主要使用的風格。
- Presenter 對 View 有完全控制權
- View 提供方法與事件給 Presenter 使用
- View 對 Presenter 一無所知

以猜拳遊戲的 View 為例
```csharp
public class View : MonoBehaviour
{
    [SerializeField] private Text messageText;
    [SerializeField] private Button[] playerChoices;
    [SerializeField] private Button nextButton;

    private readonly Subject<Choice> playerChoiceSelected = new Subject<Choice>();
    private readonly CompositeDisposable disposables = new CompositeDisposable();

    public IObservable<Choice> PlayerChoiceSelected => playerChoiceSelected;
    public IObservable<Unit> PlayerNextRequested => nextButton.onClick.AsObservable();

    void Awake()
    {
        disposables.Clear();
        playerChoices[0].onClick.AsObservable().Subscribe(_ => SelecteChoice(Choice.Rock)).AddTo(disposables);
        playerChoices[1].onClick.AsObservable().Subscribe(_ => SelecteChoice(Choice.Paper)).AddTo(disposables);
        playerChoices[2].onClick.AsObservable().Subscribe(_ => SelecteChoice(Choice.Scissors)).AddTo(disposables);
    }

    void OnDestroy()
    {
        disposables.Clear();
    }

    public void SetReady(string message)
    {
        messageText.text = message;
        nextButton.gameObject.SetActive(false);
    }

    public void SetResult(string message)
    {
        messageText.text = message;
        nextButton.gameObject.SetActive(true);
    }

    private void SelecteChoice(Choice choice)
    {
        playerChoiceSelected.OnNext(choice);
    }
}
```

## 依賴關係

依據不同的情境有兩種依賴關係

![MVP](/images/MVP.png)

(左) 定義 IView 介面
1. 著重在保持 Presenter 的控制邏輯
2. Presenter 依賴於 IView 介面
3. 主要應用於有換皮需求的 View


(右) 直接使用 View
1. 著重在保持 View 的獨立性(可能有跨專案需求)
2. Presenter 直接依賴 View
3. Presenter 基本與 View 綁定
