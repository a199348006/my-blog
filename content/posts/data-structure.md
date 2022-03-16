---
title: "資料結構簡介"
date: 2022-03-16T13:44:14+08:00
draft: false
tags: ["undefined"]
categories: ["undefined"]
description: "Introduce the data structure."
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

## 常見的資料結構

- 鏈結串列(Linked List)
- 陣列(Array)
- 堆疊(Stack)
- 佇列(Queue)
- 樹狀結構(Tree)
- 圖形結構(Graph)
- 雜湊表(Hash table)
- 堆積(Heap)
- 排序
- 搜尋

## 資料結構分類

- 線性關係
- 非線性關係(階層、相鄰關係)

## 鏈結串列(Linked List)

- 特點：
  - 記憶體位置不連續，以隨機的方式儲存
  - 因為不用事先定義好一塊連續的記憶體空間，所以插入或刪除資料都很方便
  - 每個節點知道下一個節點位置，但無法知道上一個節點位置，所以當想查詢特定節點時，必須從頭節點開始走訪

- 類型：
  - 單向鏈結串列(Singly Linked List)
  - 雙向鏈結串列(Doubly Linked List)
  - 迴圈鏈結串列(Circularly Linked List)

## 陣列(Array)

- 特點：
  - 通常用來儲存有序串列的相同資料於連續記憶空間
  - 記憶體的配置是在編譯的時候完成
  - 須事先宣告固定的記憶體空間，因此容易造成記憶體浪費
  - 讀取與修改串列的資料時間是固定的
  - 刪除或加入新元素需要移動大量資料

## 堆疊(Stack)

- 特點：
  - 只能從頂端存取資料
  - 後進先出的原則
  - 屬於抽象資料型態
  - 只需一個指標：top

- 四種常見的操作：
  - push: 存放資料至頂端，回傳新的堆疊
  - pop: 刪除頂端資料，並回傳新的堆疊
  - isEmpty: 判斷堆疊是否為空
  - full: 判斷堆疊是否為滿

## 佇列(Queue)

- 特點：
  - 先進先出特性
  - 需兩個指標，一個在前端(front)一個在尾端(rear)

- 四種常見的操作：
  - add: 將新的資料加入佇列中
  - delete: 刪除佇列前端的資料
  - front: 傳回佇列前端的值
  - empty: 判斷佇列是否為空

## 樹狀結構(Tree)

樹的定義與特性：
> 樹是由一個根節點(Root)開始發展，在樹狀結構中的最基本單位，稱為節點
(Node)，而分支出去的節點稱為子節點(Child)。樹是沒有環的結構，且任意兩節點間只有一個唯一路徑，若隨意刪除其中一個枝 (Branch)，就會變兩個樹。

- 節點(Node)：樹狀結構中每一個資料元素都稱為節點
- 枝(Branch)：節點向下延伸擴展的所用到的枝
- 根節點(Root)：根節點具有唯一性，是整個樹狀結構最上層的樹根
- 葉節點(Leaf)：節點之下都沒有子節點稱為葉節點(像樹葉的葉子)
- 非終端點(Non-terminal Nodes)：除了葉節點外的其他節點
- 祖先節點(Ancenstors) 與子孫節點 (Descendant)
- 父節點(Parent)與子節點 (Child)
- 兄弟節點(Siblings)：同一個父節點的其他節點，稱為兄弟節點
- 分支度(Dregree)：每個節點所擁有的子節點數
- 階層(Level)：從樹根開始，向下延伸的層級
- 樹深(Depth)：節點與節點間的距離。根節點深度為0

### 樹的類型

- 二元樹(Binary tree)
  - 歪斜樹(Skewed Tree)：只有左或右節點
  - 嚴格二元樹(Strictly binary tree)：子節點只能為0或2
  - 完滿二元樹(Full Binary Tree)：每個節點都有兩個子節點
  - 完整二元樹(Complete Binary Tree)：由上而下、由左至右排列
  - 二元搜尋樹(Binary Search Tree)：每一個節點的資料大於左邊的子節點
    - 平衡樹
      - AVL樹(Adelson-Velsky and Landis Tree)：每一個節點的的左邊子節點的高度-右邊子節點的高度只能是 -1、0、1
      - 紅黑樹(Red–black tree)：利用節點顏色，減少平衡操作的旋轉次數

## 圖形結構(Graph)

> 圖是由點、邊組成，通常用G=(V,E)表示，V是節點(Vertice)，E是邊(Edge)，圖可以分成有向圖與無向圖，無向圖以(V1,V2)表示，有向圖以<V1,V2>表示。

### 圖的類型

- 加權圖形(Weighted Graph)
- 無向圖
- 有向圖

## 雜湊表(Hash table)

雜湊表的定義與特性：
> 雜湊表的所儲存的資料元素都有成對的鍵(Key)及值(Value)，將Key經過雜湊函數(Hash Function)後，計算出新的值並放入對應的陣列索引中。若發生雜湊碰撞(collsion)，則使用連結串列的方式儲存。此資料結構方法被廣泛運用在資料庫搜索、關鍵字搜尋、快取等。

[雜湊表說明](https://ithelp.ithome.com.tw/articles/10273568)

## 堆積(Heap)

> 堆積是圖形結構中的樹狀結構中的一種，用於實踐優先佇列(Priority Queue)。利用保持資料結構的一定規則(從小到大或從大到小)，來確保拿取資料的效率。

堆積的定義與特性：
> 堆積一種特殊的二元樹資料結構，但不全然相同，每個節點(node)最多只有兩個子節點，而子節點與父節點之間要維持一定規則，同層的兄弟節點則無規則限制，但同一層要維持從左到右新增節點，滿了才可增加下一層。

[堆積說明](https://ithelp.ithome.com.tw/articles/10274286)

## 參考來源

[資料結構概念.pdf](https://www.wun-ching.com.tw/img/Books_files/C189-9789864300525-trial.pdf)

[基本演算法](https://zh-tw.coderbridge.com/series/cfe509b1adfd4b02ac1c0705ff28c28c/posts/12f738953ee243f7a95adecc4636d82b)

[資料結構-iT邦](https://ithelp.ithome.com.tw/users/20116811/ironman/4842)

[JavaScript 學演算法](https://chupai.github.io/series/javascript-%E5%AD%B8%E6%BC%94%E7%AE%97%E6%B3%95/page/2/)
