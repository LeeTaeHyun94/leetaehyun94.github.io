---
layout: post
title:  "Object Oriented - Reference"
description: "Object Oriented - Reference"
date:   2019-02-04 20:06:00
categories: Javascript
comments: true
---
* 복제 : variable의 value 만을 그대로 복사한다.

```javascript
var a = 1, b = a;
console.log(a);
b = 2;
console.log(a);

var a = {'id' : 1}, b = a;
console.log(a.id);
b.id = 2;
console.log(a.id);
// 위 두 코드의 코딩 방식은 비슷했다. 하지만 결과 값은 비슷하지 않은 것을 알 수 있었다.
// 코드에 대해 정확히 설명하면
// 변수에 저장된 데이터가 Primitive Type이라면 실제 value가 저장되어 있지만
// 객체의 데이터가 저장되어 있다면 실제로는 객체의 value에 대해 참조가 되어 있다는 것을 알 수 있다.

var a = {'id' : 1}, b = a;
console.log(a.id);
b = {'id' : 2}; // 왜냐면 Literal Object로 새로운 객체를 할당했기 때문.
console.log(a.id);
// 그러나 이렇게 코딩해도 a의 데이터가 변하진 않는다.

var a = {'id' : 1};
function func(b) {
    b = {'id' : 2}; // 이 코드도 위와 마찬가지로 b에는 새로운 객체가 참조되었다.
}
func(a);
console.log(a.id);

var a = {'id' : 1};
function func(b) {
    b.id = a; // 하지만 이 코드는 b가 a를 참조하고 있으므로 출력되는 값이 바뀐다.
}
func(a);
console.log(a.id);
```