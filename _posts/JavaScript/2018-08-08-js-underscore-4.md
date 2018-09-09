---
layout: post
title: "[Underscore.js] 04. Object Function"
subtitle:   "Underscore"
categories: JS
tags: Underscore
comments: true
---

## Object Functions

1\. **extend** _.extend(destination, *sources)

 - source 객체의 모든 property를 참조하여 destination 객체에 추가하는 함수로 최종적으로 destination 객체를 반환한다.
 - 이 때 source object의 property를 복제하는 것이 아니고, 단순히 참조(shallowly copy, copy by reference)한다.
 - 만약에 중복되는 key값이 있다면, 맨 뒤에 나오는 value값이 해당 key의 value를 대체한다.

 - extend 함수 예재  
```javascript
_.extend({name: 'moe'}, {age: 50});
=> {name: 'moe', age: 50}
_.extend({ x: 'x' }, { a: 'a', x: 2 }, { a: 1 });
=> { x: 2, a: 1 }
```

 - extend 함수 구현  
```javascript
_.extend = function(obj) {
  for (var i = 1; i < arguments.length; i++) {   
    for (var key in arguments[i]) {
      obj[key] = arguments[i][key];
    }
  }
  return obj;
};
// extend 함수의 인자로는 여러개의 object가 들어갈 수 있다. 따라서 이 경우에는 arguments 키워드를 통해 각 object를 검토할 수 있다.
// arguments의 두번째 원소(index = 1)의 key와 value값들을 obj에 입력하여 구현할 수 있다.
```
<br/>
2\. **defaults** _.defaults(object, *defaults)

 - extend 함수와 유사하게 defaults object의 property를 object에 대입하지만, 기존에 object의 key에 해당하는 value를 유지한다.

 - defaults 함수 예재  
```javascript
_.defaults({ x: 'x' }, { a: 'a', x: 2 }, { a: 1 });
=> { x: 'x', a: 'a' }
_.defaults({flavor: "chocolate"}, {flavor: "vanilla", sprinkles: "lots"});
=> {flavor: "chocolate", sprinkles: "lots"}
```

 - defaults 함수 구현  
```javascript
  _.defaults = function(obj) {
    for (var i = 1; i < arguments.length; i++) {   
      for (var key in arguments[i]) {
        if (obj[key] === undefined ) {
          obj[key] = arguments[i][key];
        }
      }
    }
    return obj;
  };
// 기본적은 구현 원리는 defaults와 동일하지만, 처음으로 나오는 key와 value는 유지하고, 새로 등장하는 key와 value를 추가해야한다.
// 따라서 뒤이어 나오는 object들의 key가 obj에 없는 경우에만 해당 key와 value를 추가해주면 된다.
```
<br/>
