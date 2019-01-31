---
layout: post
title:  "Object Oriented - Inheritance"
description: "Object Oriented - Inheritance"
date:   2019-01-31 10:35:00
categories: Javascript
comments: true
---
상속을 통해 객체의 로직을 그대로 물려받는 또 다른 객체를 만들 수 있다.

```javascript
function Person(name) {
    this.name = name;
}
Person.prototype.name = null;
Person.prototype.introduce = function () { return 'My name is ' + this.name; };
var p1 = new Person('llstaaar');
console.log(p1.introduce());
function Programmer(name) {
    this.name = name;
}
Programmer.prototype = new Person();
// prototype이라는 특수한 Property에 상속받을 객체를 생성하여 대입하면 Person 객체의
// prototype property의 정보들을 갖고 객체를 생성하여 넘겨주는 방식

Programmer.prototype.coding = function () { return 'Hello, World!'; };
// prototype property를 통해 새로운 property나 method들을 추가해줄 수 있다.

var p2 = new Programmer('llstaaar');
console.log(p2.introduce());
```

- Prototype (원형) : 이 property는 어떤 용도가 약속되어 있는 특수한 property이기 때문에 prototype에 저장되어 있는 속성들은 생성자를 통해서 생성된 객체에 연결된다.
- Prototype Chain : 이러한 prototype에 의한 상속이 얽혀있는 관계를 의미한다. property의 value를 찾는 과정은 자기 자신을 생성한 객체의 property -> prototype -> 부모의 property -> 부모의 prototype 값을 갖고 있는 property를 찾을 때까지 역순으로 찾아 나간다.