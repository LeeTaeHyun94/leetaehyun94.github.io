---
layout: post
title:  "Aspect Oriented Programming"
description: "AOP (Aspect Oriented Programming)"
date:   2019-02-08 10:20:00
categories: Spring
comments: true
---
- Aspect : 공통 관심사에 대한 추상적인 명칭, Business Logic은 아니지만 반드시 해야하는 공통된 작업 (ex : logging, security, transaction...)
	- Before Advice : Target의 메소드 호출 전에 적용  
	- After Returning : Target의 메소드 호출 이후에 적용  
	- After Throwing : Target의 예외 발생 후에 적용  
	- After : Target의 메소드 호출 후, 예외의 발생에 관계없이 적용  
	- Around : Target의 메소드 호출 전후 모두 적용
- Advice : 실제 기능을 구현한 걕체 (클래스를 제작하고 @Advice를 적용)
- Join Points : 공통 관심사를 적용할 수 있는 대상. (Spring AOP에서는 각 객체의 메소드가 해당)
- Pointcuts : 실제 Advice가 적용될 메소드
- Target : 대상 메소드를 가지는 객체 (실제 비즈니스 로직을 수행하는 객체)
- Proxy : Advice가 적용되어 만들어지는 걕체
- Introduction : Target에 없는 새로운 메소드나 인스턴스 변수를 추가하는 기능
- Weaving : Advice와 Target이 결합되어 Proxy 객체를 만드는 과정