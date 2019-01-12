---
layout: post
title:  "Function Oriented - Scoping"
description: "Function Oriented - Scoping"
date:   2019-01-12 19:40:00
categories: Javascript
comments: true
---
- 정적 유효범위 (Static Scoping) = Lexical Scoping

```javascript
var i = 10;
// a 함수에서의 i = 5는 b 함수에 영향을 미치지 못한다.
function a(){
    var i = 5;
    b();
}

function b(){
    Console.log(i);
}
```