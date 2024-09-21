---
title: "Unity - Editor - ScriptedImporter"
date: 2023-05-27 21:11:00
draft: false

tags: ["Unity"]
---

## 用途
- 使用C# 為Unity 本身不支持的文件格式編寫自定義資源導入器，從而添加支持。

## 注意
- Scripted Importer 無法處理已由 Unity 本身處理的文件擴展名。

## Example

這裡將 .lua 以 TextAsset 

```csharp
using UnityEngine;
using System.IO;
using UnityEditor.AssetImporters;

[ScriptedImporter( 1, "lua" )]
public class LuaImporter : ScriptedImporter 
{
    public override void OnImportAsset( AssetImportContext ctx ) 
    {
        TextAsset subAsset = new TextAsset( File.ReadAllText( ctx.assetPath ) );
        ctx.AddObjectToAsset( "text", subAsset );
        ctx.SetMainObject( subAsset );
    }
}
```

## Ref
- [Scripted Importers](https://docs.unity3d.com/Manual/ScriptedImporters.html)
- [[Unity] 资源工作流程 - ScriptedImporter](https://www.cnblogs.com/wildmelon/p/16087056.html)