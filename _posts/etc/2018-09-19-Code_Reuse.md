---
layout: post
title: "[Computer Science] What is Code Reuse"
subtitle:   "Computer Science"
categories: etc
tags: Efficiency
comments: true
---

## Code Reuse

반복된 작업을 줄이고 에러 발생 확률을 낮추기 위한 용도로 작서한 Code를 재사용한다. 유사한 작업을 반복하는 코드를 재사용할 경우, 코드 수정 혹은 업데이트 등의 관리를 효과적으로 할 수 있게 된다.
Code를 재사용하는 방법으로 `Functions`, `Decorators`, `Classes`가 있다. 이 중 `Functions`은 재사용 가능성이 높은 코드를 함수화하는 것을 의미한다.

### Decorators

> Decorators는 특정 동작으로 기존의 Object Instance를 보완한다.

### Classes

> Class는 특정 타입을 갖춘 샐운 Object Instance를 생성한다.


## Instantiation Patterns

Instantiation Pattern은 Object가 어떻게 존재하는 지를 설명해준다. JavaScript에서는 다음의 4가지 Pattern이 있다.
`Functional`, `Functional-shared`, `prototypal`, `pseudoclassical`.

#### Functional Instantiation

함수를 이용해서 Object를 만드는 방식으로 객체를 Instantiation할 때, 발생하는 작업의 양으로 인해 memory와 CPU 등의 컴퓨터 자원이 가장 많이 사용된다. Instance를 생성할 때 마다 각각의 인스턴스들이 메소드의 수 만큼 메모리를 차지하기 떄문이다.
Istantiation 과정에서 Closure가 만들어질 것이기 때문에 Private 변수를 사용가능하게 만드는 유일한 Pattern이다. 

#### Funtion-Shared Instantiation

Function-Shared Pattern은 특정 객체에서 하나의 함수를 추출하여 Instance를 생성한다. 이 경우에는 메소드의 메모리 주소 만을 참조하기 때문에 memory효율이 좋아진다. 
모든 Instance는 같은 함수를 참조하게 되며, Instance의 property에 접근하기 위해 `this`를 사용해야 한다.

#### Prototypal Instantiation

특정 객체를 prototype으로 하는 객체를 생성해주는 `Object.create()`함수를 사용하여 Instance를 생성한다. 
`Object.create()`메서드는 지정된 프로토타입 object 및 property를 갖는 새로운 객체를 만든다. 

#### Pseudoclassical Instantiation

메소드 자체를 prototype으로 만들어서 Instance를 생성하는 방법이다. 