---
title: "Indie Project - AnimalConnect"
date: 2023-02-20 21:11:00
draft: true

tags: ["Unity"]
---

# AnimalConnect

## TsumTsum (ツムツム) Type Game 事前調查

### Store
- [LINE: Disney Tsum Tsum](https://play.google.com/store/apps/details?id=com.linecorp.LGTMTMG&hl=zh_TW)
- [あにぷら　～かわいいどうぶつのツムツム風パズルゲーム～](https://play.google.com/store/apps/details?id=com.masanoh.AnimalPlanet)

### Online (廣告很多)
- [Merge Pumpkin](https://game16.net/burage/puzzlegame/merge-pumpkin/)
- [Magic Pom](https://game16.net/burage/puzzlegame/magic-pom/)

### 體驗
- 連線目標種類不能太多，體感 5 種是極限，再多死局機率高
- 需要有解死局的機制(風扇之類)

### Repo
- [qinyeli/TsumTsum](https://github.com/qinyeli/TsumTsum)
- [Tsunehiko511/TsumuTsumuYouTube](https://github.com/Tsunehiko511/TsumuTsumuYouTube)

### 
- [つむつむ【作り方】](https://www.youtube.com/playlist?list=PLEkX-p0oUs8ybA9iLRzchUJ0UsdJS853Y)



- google ツムツム 似たゲーム
- [妖怪ウォッチ ぷにぷに](https://play.google.com/store/apps/details?id=com.Level5.YWP&hl=en_US)
- [ツムツム似！？無料パズルゲーム「プクプク」攻略まとめ！毎日遊んでお小遣い稼ぎ](https://motokase.com/pukupuku-matome/)
- [マーベル ツムツムに似たゲーム、類似アプリ一覧](https://gameappch.com/app/alike.html?app=02843)
- [SUMI SUMI PARTY : Tap Puzzle](https://play.google.com/store/apps/details?id=jp.co.imagineer.sumikkogurashi.sumisumi2)


## 基本元素
- Ball: 主要互動目標

## 核心玩法
- Ball 受重力影響會往下移動
- Ball 彼此之間有碰撞推擠
- 將 Ball 連接在一起當達到一定數量(一般是三個以上)可以消除，並掉落新的
- 連接的方式有兩種
  - 手動: 玩家以拖曳方式滑過目標，自行決定要連結那些
  - 自動: 玩家以點擊的一個目標，系統會判定可連結對象
- 連接的判定有兩種
  - 相鄰: 使用 距離 (多為統一形狀使用)
  - 接觸: 使用 接觸 (多為不規則形狀使用)
- 連接後有兩種
  - 消失
  - 合併

## 機制
- Timer: 產生時間壓力，影響判斷力
- Bomb: 消除目標周圍的 Ball
- Fever: 在一定的時間內可以得到更多分數
- Ice: 冰塊包住 Ball， Ball 不能被連線

## 互動
- Bomb 炸冰塊，冰塊會消失，Ball留下

## 技能
- Fan: 擾動所有可被吹動的物件
- Uniformize: 隨機同化一個 Ball 周圍的 Balls



## Ball
- 讓玩家互動的媒介
- 可互動? 不可互動?
- 呈現 type 以達到分類的作用



## Chain
- 處理 "規則" 所取得的 Balls 

## Bomb
- 只是一個位置訊號源

## Ice
- 是 Ball Status

## Big
- 是 Ball Status




## GenerateFlow
- 總共生成 5種 type 共 50 個球
- 其中有 3 個球是 冰凍 狀態

## HandleLink
- 相同的 type 可以連線，但被冰凍的則不行

## HandleChain
- 將連線的的球放回池中

## HandleBomb
- 將炸彈周圍的球放回池中，但被冰凍的只會將冰消失


  