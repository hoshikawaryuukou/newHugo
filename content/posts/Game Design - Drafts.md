---
title: "Game Design - Drafts"
date: 2022-11-06 20:05:00
draft: true

tags: ["Drafts"]
---


《饥荒》使用lua作为其脚本语言，得益于lua动态类型脚本语言的特性，因此很容易实现基于组件的开发，因此我们发现除去一些AI因为逻辑相对复杂的原因而采用了状态机和行为树，以及一些通用的或者框架类的脚本，其他脚本都被抽象为component
《饥荒》中引入一个prefab 脚本 的概念，在这个脚本中完成一个 gameobject的“组装”，这个过程包括资源文件和逻辑组件。

从关注一个游戏对象是什么，变为关注一个游戏对象能做什么？
以游戏内道具为例，我们不在给道具下定义为装备、消耗品、材料或任务道具这些。
而是赋予道具能力：可装备的、可饮用的、可作为合成材料的。然后再针对每一种能力编写具体的功能逻辑。



遊戲性是指控制風險並獲得回報的樂趣
攻略是指控制風險並獲得回報的方法
Game Essence = The fun of managing risks/getting rewards 
Strategy = How you manage risks/get rewards

## Core
- 游戏设计的236个技巧 游戏机制 关卡设计和镜头窍门

## 場景
- 游戏场景设计 专业技法解析

## 設計
- 將核心設計成純函數(Pure Function)，Pure Function 具有同輸入同輸出的特性，這樣他擁有高可預測性
- 以純功能的方式製作核心遊戲邏輯

### 構建軟件
我希望達到什麼目的？ 願景
創建一個服務總線，以促進創建高度解耦（時間、平台和實施）的業務服務，這些服務可以水平擴展且具有高度彈性地故障。

動機是什麼？
想了解更多關於構建分佈式系統和中間件的信息
想提高我的 scala 和 akka 技能
需要一個類似於 NServiceBus 的服務總線，適用於 linux 和任何語言，用於我未來的項目

系統應該具備哪些特徵？
高度容錯——一旦捕獲到業務意圖，就永遠不會丟失。例如至少一次消息傳遞
啟用水平可擴展性（盡可能多）
易於監控（系統性能、錯誤）
主要在linux上運行
可用於任何編程語言

待辦事項列表和問題列表

我盡量減少腦力勞動
在項目的這個階段，我很清楚自己想要構建什麼以及為什麼要構建它。
這些原因都被寫下來，以便我在項目過程中清楚地理解——而不是作為感覺保存在記憶中，然後每次我想到它們時通過我當前的情緒狀態重新解釋。

精神清零
即使我有一個願景和功能列表，我還是不願意坐下來開始編碼——太多的未知數。
根據經驗，我知道在這種狀態下編碼會使我的大腦分散和大量不穩定的黑客攻擊。
相反，我想要一個理論上合理的設計來指導我。

從圖表中即時回報

多幾張圖，頭腦更清晰

幫助吸引人們加入


------------------
-[《鈴蘭之劍：為這和平的世界》釋出開發團隊的一封信 分享設計理念與研發方向](https://gnn.gamer.com.tw/detail.php?sn=241688)

## Case
- [《OPUS: 龍脈常歌》遊戲開發精華 — 關卡設計](https://medium.com/@sigono/opus-%E9%BE%8D%E8%84%88%E5%B8%B8%E6%AD%8C-%E9%81%8A%E6%88%B2%E9%96%8B%E7%99%BC-%E9%97%9C%E5%8D%A1%E8%A8%AD%E8%A8%88-8ab0291d209e)

## OO
* [Matching games Memory games Pairs: Remembery](https://play.google.com/store/apps/details?id=ua.krou.remembery)
* [鬥技場的阿利娜](https://store.steampowered.com/app/1668690/_/?l=tchinese)
* [Webbed](https://store.steampowered.com/app/1390350/Webbed/)

- 發行商:這能有多少受眾？ 
- Steam頁面蒐集願望清單以及頁面拜訪數據
- 由於小團隊資金沒有到太過充裕，遊戲在視覺方面選擇用比較簡單的畫面呈現。所有設計決策重點都放在避免玩家與遊戲間的摩擦，以提供流暢的體驗。

## 技能
- [探讨服务端回合制战斗系统](https://wudaijun.com/2017/09/ngs-battle/#valine-comments)
- [一种易扩展游戏技能系统的实现方案](https://www.shymean.com/article/%E4%B8%80%E7%A7%8D%E6%98%93%E6%89%A9%E5%B1%95%E6%B8%B8%E6%88%8F%E6%8A%80%E8%83%BD%E7%B3%BB%E7%BB%9F%E7%9A%84%E5%AE%9E%E7%8E%B0%E6%96%B9%E6%A1%88)
- [如何设计技能系统](http://www.liuocean.com/2023/01/07/ru-he-she-ji-ji-neng-xi-tong/)

## Framework
- [MonoGame](https://www.monogame.net/)
- [games 104](https://games104.boomingtech.com/tc/course-list/)


### 參考
- [Unity多人联机网络游戏开发都存在哪些误区？](https://www.zhihu.com/question/512125478)
- [游戏服务器与普通服务器有什么区别?](https://www.zhihu.com/question/23508968)
- [网游服务器逻辑和传输如何分层/解耦？](https://www.zhihu.com/question/512121738/answer/2347895513)
- [How do multiplayer games sync their state? Part 1](https://medium.com/@qingweilim/how-do-multiplayer-games-sync-their-state-part-1-ab72d6a54043)