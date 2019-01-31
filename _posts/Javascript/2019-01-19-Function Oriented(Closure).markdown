---
layout: post
title:  "Function Oriented - Arguments"
description: "Function Oriented - Arguments"
date:   2019-01-19 20:30:00
categories: Javascript
comments: true
---
내부 함수가 외부 함수의 Context에 접근하는 행위

내부 함수에서는 외부 함수의 지역 변수에 접근 가능하다는 것이 특징.
```javascript
function outter() {
    var title = 'coding everybody';
    function inner() {
        console.log(title);
    }
    inner();
}
outter();
// 어떤 특정한 외부 함수 내부에서만 쓰고 싶은 함수를 외부 함수 안 쪽에 함수를 선언하게 된다.
// inner 함수에서 밖의 title 변수에 접근 가능하다.
function outter() {
    var title = 'coding everybody';
    return function() {
        console.log(title);
    }
}
inner = outter();
inner();
// 외부 함수의 실행이 끝나서 외부 함수가 소멸된 이후에도 내부 함수는 외부 함수의 변수에 접근할 수 있다.
// 이러한 메커니즘을 Closure 라고 한다.
```

## 1. Private Variable

```javascript
function factory_movie(title) {
    return {
        get_title : function() {
            return title;
        },
        set_title : function(_title) {
            title = _title
        }        
    };
}
ghost = factory_movie('Ghost in the shell');
matrix = factory_movie('Matrix');
console.log(ghost.get_title());
console.log(matrix.get_title());
ghost.set_title('공각기동대');
console.log(ghost.get_title());
console.log(matrix.get_title());
// 이와 같은 방식으로 같은 함수를 통해 다른 객체를 만들 수 있다.
// 외부 함수의 지역 변수인 title이 서로 다른 같은 모양의 객체를 만들 수 있다는 것!
// title 같은 private variable을 프로그래밍 가능하다.
```

## 2. Closure를 응용하며 주의해야 할 점
함수가 값으로 사용될 수 있는 특성을 이용하여 함수의 인자로 전달해주면 인자로 전달해 준 함수가 호출되는 것을 통해 실행하고자 하는 함수의 동작 방식을 바꿀 수 있다.

```javascript
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(){
        return i;
    }
}
for(var index in arr) {
    console.log(arr[index]());
}
// 이렇게 코딩하면 arr 배열의 값들은 전부 5가 된다. 생각처럼 0, 1, 2, 3, 4 가 저장되지 않는 것을 볼 수 있다.
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(id) {
        return function(){
            return id;
        }
    }(i);
}
for(var index in arr) {
    console.log(arr[index]());
}
// 이렇게 배열의 값에 외부 함수의 지역 변수로 id를 선언하고 그 id를 반환하는 내부 함수를 반환하는 외부 함수를 구성하게 되면
// 배열의 각 인덱스에는 개별적으로 외부 함수의 private variable 값이 들어가게 되어
// 0, 1, 2, 3, 4를 저장할 수 있게 된다.
```