---
layout: post
title:  "Function Oriented - Closure"
description: "Function Oriented - Closure"
date:   2019-01-24 20:10:00
categories: Javascript
comments: true
---
```javascript
function sum(){
    var i, _sum = 0;    
    for(i = 0; i < arguments.length; i++){
        console.log(i + ' : ' + arguments[i]);
        _sum += arguments[i];
    }   
    return _sum;
}
console.log('result : ' + sum(1,2,3,4));
// 이처럼 sum 함수에 인자를 전달받는 부분이 없음에도 불구하고 1, 2, 3, 4를 인자로 전달할 수 있다.
// 이유는 모든 함수에는 arguments라는 특수한 배열이 있기 때문이다.

function zero(){
    console.log(
        'zero.length', zero.length, // 함수로 전달된 실제 인자의 수를 의미
        'arguments', arguments.length // 함수에 정의된 인자의 수를 의미
    );
}
function one(arg1){
    console.log(
        'one.length', one.length,
        'arguments', arguments.length
    );
}
function two(arg1, arg2){
    console.log(
        'two.length', two.length,
        'arguments', arguments.length
    );
}
zero(); // zero.length 0 arguments 0 
one('val1', 'val2');  // one.length 1 arguments 2 
two('val1');  // two.length 2 arguments 1
```