---
layout: post
title:  "Object Oriented - Extension of standard embedded object"
description: "Object Oriented - Extension of standard embedded object"
date:   2019-02-01 10:40:00
categories: Javascript
comments: true
---
- 표준 내장 객체 : Javascript가 기본적으로 갖고 있는 객체 (Object, Function, Array, String, Boolean, Number, Math, Date, RegExp)

```javascript
Array.prototype.rand = function() {
    return this[Math.floor(this.length * Math.random())];
};
var arr = new Array('seoul', 'new york', 'ladarkh', 'pusan', 'Tsukuba');
console.log(arr.rand());
// 이러한 방식으로 표준 내장 객체의 prototype property를 통해
// 원하는 property나 method를 확장시킬 수 있다.
```