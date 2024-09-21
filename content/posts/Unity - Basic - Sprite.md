---
title: "Unity - Basic - Sprite and Atlas"
date: 2023-02-20 21:11:00
draft: false

tags: ["Unity"]
---

## Sprite
- [【2Dゲームで必須】UnityのSprite（スプライト）の単位をわかりやすく解説](https://shibuya24.info/entry/unity-unit)
- [【間違えやすい】Unityの正しい画像サイズとは](https://shibuya24.info/entry/unity-ui-texture-size)

## Atlas
- [【Unity】SpriteをパックするSpriteAtlasの使い方](https://shibuya24.info/entry/unity-spriteatlas)

### 目的
- 減少DrawCall
- 圖集將圖片打包為2的冪次方的素材大小，可以提升性能
- 減小包體大小

### 注意
- Sprite Atlas V1 - Always Enabled 啟用圖集時
  - Edit Mode : reference the packed Textures
  - Play Mode : reference the original unpacked Textures
- SpriteAtlas AssetBundle 來打包時，**不要勾選** Include In Build