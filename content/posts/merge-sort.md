---
title: "合併排序(merge sort)"
date: 2022-03-18T09:22:50+08:00
draft: false
tags: ["Javascript"]
categories: ["Sorting Algorithm"]
description: "以Javascript實作合併排序。"
hideSummary: false # To Hide summary being shown in list pages
math: true
---

## 前言

> 時間複雜度為 O(n log n) 的演算法。

- 穩定排序
- 時間複雜度
  - 最佳：\\( O(n\log n) \\)
  - 最差：\\( O(n\log n) \\)
  - 平均：\\( O(n\log n) \\)
- 空間複雜度：\\( O(n) \\)

### 操作流程

- 拆分
  1. 把大陣列切一半成為兩個小陣列
  2. 把切好的兩個小陣列再各自切一半
  3. 重複步驟二直到每個小陣列都只剩一個元素
- 合併
  1. 排序兩個只剩一個元素的小陣列並合併
  2. 把兩邊排序好的小陣列合併並排序成一個陣列
  3. 重複步驟二直到所有小陣列都合併成一個大陣列

## 實際操作

> 合併排序的實現方法有兩種：遞迴結構、迭代結構。

### 遞迴結構實作

```javascript
function merge(leftArr, rightArr) {
  let temp = [];
  let [leftIndex, rightIndex] = [0, 0];

  while (leftIndex < leftArr.length && rightIndex < rightArr.length) {
    if (leftArr[leftIndex] < rightArr[rightIndex]) {
      temp.push(leftArr[leftIndex++]);
    } else {
      temp.push(rightArr[rightIndex++]);
    }
  }
  return [...temp, ...leftArr.slice(leftIndex), ...rightArr.slice(rightIndex)];
}

function mergeSort(arr) {
  const n = arr.length;
  if (n < 2) return arr;
  const midIndex = Math.floor(n / 2);
  const leftArray = arr.slice(0, midIndex);
  const rightArray = arr.slice(midIndex);

  return merge(mergeSort(leftArray), mergeSort(rightArray));
}
```

## 參考來源

[JavaScript 學演算法 - 合併排序](https://chupai.github.io/posts/200525_sort_algorithm_merge_sort/)

[排序法進階：合併排序法](https://medium.com/appworks-school/%E5%88%9D%E5%AD%B8%E8%80%85%E5%AD%B8%E6%BC%94%E7%AE%97%E6%B3%95-%E6%8E%92%E5%BA%8F%E6%B3%95%E9%80%B2%E9%9A%8E-%E5%90%88%E4%BD%B5%E6%8E%92%E5%BA%8F%E6%B3%95-6252651c6f7e)
