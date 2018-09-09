---
layout: post
title: "[Underscore.js] 01. underscore, Utility Function"
subtitle:   "Javascript"
categories: javascript
tags: Underscore
comments: true
---
# underscore.js란 무엇인가?
> JavaScript의 내장 객체들을 확장하지 않고, 다양한 함수형 프로그래밍을 지원할 수 있는 JavaScipt 라이브러리이다.
[underscore.js 공식 페이지](https://underscorejs.org/)  

## underscore.js는 5개의 그룹으로 100가지 이상의 함수를 정리하였다.
- Utility Functions
- Collection Functions(Arrays or Objects)
- Array Functions
- Object Functions
- Function(uh, ahem) Functions

## Utility Functions
1. **identity** _.identity(value)
- 인자 value와 같은 값을 리턴해주는 함수로 기본 iteratee 함수와 관련해서 사용할 때 매우 유용하다.

- identity 함수 예재  
```javascript
var fruits = {type : 'apple', origin : 'America'};
fruits === _.identity(fruits);
 => true
```

- identity 함수 구현  
```javascript
 _.identity = function(val) {
  return val;
};
// 인자로 들어가는 값을 똑같이 반환해주는 함수
```
