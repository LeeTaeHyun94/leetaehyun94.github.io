---
layout: post
title:  "Object Oriented - constructor, new"
description: "Object Oriented - constructor, new"
date:   2019-01-27 22:05:00
categories: Javascript
comments: true
---
```javascript
var person = {}; // 비어 있는 객체 생성 (Literal Object)
person.name = 'llstaaar';
person.introduce = function() {
    return 'My name is ' + this.name;
};
console.log(person.introduce());
// 위 코드는 객체를 만드는 과정이 분산되어 있으므로 객체를 정의할 때 값도 저장하도록 하자.

var person = {
    'name' : 'llstaaar',
    'introduce' : function() { return 'My name is ' + this.name; }
};
// 하지만 이 코드 또한 같은 특징을 가진 객체를 생성할 때 코드의 중복이 생기므로 좋은 코드는 아니다.

    Constructor (생성자) : 객체를 만드는 역할을 하는 함수, 변수를 선언하면서 new 키워드를 붙여주면 함수가 객체의 생성자로 사용되는 것을 알 수 있다.

function Person(name) {
    this.name = name;
    this.introduce = function() {
        return 'My name is ' + this.name;
    };
}
var p1 = new Person('llstaaar');
var p2 = new Person('llmooon');
console.log(p1.introduce());
console.log(p2.introduce());
```