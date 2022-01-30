---
title: "使用Hugo部署至GitHub"
date: 2022-01-30T11:49:15+08:00
draft: false
tags: ["hugo", "github"]
categories: ["undefined"]
description: "使用Hugo套用主題部署至GitHub Pages，以及自動化部署GitHub Actions"
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

> 網路上已有了許多教學及流程可以參考，在實作過程中還算順利，所以這邊就只附上我個人的[參考文獻](#參考來源)，並提出些碰到的狀況。

## Q: found no layout file for "HTML" for "page"

這是在我推上github之後，想在本地端啟動server所發生的錯誤，解決方式如下：

重新下載：

- `git submodule init`

- `git submodule update`

[參考來源](https://stackoverflow.com/questions/60269683/how-to-fix-the-error-found-no-layout-file-for-html-for-page-in-hugo-cms)

## 參考來源

[Hugo介紹](https://ithelp.ithome.com.tw/articles/10235097)

[官方文件-Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

[如何將Hugo部落格部署到Github上?](https://yurepo.tw/2021/03/如何將hugo部落格部署到github上/)

[GitHub Actions](https://ithelp.ithome.com.tw/articles/10245847)
