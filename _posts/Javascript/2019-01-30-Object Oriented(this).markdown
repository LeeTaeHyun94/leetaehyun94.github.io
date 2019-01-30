---
layout: post
title:  "Object Oriented - this"
description: "Object Oriented - this"
date:   2019-01-30 21:25:00
categories: Javascript
comments: true
---
- this : 함수 내에서의 함수 호출 맥락(Context), Javascript에서는 함수와 객체의 느슨한 관계를 연결시켜주는 역할을 하는 키워드, 함수를 어떻게 호출하느냐에 따라서 this가 가리키는 대상이 달라진다.

```javascript
this === window; // true, 평문에서의 this는 전역 객체인 window를 가리킨다.
var o = {
    func : function() {
        if(o === this) console.log("o === this");
    } // 객체에 속하는 메소드의 this는 그 객체를 가리킨다.
};

// 생성자(함수) 안에 있는 this는 함수로 호출됐을 때는 전역 객체인 window를 가리키고
// 생성자로 사용됐을 때는 생성되는 객체를 가리키게 된다.

function sum1(x, y) { return x + y; }
var sum2 = new Function('x', 'y', 'return x + y;'); // 객체로서 함수를 선언

var o = {}
var p = {}
function func(){
    switch(this){
        case o:
           	console.log('o');
            break;
        case p:
            console.log('p');
            break;
        case window:
            console.log('window');
            break;          
    }
}
func(); // 함수를 그냥 호출했을 때에는 this === window
func.apply(o); // apply 메소드를 통해 o 객체를 인자로 전달하여 함수를 호출하면 this === o
func.apply(p); // apply 메소드를 통해 p 객체를 인자로 전달하여 함수를 호출하면 this === p
```