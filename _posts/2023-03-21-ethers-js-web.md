---
layout: post
title:  "用Ethers.js，前端錢包綁定實作"
date:   2023-03-21 22:38:00 +0900
categories: eth
---

因公司專案開發的需求，一邊學習、一邊筆記
過程相當單純，使用 ethers.js，所有的前端框架都可使用

## 安裝 Ethers.js

套件的官網 [https://www.npmjs.com/package/ethers](https://www.npmjs.com/package/ethers)

中文說明 [https://learnblockchain.cn/ethers_v5/](https://learnblockchain.cn/ethers_v5/)

英文說明 [https://docs.ethers.org/v5/](https://docs.ethers.org/v5/)

```
npm install ethers
```

## 引用
``` js
//node 
const { ethers } = require("ethers");

//ES6 or TypeScript
import { ethers } from "ethers";
```

## 檢查錢包是否存在
整個流程的第一步，檢查錢包系統是否存在，如果不存在的話後面流程也不用走了

``` js
async function connect() {
    try {
        const { ethereum } = window;
        if (!ethereum) {
            console.log("setError", "Metamask not installed!");
            return;
        }
    } catch (error) {
        console.log(error);
    }
}
```

## 綁定錢包
最重要的流程，會打開錢包App，尋求認證

``` js
  async function requestAccess() {
      const { ethereum } = window;
      const accounts = await ethereum.request({
          method: "eth_requestAccounts",
      });
      console.log("setAccount", accounts[0]);
  }
```

## 檢查是否已經綁定錢包
錢包是否提供頁面存取的權限

``` js
  async function checkIfConnected() {
      const { ethereum } = window;
      const accounts = await ethereum.request({ method: "eth_accounts" });
      if (accounts.length !== 0) {
          console.log("setAccount", accounts[0]);
          return true;
      } else {
          return false;
      }
  }
```

## 取得簽名
拿到錢包的Address

``` js
  async function getSigner() {
    try {
        const { ethereum } = window;
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signer = provider.getSigner();
        const selfAddress = await signer.getAddress()
        console.log("selfAddress",selfAddress)
        return selfAddress
    } catch (error) {
        console.log(error);
        return null;
    }
  }
```