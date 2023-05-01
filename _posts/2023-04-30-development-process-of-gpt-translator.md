---
layout: post
title:  "開發過程與更新記錄"
date:   2023-04-30 07:42:00 +0800
categories: chatgpt
---


## 更新記錄

05-01 修正發音無法正常播放問題

04-29 修正對方發音無法正常翻譯

04-28 修正歷史記錄點選後，不能再做新的翻譯

04-27 因為日文的翻譯有部分user異常，修正prompt

04-26 加上Menu功能，放上使用說明

04-25 歷史記錄列表修正，最新的放上面

04-24 歐洲語系全部加上、阿語、土耳其語加上

## 開發過程

翻譯器：OpenAI的 gpt-3.5

語音識別系統：OpenAI的 whisper

發音功能：Azure的 TTS系統


前端框架：Vue3 

UI套件：element-ui-plus

``` json
 "dependencies": {
    "@element-plus/icons-vue": "^2.1.0",
    "element-plus": "^2.3.2",
    "vue": "^3.2.47"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^4.1.0",
    "unplugin-auto-import": "^0.15.2",
    "unplugin-vue-components": "^0.24.1",
    "vite": "^4.2.0"
  }
```


