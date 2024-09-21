---
title: "AI - Ollama"
date: 2024-08-19 21:11:00
draft: false

tags: ["AI"]
---

## Guide
- [Ollama](https://ollama.com/)
- [Ngrok + Ollama | 在世界任何地方与localhost开源大模型聊天](https://www.youtube.com/watch?v=JfI3K3HwQuI)
- [Free Inference Is All I Need: How to Run Large Language Models for Free Using Google Colab](https://blog.gopenai.com/free-inference-is-all-i-need-how-to-run-large-language-models-for-free-using-google-colab-fe961e86503b)

## UI
- [Page Assist - A Web UI for Local AI Models](https://chromewebstore.google.com/detail/page-assist-a-web-ui-for/jfgfiigpkhlkbnfnbobbkinehhfdhndo)

## Model
- [Hugging Face](https://huggingface.co/)
- [qwen2](https://ollama.com/library/qwen2)
- [internlm2](https://ollama.com/library/internlm2)
- [mradermacher/mini-magnum-12b-v1.1-GGUF](https://hf-mirror.com/mradermacher/mini-magnum-12b-v1.1-GGUF)
- [Roleplay, Creative Writing, Uncensored, NSFW](https://huggingface.co/collections/DavidAU/roleplay-creative-writing-uncensored-nsfw-66163c580c61496c340afe32)

## Commands
- ollama list : 查看以配置本地模型
- ollama run {model} : 下載/執行模型

## Extra

### import_gguf_to_ollama.bat
```bat

@echo off

REM 設定本地環境，並切換到批次檔所在的目錄
setlocal
cd /d %~dp0

REM 搜尋當前目錄中的 .gguf 檔案
for %%f in (*.gguf) do (
    REM 創建 Modelfile.txt 並寫入模型檔案名稱
    echo FROM %%~nf.gguf > Modelfile.txt
    
    REM 打印 Modelfile.txt 的內容以供確認
    type Modelfile.txt
    
    REM 執行 ollama create 命令來包裝模型檔
    ollama create %%~nf -f Modelfile.txt
    
    REM 刪除 Modelfile.txt
    del Modelfile.txt
    
    REM 如果有多個 gguf 檔案，只處理第一個找到的檔案
    goto end
)

:end
REM 顯示完成訊息
echo done...

REM 列出已經存在的模型
ollama list 

REM 等待用戶確認並關閉
pause >nul

```
