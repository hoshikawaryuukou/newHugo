---
title: "Software Design - Pattern - State"
date: 2024-06-27 21:05:00
draft: true

tags: ["Software Design", "Pattern"]
---

- [State · Design Patterns Revisited · Game Programming Patterns](https://gameprogrammingpatterns.com/state.html)




每次我們接觸這部分程式碼時，我們都會破壞一些東西。

複雜分支和可變狀態（隨時間變化的欄位）是兩種容易出錯的程式碼，

總而言之，要添加這種衝鋒攻擊，我們必須修改兩個方法並添加一個 chargeTime_字段，Heroine儘管它僅在閃避狀態下才有意義。
我們希望將所有程式碼和資料很好地封裝在一個地方。四人幫已經為我們提供了保障。




```ts
// scope1
{
    let state1;
    // do something...

    // scope2
    {
        let state2;
        // do something...

        // scope3
        {
            let state3;
            // do something...

            // scope4
            {
                let state4;
                // do something...
            }
        }
    }
}
```

argument drilling
```js
function outerFunction(param) {
    innerFunction(param);
}

function innerFunction(param) {
    console.log(param);
}
```

“Argument drilling” 是一種程式設計中的現象，當一個參數需要被傳遞到多層函數或組件中時，即使某些函數或組件並不直接使用該參數，也需要將其作為參數傳遞下去。這種現象在 React 等組件化的程式設計語言中尤其常見，並且被認為是一種 “bad smell”。

解決 “argument drilling” 的一種方法是使用上下文（Context）或者狀態管理工具（如 Redux、MobX 等）來共享狀態，這樣就可以避免將參數一層一層地傳遞下去1。

另一種方法是重構你的程式碼，讓每個函數只接收和處理它真正需要的參數。這樣可以提高程式碼的可讀性和可維護性，並降低出錯的可能性1。

在 React中的 "prop drilling"
- [Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)


```ts
type User = {
  name: string;
  age: number;
};

function func00(user: User) {
  // do something... 沒有對 user 操作
  func01(user);
}

function func01(user: User) {
  // do something... 沒有對 user 操作
  func02(user);
}

function func02(user: User) {
  console.log(`Hello, ${user.name}`);
}


func00({ name: 'Alice', age: 25 });
```

## Other
- [State Machine and Event Bus in Flash Game Development](https://ingramchen.io/blog/2011/04/state-machine-and-event-bus-in-flash-game-development.html)
- [React Hooks —— 状态管理篇](https://juejin.cn/post/7170521701162156046)
- [Prop Drilling vs. State Lifting in React: Optimizing Data Flow](https://www.linkedin.com/pulse/prop-drilling-vs-state-lifting-react-optimizing-data-flow-thakur-y8qie/)
