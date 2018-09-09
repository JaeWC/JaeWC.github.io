---
layout: post
title: "[recursion] 02. stringifyJSON"
subtitle:   "Recursion"
categories: JavaScript
tags: Recursion
comments: true
---

## Recursion

2\. **stringifyJSON** 

 - [JSON.stringify의 MDN 자료](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)
 - 위의 JSON.stringify에 대한 MDN의 자료를 우선적으로 참고하는 것이 좋다.간단하게 stringifyJSON 함수는 주어진 인자를 JSON 문자열로 반환해주는 함수이다.

 - stringifyJSON 구현 아이디어(JSON.stringify API에 기반)
> - 인자로 string이 들어갈 경우, 따옴표가 string 자체에 추가된다.
> - Boolean, Number, null은 해당 값을 String으로 바꿔줘서 출력된다.
> - Array와 Object는 앞뒤의 []와 {}를 포함하여 내부의 값들을 해당 타입에 맞춰서 문자열로 바꿔서 출력해준다.
> - undefined, 함수, 심볼은 Object에서는 생략되고, Array에서는 null로 출력된다.
> - 기본 자료형의 stringifyJSON 패턴을 구현한뒤, Array와 Object를 나눠서 각 원소들을 recursion으로 문자형으로 변환시켜주면 된다.

 - stringifyJSON 함수 구현  
```javascript
var stringifyJSON = function(obj) {
  if (typeof obj === 'string') {
  	return '"' + obj + '"';
  } else if (typeof obj === 'boolean' || typeof obj === 'number' || obj === null) {
  	return String(obj);
  }
  if (Array.isArray(obj)) {
  	if (obj.length === 0) {
  		return '[]';
  	} else {
  		var stringArr = []
  		for (var i = 0; i < obj.length; i++) {
  			if (obj[i] === undefined || typeof obj[i] === 'function' || typeof obj[i] === 'symbol') {
  				stringArr.push(stringifyJSON(null));
  			} else {
  				stringArr.push(stringifyJSON(obj[i]));
  			}
  		}
  		return '[' + stringArr.join() + ']';
  	}
  }
  if (Object.keys(obj).length === 0) {
  	return '{}';
  } else {
  	var stringObj = ''
  	for (var prop in obj) {
  		if (obj[prop] === undefined || typeof obj[prop] === 'function' || typeof obj[prop] === 'symbol') {
  			delete obj[prop];
  			stringifyJSON(obj);
  		} else {
  			stringObj += stringifyJSON(prop) + ':' + stringifyJSON(obj[prop]) + ',';
  		}
  	}
  	stringObj = stringObj.slice(0, stringObj.length - 1)
  	return '{' + stringObj + '}';
  }
};
```
