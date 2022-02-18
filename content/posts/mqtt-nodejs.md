---
title: "MQTT and mqtt.js"
date: 2022-02-17T16:21:29+08:00
draft: false
tags: ["MQTT", "Node.js"]
categories: ["undefined"]
description: "MQTT介紹、MQTT Explorer軟體應用及mqtt.js小測試"
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

> 在這裡只記錄些實作過程中的摘要，若是想觀看圖文並茂的文章及教程可以至最下方的[參考來源](#參考來源)。

套件版本：

- mosquitto: 2.0.14
- MQTT Explorer: 0.4.0-beta
- mqtt.js: 4.3.5

## MQTT簡介

MQTT的架構中分為以下三者：

- Publisher(發佈者)：發佈訊息的人
- Broker(代理人)：負責接收來自Publisher的訊息並發訊息給Subscribe
- Subscriber(訂閱者)：接收訊息的人

### MQTT訊息格式

> Control Header及Remaining Length皆必須存在，已Publish Message來說Variable Header>會放入topic主題，Payload放入傳遞的訊息內容。

- Control Header
- Remaining Length
- Variable Header: **topic**
- Payload: **message**

### 網路品質(QoS)

> MQTT定義了0, 1和2三個層級的品質設定：
>
> - 0: 最多傳送一次(at most once)
> - 1: 至少傳送一次(at leat once)
> - 2: 確實傳送一次(exactly once)

[詳細教程](https://swf.com.tw/?p=1015)

## 安裝Mosquitto Windows及相關設定

### Mosquitto安裝

[Mosquitto Download](https://mosquitto.org/download/)

> 安裝過程中Service可以取消勾選(手動開啟BQTT Broker功能)
>
> - [ ] Service: 手動開啟BQTT Broker功能
> - [x] Service: 開機執行

_防火牆也需要到**進階設定**->**輸入規則**->**新增規則**->**將預設port: 1883開啟**，**輸出規則**重複上述操作。_

[詳細安裝及防火牆設置參照](https://jimirobot.tw/esp32-mosquitto-windows-mqtt-tutorial/)

### Mosquitto conf設定

> 安裝目錄預設為C:\Program Files\mosquitto

#### 新增mosquitto\usrlist.txt

```txt
帳號:密碼
admin:admin
```

執行CMD: `mosquitto_passwd.exe -U usrlist.txt`，此時可以看看usrlist.txt的變化。

#### 修改mosquitto\mosquitto.conf

在文件末端加入

```txt
allow_anonymous false
password_file C:\Programs Files\mosquitto\usrlist.txt
listener 1883
```

- allow_anonymous false: 不允許匿名登入
- password_file: 指定帳號清單的目錄
- listener: 指定遠端登入時可以使用的PORT

### 啟動MQTT Broker

`mosquitto.exe -c mosquitto.conf -v`

- -c: 指定config檔名
- -v: verbose mode詳細模式

### 安裝MQTT Client軟體測試Server連線

[MQTT Explorer](http://mqtt-explorer.com/)

透過MQTT Explorer在Publish中輸入Topic及要傳遞的訊息並送出。(如下圖)

![MQTT Explorer](/my-blog/images/mqtt/mqtt-explorer.png)

## Subscribe

### 萬用字元

> 訂閱主題搭配萬用字元：**+** 和 **#**，來實現訂閱單層或多層相關主題。
>
> - +字元：匹配單一階層的主題名稱
> - #字元：匹配多層主題名稱，**這個字元只放在名稱最後**

例：example/topic/+/a，涵蓋：

- example/topic/first/a
- example/topic/second/a

例：example/topic/#，涵蓋：

- example/topic/first/a
- example/topic/second/a
- example/topic/second/b
- example/topic/third

## Node.js with mqtt.js

> 利用MQTT Explorer發佈訊息時，訂閱者收到訂閱內容。

```javascript
const mqtt = require('mqtt');
const options = {
  port: 1883,
  clinetId: 'chowder',
  username: 'username', // 填入先前設定的帳號密碼
  password: 'password',
};

const client = mqtt.connect('mqtt://127.0.0.1', options);
client.on('connect', function () {
  console.log('Connecting to mqtt.');
  client.subscribe('example/topic/#');
});

client.on('message', function (topic, msg) {
  console.log(topic, msg.toString());
});
```

[詳細實作教程](https://swf.com.tw/?p=1023)

[mqtt.js官方說明](https://yarnpkg.com/package/mqtt)

## 參考來源

[MQTT-JIMI](https://jimirobot.tw/esp32-mosquitto-windows-mqtt-tutorial/)

[MQTT-cubie](https://swf.com.tw/?p=1002)
