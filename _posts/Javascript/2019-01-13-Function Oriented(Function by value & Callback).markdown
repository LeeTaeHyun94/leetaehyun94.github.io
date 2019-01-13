---
layout: post
title:  "Function Oriented - Function by value & Callback"
description: "Function Oriented - Function by value & Callback"
date:   2019-01-13 20:35:00
categories: Javascript
comments: true
---
Javascript에서는 함수 또한 객체 (일종의 값)

## 1. 함수의 다양한 형태(용도)

```javascript
var a = {
    b : function(){
        
    }
}; // 이런 식으로 변수에 함수 값을 대입 가능하다.

function cal(func, num) {
    return func(num);
}
function increase(num) {
    return num + 1;
}
function decrease(num) {
    return num - 1;
}
console.log(cal(increase, 1));
console.log(cal(decrease, 1));

function cal(mode) {
    var funcs = {
        'plus' : function(left, right) { return left + right; },
        'minus' : function(left, right) { return left - right; }
    };
    return funcs[mode];
}
console.log(cal('plus')(2, 1));
console.log(cal('minus')(2, 1));
// 함수의 return 값으로도 사용 가능

var process = [
    function(input) { return input + 10; },
    function(input) { return input * input; },
    function(input) { return input / 2; }
];
var input = 1;
for(var i = 0; i < process.length; i++) input = process[input];
console.log(input);
// 배열의 값으로도 함수를 대입 가능하다.
```

## 2. Callback
함수가 값으로 사용될 수 있는 특성을 이용하여 함수의 인자로 전달해주면 인자로 전달해 준 함수가 호출되는 것을 통해 실행하고자 하는 함수의 동작 방식을 바꿀 수 있다.

```javascript
var numbers = [20, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1];
var sortFunc = function(a, b) {
    return b - a;
};
console.log(numbers.sort(sortFunc));
// 원래 sort 메소드는 배열의 숫자들을 문자열로 처리해서 사전 순으로 정렬해주지만 직접 정렬을 위한 함수를 작성하여 인자로
// 전달해주게 되면 숫자의 크기를 오름차순으로 정렬이 된다.
```

- Ajax를 통한 비동기 처리에서 콜백이 유용하게 사용된다.