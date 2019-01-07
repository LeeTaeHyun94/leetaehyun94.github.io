---
layout: post
title:  "Regular Expression"
description: "Regular Expression in Javascript"
date:   2019-01-07 23:30:00
categories: Javascript
comments: true
---
문자열에서 특정한 문자를 찾아내는 도구
```javascript
var pattern = /a/ = new RegExp('a');
pattern.exec('abcdef'); // return Object ["a", index : 0, input: "abcdef", groups: undefined]
			// 필요한 정보를 추출
'abcdef'.match(pattern);
pattern.test('abcdef'); // return boolean
			// 패턴의 유무
'abcdef'.replace(pattern, 'A'); // 패턴을 찾고 전달한 문자열로 교체

/(\w+)\s(\w+)/ // $1(하나 이상의 심볼) + 공백 + $2(하나 이상의 심볼)

var urlPattern = /\b(?:https?):\/\/[a-z0-9-+&@#\/%?=~_|!:,.;]*/gim;
```