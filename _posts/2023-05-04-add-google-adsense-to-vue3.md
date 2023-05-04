---
layout: post
title:  "如何在Vue3中加入google adsense"
date:   2023-05-04 08:42:00 +0800
categories: vue
---


## 前言

Google Ads給的廣告代碼是無法直接使用在Vue上的，你會看到下面這樣的程式碼，Vue的Template裡不支援script的tag

```
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-xxxxxxxxx"
     crossorigin="anonymous"></script>
<ins class="adsbygoogle"
     style="display:block"
     data-ad-format="fluid"
     data-ad-layout-key="-fb+5w+4e-db+86"
     data-ad-client="ca-pub-xxxxxxxx"
     data-ad-slot="xxxxxxx"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>

```

## 做法

### 第一步

在index.html的head下，加上下面code，記得把xxxxx換成你自己的代號

```
<head>
    ...省略
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-xxxxxxxxxx" crossorigin="anonymous"></script>
    ...省略
</head>

```

### 第二步

在index.html的body下，加上下面code

```
<body>
    <script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-xxxxxxxxx"crossorigin="anonymous"></script>
    <script>
      window['addAds'] = function(){
          const cardList = document.getElementsByClassName('gads');
          for(let i=0 ; i<cardList.length ; i++){
              (adsbygoogle = window.adsbygoogle || []).push({});
          }
      }
    </script>
    ...省略
```

### 第三步

在Vue中想要加上廣告的components，加上div並用v-html把 ins加上

```
<template>
    <div v-html="ads1">
</template>
```

在script裡加上v-html的內容

```
<script>
const ads1 = `
<ins class="adsbygoogle"
    style="display:block"
    data-ad-client="ca-pub-xxxxxxxx"
    data-ad-slot="xxxxxxxx"
    data-ad-format="auto"
    data-full-width-responsive="true"></ins>`

</script>
```

### 第四步

在Vue的Component的onMounted加上一行code

```
<script>
onMounted(() => {
    window.addAds()
})
</script>

```

完成！
