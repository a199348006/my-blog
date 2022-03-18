---
title: "泡沫排序(bubble sort)"
date: 2022-03-18T09:59:14+08:00
draft: false
tags: ["Javascript"]
categories: ["Sorting Algorithm"]
description: "以Javascript實作泡沫排序。"
hideSummary: false # To Hide summary being shown in list pages
math: true
---

## 前言

> 氣泡排序(Bubble Sort)又稱為冒泡排序、泡沫排序，是排序演算法中最簡單的，但運行時間是最差的。

- 穩定排序
- 時間複雜度
  - 最佳：\\( O(n\log n) \\)
  - 最差：\\( O(n^2) \\)
  - 平均：\\( O(n^2) \\)
- 空間複雜度：\\( O(1) \\)

### 操作流程

- Round 1
  - 比較相鄰元素，前者大於後者就相互交換
  - 從頭到尾執行，確保最後一個元素為最大值
- Round 2
  - 扣除最後一個元素，並重複Round 1

## 實際操作

```Javascript
function swap(arr, index1, index2) {
  const temp = arr[index1];
  arr[index1] = arr[index2];
  arr[index2] = temp;
}

function bubbleSort(arr) {
  const n = arr.length;
  let swapped = true;
  for (let i = 0; (i < n - 1) && swapped; i++) {
    swapped = false;
    for (let j = 0; j < n - 1 - i; j++) {
      if(arr[j] > arr[j + 1]) {
        swapped = true;
        swap(arr, j, j + 1);
      }
    }
  }
  return arr;
}
```

## 參考來源

[JavaScript 學演算法](https://chupai.github.io/posts/200518_sort_algorithm/)