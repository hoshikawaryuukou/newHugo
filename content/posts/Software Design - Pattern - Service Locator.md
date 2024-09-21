---
title: "Software Design - Pattern - Service Locator"
date: 2023-06-28 20:05:00
draft: false

tags: ["Software Design", "Pattern"]
---

## 前述

Service Locator 確實也是 IoC 的一種實作方式，不過採用的是 依賴尋找(Dependency Lookup) 的設計。
筆者之前有一陣子蠻常使用這 pattern，那時對 DI 與 IoC 的概念並不熟悉，只覺得這樣使用依賴變得很方便。

因為我可以在任何地方直接這樣取用資源
```csharp
var target = ServiceLocator.Resovle<Target>();
```

這樣的寫法有以下問題 :
1. 透過 ServiceLocator 因為這個取用資源的過程是隱性的，不容易被直接發現。
2. 想用誰就拿誰這件事也有點危險，Ex: View 可以拿到不屬於 Presentation layer 該碰的對象。

所以當 DI 與 IoC 的概念熟悉後，並且使用 DI / IoC Container 後就漸漸不使用這 pattern 了。

## 應用

但這次工作上反而覺得 Service Locator 可以勝任從 Singleton 過渡到  DI / IoC Container 的中繼階段。

因為這次接觸到的專案嚴重依賴 Singleton，且組員也已習慣 Singleton 的寫法了，要直切換到  DI / IoC Container 會有不小的陣痛期(當然實務上能不能切又是另一個故事了)。

於是筆者想起了 Service Locator，有以下理由
1. 因為在使用上就很像是 Singleton
2. 筆者希望組員能快速感受到 IoC 所帶來的紅利
3. 集中管理依賴

## 實作

此模式使用稱為「服務定位器」的中央註冊表，它根據請求返回執行特定任務所需的對象。

以下是一種變體實作
- 註冊的對象不強制要實作介面
- 基本上只當是個容器
- 因為不使用反射，需要搭配一個 Installer (組合根)

```csharp
// 這裡透過 static 來達到全域使用
public class ServiceLocator
{
    private static readonly Dictionary<Type, object> instances = new Dictionary<Type, object>();

    public static void Register<T>(T instance)
    {
        instances[typeof(T)] = instance;
    }

    public static T Resolve<T>()
    {
        if (instances.TryGetValue(typeof(T), out var instance))
        {
            return (T)instance;
        }

        throw new Exception($"Service of type {typeof(T)} is not registered.");
    }

    public static void Release<T>()
    {
        if (instances.ContainsKey(typeof(T)))
        {
            instances.Remove(typeof(T));
        }
    }
}
```

```csharp
// 由 Installer 來對容器註冊對象
public class DemoBasicServiceLocatorsInstaller : MonoBehaviour
{
    public DemoBasicMoneyUI moneyUI;

    public MoneyType moneyType;
    public int moneyValue = 100;

    void Start()
    {
        switch (moneyType)
        {
            case MoneyType.Real: ServiceLocator.Register<IMoneyFormatConverter>(new RealMoneyFormatConverter()); break;
            case MoneyType.Coin: ServiceLocator.Register<IMoneyFormatConverter>(new CoinMoneyFormatConverter()); break;
            default: throw new System.NotImplementedException();
        }

        moneyUI.Show(moneyValue);
    }
}
```

```csharp
// 並在需要的地方跟容器取用
public class DemoBasicMoneyUI : MonoBehaviour
{
    [SerializeField] private TMP_Text text;

    private IMoneyFormatConverter moneyFormatConverter;

    public void Show(int moneyValue)
    {
        moneyFormatConverter ??= ServiceLocator.Resolve<IMoneyFormatConverter>();
        text.text = moneyFormatConverter.Convert(moneyValue);
    }
}
```
