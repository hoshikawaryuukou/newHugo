---
title: "Telegarm - Note"
date: 2024-06-22 21:11:00
draft: false

tags: ["Telegarm"]
---

## Bot - API Token
- 搜索 `BotFather` 並開始對話。
- 使用 `/newbot` 命令創建一個新的機器人，按提示操作。
- 創建完成後，你會獲得一個 API Token，將其保存下來。

## Bot - Chat ID
- 將你創建的**機器人添加到你想發訊息的群組**中。
- 發送一條消息到該群組。
- 使用以下 URL 來獲取群組的更新:
    ```bash
    https://api.telegram.org/bot<YourBotToken>/getUpdates
    ```
- 查看返回的 JSON 數據，找到 chat 字段中的 id，這就是群組的 Chat ID。
    ```json
    {
        "ok": true,
        "result": [
            {
                "update_id": 123456789,
                "message": {
                    "message_id": 1,
                    "from": {},
                    "chat": {
                        "id": -1001234567890,
                        "title": "Your Group Title",
                        "type": "supergroup"
                    },
                    "date": 1617821123,
                    "text": "Your Message"
                }
            }
        ]
    }
    ```

## Sticker
- [Telegram 貼圖 DIY教學](https://www.youtube.com/watch?v=1E25Q6wQ5L8)
