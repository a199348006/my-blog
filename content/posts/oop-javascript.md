---
title: "物件導向：Javascript"
date: 2022-03-26T16:16:25+08:00
draft: false
tags: ["Javascript", "OOP"]
categories: ["Undefined"]
description: "OOP(Object-oriented programming) in javascript."
hideSummary: false # To Hide summary being shown in list pages
---

## 前言

> 記錄以物件導向程式設計來寫Javascript(ES6)。

## Class 訪問器及靜態方法

```javascript
class Person {
  constructor (name, age) {
    this._name = 'Chowder';
    this.age = age;
  }

  get name() {
    console.log('get')
    return this._name;
  }

  set name(newValue) {
    console.log('set')
    this._name = newValue;
  }

  static foo() {
    console.log('it is foo.')
  }
}

Person.foo(); // it is foo.

let p = new Person('Chowder', 25);
console.log(p);  // Person { _name: 'Chowder', age: 25 }
p.name           // get
p.name = 'Kevin' // set
console.log(p)   // Person { _name: 'Kevin', age: 25 }                            
```

## Class 繼承

```javascript
class Person {
  constructor (name, age) {
    this.name = name;
    this.age = age;
  }

  eating() {
    console.log(this.name, 'is eating.')
  }
}

class Student extends Person {
  constructor (name, age, sno) {
    super(name, age); // super: call parent constructor
    this.sno = sno;
  }

  studying() {
    console.log(this.name, 'is studying.')
  }

  eating() { // cover parent func
    super.eating(); // super: call parent func
    console.log('Student is eating.')
  }
}

let s = new Student('Allen', 18, 20220001);
console.log(s) // Student { name: 'Allen', age: 18, sno: 20220001 }
s.eating();    // Allen is eating.
               // Student is eating.
s.studying();  // Allen is studying.
```

## Class 繼承內建Class

```javascript
class myArray extends Array {
  firstItem() {
    return this[0];
  }

  lastItem() {
    return this[this.length - 1];
  }
}

let arr = new myArray(9, 8, 7, 6, 5);
console.log(arr.firstItem())
console.log(arr.lastItem())
```

## 參考來源

[JavaScript物件導向—深入ES6的class](https://iter01.com/670548.html)

[iT邦幫忙](https://ithelp.ithome.com.tw/articles/10220019)
