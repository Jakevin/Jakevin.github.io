---
layout: post
title:  "GPT-browsing 功能測試"
date:   2023-05-18 08:42:00 +0800
categories: chatgpt
---

## GPT-browsing 

[實驗網址1](https://jakevin.github.io/azure-tts/gpt-browser-test/first.html)

[實驗網址2](https://jakevin.github.io/azure-tts/gpt-browser-test/second.html)

[實驗網址3](https://jakevin.github.io/azure-tts/gpt-browser-test/third.html)

[實驗網址4](https://jakevin.github.io/azure-tts/gpt-browser-test/fourth.html)

[實驗網址5](https://warnermusictwtw.kktix.cc/events/b8994dc3)


## 實驗1

純靜態網頁，早期沒有Browsing功能的時使，GPT會抓頁面的meta來分析，多了Browsing功能後有什麼差別呢？

<img src="/assets/img/gpt-browsing-01.png" width="60%">

wow! 太好了，meta的內容都pass掉，正確的了解到網頁的內容了

## 實驗2

用vue3 寫了一個很簡單應用，僅僅是頁面在loading完後，把title跟content補上

```
const { createApp, reactive, onMounted } = Vue
const app = createApp({
    setup() {
        const state = reactive({
            title:"",
            content:``
        })
        onMounted(() => {
            console.log('onMounted')
            state.title = "銀座"
            state.content = `東京`
        
        });
        
        return {
            state,
        };
    }
}).mount("#app");
```

<img src="/assets/img/gpt-browsing-02.png" width="60%">

結果發現，Browsing完全讀不到寫在整onMounted下的資料


## 實驗3

我們使用 onMounted了，直接在Vue啟動時就把資料安上

```
const { createApp, reactive } = Vue
const app = createApp({
    setup() {
        const state = reactive({
            title:"銀座",
            content:`東京`
        })
        
        return {
            state,
        };
    }
}).mount("#app");
```

<img src="/assets/img/gpt-browsing-03.png" width="60%">

結果發現，Browsing還是看不出網站內容

## 實驗4

我們使用原生的Javascript來做處理，直接在 script標籤下執行塞值的事

```
<body>
    <noscript>
      <p>此網頁需要支援 JavaScript 才能正確運行，請先至你的瀏覽器設定中開啟 JavaScript。</p>
    </noscript>

    <div id="app">
        <h1 id="title"></h1>
        <h6 id="content"></h6>
    </div>

    <script>
      document.getElementById("title").innerHTML = '鋒面接近愈晚雨愈大 西半部及宜蘭明天防局部大雨';
      document.getElementById("content").innerHTML = '中央氣象局今天表示，晚間起鋒面接近，愈晚雨愈大，西半部及宜蘭明天可能會有局部大雨；下一波鋒面預估22日起接力影響。另外，在關島一帶有熱帶系統正在醞釀，周末可能增強為熱帶性低氣壓。';
    </script>
  </body>
```

<img src="/assets/img/gpt-browsing-04.png" width="60%">

結果發現，Browsing還是看不出網站內容

## 實驗5

讓Browsing抓看看 SSR（server side rendering ）的網頁

<img src="/assets/img/gpt-browsing-05.png" width="60%">

是可以順利抓取到網站內容

## 結論

Browsing 似乎是用 python的爬蟲在抓資料，需要動態loading，或是互動方式取得的資料是無法理解的。

再來，如果是透過 server side rendering 的頁面，就有可能被 Browsing找到

其實理論上就是 SEO的做法，讓SEO的爬蟲能找你內容的話，Browsing也可以理解你網站的內容

另外，要快速知道 Browsing能不能理解網站的方法，在網頁上按右鍵，選檢視網頁原始碼，會另開一網視窗

這個視窗的內容就是Browsing看到的內容。

<img src="/assets/img/gpt-browsing-06.png" width="60%">
