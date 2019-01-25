---
layout: post
title:  "Function Oriented - Calling Function"
description: "Function Oriented - Calling Function"
date:   2019-01-25 20:10:00
categories: Javascript
comments: true
---
우리가 사용하는 함수들은 모두 Function 객체의 인스턴스이다. 때문에 Function 객체의 내장 메소드들을 사용가능한데, 호출에 사용되는 메소드는 apply와 call이 있다.
```javascript
function sum(arg1, arg2) {
    return arg1 + arg2;
}
console.log(sum.apply(null, [1, 2]));

o1 = {val1 : 1, val2 : 2, val3 : 3}
o2 = {v1 : 10, v2 : 50, v3 : 100, v4 : 25}
function sum(){
    var _sum = 0;
    for(name in this){ // this에 객체를 인자로 전달
        _sum += this[name];
    }
    return _sum;
}
console.log(sum.apply(o1)) // 6
console.log(sum.apply(o2)) // 185
```