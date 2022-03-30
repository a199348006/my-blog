---
title: "HTTP Status Code"
date: 2022-03-25T15:04:04+08:00
draft: false
tags: ["Undefined"]
categories: ["Undefined"]
description: "記錄些較常使用的HTTP狀態碼。"
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

> 記錄會較常使用的狀態碼，詳細可以下拉至[參考來源](#參考來源)。

## 2XX成功

- 200 OK - 在GET請求中，回應將包含與請求的資源相對應的實體。在POST請求中，回應將包含描述或操作結果的實體。
- 201 Created
- 204 No Content - 伺服器成功處理了請求，沒有返回任何內容。

## 3XX重新導向

- 304 Not Modified - 表示資源在由請求頭中的If-Modified-Since或If-None-Match參數指定的這一版本之後，未曾被修改。

## 4XX客戶端錯誤

- 400 Bad Request
- 401 Unauthorized - 未提供或無效的身份驗證Token時
- 403 Forbidden - 身份驗證成功但無權訪問資源
- 404 Not Found
- 405 Method Not Allowed - 當請求的HTTP方法不允許經過身份驗證的用戶時
- 415 Unsupported Media Type - 如果作為請求的一部分提供了錯誤的內容類型
- 422 Unprocessable Entity - 用於欄位資料驗證錯誤
- 429 Too Many Requests

## 5XX伺服器錯誤

- 500 Internal Server Error - 伺服器端程式有誤，需要工程師修復

## 參考來源

[維基百科](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)

[iT邦幫忙](https://ithelp.ithome.com.tw/articles/10224134)
