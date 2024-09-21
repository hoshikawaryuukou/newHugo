---
title: "Unity - Package - xLua"
date: 2023-05-28 21:11:00
draft: false

tags: ["Unity"]
---

本次操作 xLua 主要是做熱更方案的評估測試，筆者目前還是偏好使用 HybridCLR。

## Official
- [Tencent/xLua](https://github.com/Tencent/xLua)

## 評估
- 使用 lua
- 仍是目前主流/穩定做法 (畢竟也行之有年了)。
- 邏輯操作可能要移師到 lua 側。
- 缺少 ide 支援如果要在 lua 側 進行 unity 相關操作時，維護/除錯成本極高。

## Example

在 lua 側進行 unity 相關操作

```lua
local speed = 10
local lightCpnt = nil

function start()
	print("lua start...")
	print("injected object", lightObject)
	lightCpnt= lightObject:GetComponent(typeof(CS.UnityEngine.Light))
end

function update()
	local r = CS.UnityEngine.Vector3.up * CS.UnityEngine.Time.deltaTime * speed
	self.transform:Rotate(r)
	lightCpnt.color = CS.UnityEngine.Color(CS.UnityEngine.Mathf.Sin(CS.UnityEngine.Time.time) / 2 + 0.5, 0, 0, 1)
end

function ondestroy()
    print("lua destroy")
end
```