---
layout: post
title: "[recursion] 01. getElementsByClassName"
subtitle:   "Recursion"
categories: JS
tags: Recursion
comments: true
---

## Recursion

1\. **getElementsByClassName** 

 - DOM 구조에서 특정 ClassName을 전부 반환해주는 함수이다.
 - DOM은 tree구조를 갖고있기 때문에 DOM의 상위 element에서 ClassName을 찾아본 뒤, 하위 element에서 동일한 작업을 반복해야 햔다.
 - 즉, recursion의 방식으로 이 과정을 반복할 수 있다.

 - getElementsByClassName 구현 아이디어  
> - **document.body** : DOM 구조의 최상단은 HTML 자체이며, 그 하단은 <head>와 <body> 태그이기 때문에 body 태그의 내용부터 확인하는 작업이 필요하다.
> - **Element.classList** : 특정 element에 class list가 있는지 확인해준다. 즉, 결과값은 true or false를 반환해준다.
> - **Element.classList.contains()** : element의 class list가 있을 경우, 특정 ClassName을 포함하고 있는 지 여부를 반환해준다.
> - **element.hasChildNodes()** : 특정 element에 ChildNode가 있는지를 확인해주는 함수이다.
> - **element.children** : 특정 element의 children element들을 전부 반환해주는 것으로, recursion을 시행할 때의 인자로 보면 된다.

 - getElementsByClassName 함수 구현  
```javascript
var getElementsByClassName = function(className) {
  var classList = [];
  var bodyElem = document.body;
  var findingElements = function(element) {
  	if (element.classList && element.classList.contains(className)) {
  		classList.push(element);
  	}
  	if (element.hasChildNodes()) {
  		var childElem = element.children;
  		for (var i=0; i < childElem.length; i++) {
  			findingElements(childElem[i]);
  		}
  	}
  };
  findingElements(bodyElem);
  return classList;
};
```
