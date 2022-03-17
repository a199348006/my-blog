---
title: "XAMPP常用設定"
date: 2022-01-27T10:17:46+08:00
draft: false
tags: ["XAMPP"]
categories: ["Undefined"]
description: "XAMPP config setting after install XAMPP"
hideSummary: true # To Hide summary being shown in list pages
---

## 更改XAMPP文字編輯器

- 點右上角config鈕
- 在Editor方塊內選文字編輯器(ex:Notepad++)

***

## 更改phpMyAdmin認證模式，開啟檔案：phpMyAdmin(config.inc.php)

- 將['auth_type'] = 'config';  改成 ['auth_type'] = 'cookie'; (網頁式密碼輸入對話框) 或  ['auth_type'] = 'http'; (彈出式密碼輸入對話框)
- 如果改成'http'，則可修改密鑰   $cfg['blowfish_secret'] = 'xampp'   (不改也可)
- 儲存後重新啟動控制面板

***

## 啟動如出現錯誤

- 檢查xampp是否放置於中文資料夾
- 點選右側NetStat鈕 ，查看80(http)、443(https)、3306(MySQL)Port是否被佔用

***

## 更改http 80port為8080port，開啟檔案：Apache(httpd.conf)

- 搜尋80(有兩處要改)

  `Listen 8080`

  `ServerName localhost:8080`

***

## 更改預設首頁資料夾，開啟檔案：Apache(httpd.conf)

- 搜尋 'htdocs'
- 修改路徑1：DocumentRoot "C:/xampp/htdocs/xxxxx"
- 修改路徑2：Directory "C:/xampp/htdocs/xxxxx"

**P.S. 也可在C:\XAMPP\htdocs中修改index.php內容：header('Location: '.$uri.'/xxx/');**

***

## 避免瀏覽器列出檔案目錄，開啟檔案：Apache(httpd.conf)

- 上面更改htdocs的位置下方
- Options Indexes FollowSymLinks Includes ExecCGI (刪除Indexes)

***

## 更改PHP能使用短標籤，開啟檔案：PHP(php.ini)

- 搜尋 'short'
- 更改為 short_open_tag=on

***

## 更改時區，開啟檔案：PHP(php.ini)

- 將內容拉至最下方
- 修改為 date.timezone=Asia/Taipei

***

## 是否顯示錯誤訊息，開啟檔案：PHP(php.ini)

- 搜尋'dispaly'
- 修改為display_errors=Off

`config.inc.php 新增密碼後 $cfg['Servers'][$i]['password'] = 'xxxxxx'; 出現 Access Denied for User 'root'@'localhost' (using password : NO) 錯誤`

- 在 my.ini 檔案中的 [mysqld] 段落中新增一行 skip-grant-tables  
- 重新啟動 Apache 和 MySQL

***

## 設定遠端可連線phpMyAdmin

- 修改 [httpd-xampp.conf] 檔案中93和105行的 Require local 改成 Require all granted
- 重新啟動XAMPP的 Apache 和 MySQL

***

## 參考來源

<http://ep.ckvs.tyc.edu.tw/blog/files/6-5919-9316.php>
