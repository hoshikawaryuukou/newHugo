---
title: "Android - Reverse Engineering"
date: 2024-08-30 13:11:00
draft: false

tags: ["Android"]
---

## apktool
- [APKTool反编译](https://www.cnblogs.com/hanyuanhun/p/18266371)

### extract.bat
⚠️ 將 **extract.bat**, **apktool.jar**, **apk** 放在相同目錄。

```bat
@echo off
REM Set the directory where apktool.jar is located
set APKTOOL_DIR=%~dp0

REM Enable delayed variable expansion
setlocal enabledelayedexpansion

REM Loop through all APK files in the same directory as apktool.jar
for %%f in ("%APKTOOL_DIR%*.apk") do (
    REM Get the APK file name (without extension)
    set APK_NAME=%%~nf
    echo Decompiling APK: !APK_NAME!

    REM Decompile the APK
    java -jar "%APKTOOL_DIR%apktool.jar" d "%%f" -o "%APKTOOL_DIR%!APK_NAME!"
)

echo All APK files have been decompiled!
pause
```
