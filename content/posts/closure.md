---
title: "Closure 閉包"
date: 2022-05-03T15:58:45+08:00
draft: false
tags: ["Javascript"]
categories: ["Undefined"]
description: "記錄閉包相關，例：Currying, Revealing Module Pattern."
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

## 典型的Closure

> 內部(Inner)函式被回傳後，除了自己本身的程式碼外，也會捕抓到了環境的變數值，記住了執行當時的環境。

```javascript
const varGlobal = 'x';

function outer (paramOuter) {
  const varOuter ='y';

  function inner (paramInner) {
    const varInner ='z';
    console.log(varGlobal);
    console.log(varOuter);
    console.log(varInner);
    console.log(paramOuter);
    console.log(paramInner);
  }
  return inner;
}

const func = outer('a');
func('b');

// x
// y
// z
// a
// b
```

## 柯里化(Currying)

```javascript
// 原本
function add(x, y z) {
  return x + y + z;
}

// 柯里化
function add(x, y, z) {
  return function (y) {
    return function (z) {
      return x + y + z;
    }
  }
}

add(2)(3)(4); // 9
```

## IIFE(立即呼叫函式表達式)

常見的寫法：

```javascript
(function () { /* code */ }())

(function () { /* code */ })()
```

### 模組(Module)樣式

暴露的模組樣式(Revealing Module Pattern)

```javascript
let Module = (function () {
  let privateFunc = function () {
    console.log('It is privateFunc.');
  }

  let publicFunc1 = function () {
    console.log('Public 1');
  }

  let publicFunc2 =  function () {
    console.log('Public 2');
    privateFunc();
  }

  return {
    publicFunc1: publicFunc1,
    publicFunc2: publicFunc2
  }
})()
```

## 參考來源

[從ES6開始的JavaScript學習生活-Closure](https://eyesofkids.gitbooks.io/javascript-start-from-es6/content/part4/closure.html)
