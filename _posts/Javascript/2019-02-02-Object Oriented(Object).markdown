---
layout: post
title:  "Object Oriented - Object"
description: "Object Oriented - Object"
date:   2019-02-02 20:00:00
categories: Javascript
comments: true
---
Object 객체는 객체의 가장 기본적인 형태를 가지고 있는 객체이다. 따라서 모든 객체들은 Object를 상속받고 Object 객체의 property와 method를 사용할 수 있다. prototype을 통해 상속되는 속성들은 새롭게 생성되는 모든 객체가 개별적으로 사용이 가능하지만 다른 속성들은 Java/C#의 static variable/method처럼 사용한다. method는 인자로 객체를 전달해주어서 사용하는 방식 (ex. Object.keys(arr)) 이다.

* Object 객체 또한 표준 내장 객체이므로 prototype property에 원하는 property나 method를 추가하여 모든 객체들에게 필요한 기능들을 확장이 가능하다.
* 그러나 표준 내장 객체의 확장은 해당 객체를 상속받는 모든 객체에 영향을 미치므로 신중히 설계하도록 하자.