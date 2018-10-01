---
layout: post
title: "[What is Algorithm] What is Recursion"
subtitle:   "Algorithm"
categories: algorithm
tags: understanding algorithm
comments: true
---

의사코드(Pseudocode)란 문제와 풀이 방법을 간단한 코드 형태로 설명한 것이다. 코드처럼 보이지만 실제로는 인간의 언어와 비슷한 구조이다.



## Recursion

재귀(Recursion)란 함수가 자기 자신을 호출하는 것을 말한다.

재귀는 풀이를 더 명확하게 만들어주지만 재귀를 쓴다고 성능이 더 나이지는 것은 아니다. 가혹 반복문이 더 성능이 좋은 경우가 많다. 이에 대하여 Leigh Caldwell은 다음과 같이 말했다.

> '프로그램에 반복문을 사용하면 프로그램의 성능을 향상시킬 수 있지만, 재귀를 사용하면 프로그래머의 능력을 향상시킬 수 있습니다.'



#### Base case & Recursive case

재귀 함수를 만들 때는 언제 재귀를 멈출지 알려줘야 한다. 기본 단계(Base case)와 재귀 단계(Recursive case)가 필요한 이유이기도 하다.

- Recursive case : 함수가 자기 자신을 호출하는 부분
- Base case : 함수가 자기 자신을 다시 호출하지 않는 경우, 즉 무한 반복으로 빠져들지 않게 하는 부분



## Stack

스택이라는 자료구조는 Push(삽입: 가장 위에 새로운 항목을 추가)와 Pop(떼어내고 읽기: 가장 위의 항목을 떼어내고 읽기) 두 가지 일만 할 수 있다.([What is Stack](https://github.com/JaeWC/TIL/blob/master/Algorithm/%5BDataStructure%5D%20What%20is%20Stack.md))

#### Call Stack

컴퓨터는 호출 스택(Call Stack)이라 불리는 스택을 사용합니다. 

```javascript
function greet(name) {
    console.log('hello, ' + name + '!');
    greet2(name);
    console.log('getting ready to say bye...');
    bye();
	return;
}

function greet2(name) {
    console.log('how are you, ' + name + '?');
	return;
}

function bye() {
    console.log('ok bye!');
	return;
}
```

- `greet('Jae')`라는 명령어가 있다고 가정할 때, 컴퓨터는 이 함수 호출을 위한 Call Stack에 함수를 Push한다.
- 변수 `name`이 `'Jae'`가 되었으므로 이 값을 Call Stack 메모리에 저장한다.
- `greet(name)`함수에 따라 `hello, Jae!`가 출력된 이후, `greet2('Jae')`함수가 호출 순서에 따라 Call Stack에 Push 된다.
- 새로운 함수 호출에 필요한 또 다른 메모리 상자(Call Stack)를 할당한다.
- `how are you, Jae?`라고 반환한 뒤, 함수 호출 상태에서 반환하여 `greet2('Jae')`가 Call Stack에서 Pop된다.
- 이제 Call Stack에는 `greet(name)`함수 만이 남아있고, 함수 호출 순서에 따라 `getting ready say to bye...`가 반환된다.
- 함수 호출 순서에 따라 `bye()`함수가 Call Stack에 Push되고, `ok bye!`가 반한되며 `bye()`함수가 Call Stack에서 Pop 된다.
- 이제 마지막으로 `greet('Jae')`함수가 Pop 되면서 Call Stack이 비워진다.

이와 같이 여러 개의 함수를 호출하면서 함수에 사용되는 변수를 저장하는 스택을 **호출 스택(Call Stack)**이라 한다.



#### Call Stack at Recursion

재귀 함수도 호출 스택을 사용하며, 무엇보다 재귀에서 커다란 역할을 한다. 재귀함수가 호출되면서 Call Stack에 함수가 Push된다. 이처럼 스택을 사용하면 편리하지만 모든 정보를 저장해야 하므로 메모리를 많이 소비하며 함수 호출을 할 때마다 메모리를 사용하게 된다.

Stack이 너무 커졌다는 것은 과다한 함수 호출 정보를 저장하고 있다는 뜻으로 다음과 같은 방법으로 해결할 수 있다.

- 재귀 대신 반복문을 써서 코드를 다시 작성할 수 있다.
- [tail recursion](https://en.wikipedia.org/wiki/Tail_call)을 사용할 수 있다.