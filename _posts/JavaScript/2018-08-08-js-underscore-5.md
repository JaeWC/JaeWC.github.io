---
layout: post
title: "[Underscore.js] 05. Function Functions"
subtitle:   "Underscore"
categories: javascript
tags: Underscore
comments: true
---

## Function Functions

1\. **once** _.once(function)

 - 인자로 받은 함수가 오직 한 번만 호출되도록 만드는 역할을 하는 것으로 반복적인 호출은 아무 영향이 없고, 최초의 호출에 해당하는 값을 반환한다.
 - 초기 설정을 하는데에 유용한 함수이다.

 - once 함수 예재  
```javascript
var initialize = _.once(createApplication);
initialize();
initialize();
// Application is only created once.
```

 - once 함수 구현  
```javascript
_.once = function(func) {
  var alreadyCalled = false;
  var result;
  return function() {
    if (!alreadyCalled) {
      result = func.apply(this, arguments);
      alreadyCalled = true;
    }
    return result;
  };
};
// alreadtCalled 변수와 result 변수는 익명함수 function()에 의해 호출될 수 있는 Local Variables이다.
// 함수가 호출된 적이 있는 지 여부를 우선 확인해야 되고, 만약 호출된 적이 있었다면(alreadyCalled = true;) 그 때 함수의 return 값을 반환해야 한다.
// .apply()는 Function 메소드로 주어진 this와 arguments로 함수를 호출한다. 
// 여기서는 인자로 어떤 값이 들어갈지 모르는 구현함수이기에 apply 메소드에 arguments를 대입하는 것이 적절하다.
```
<br/>
2\. **memoize** _.memoize(function, [hasFunction])

 - 한번 연산된 결과를 캐시해두어 이후에 호출하는 함수로 속도 및 성능을 향상시킬 수 있다.

 - memoize 함수 예재  
```javascript
var fibonacci = _.memoize(function(n) {
  return n < 2 ? n: fibonacci(n - 1) + fibonacci(n - 2);
});
```

 - memoize 함수 구현  
```javascript
  _.memoize = function(func) {
    var cache = {};
  
    return function() {
      if (!cache.hasOwnProperty(JSON.stringify(arguments))) {
        cache[JSON.stringify(arguments)] = func.apply(null, arguments);
      } 
      return cache[JSON.stringify(arguments)];
    }
  };
// 우선, memoize 함수가 이미 호출한 적이 있는 값을 cache해 두는 object가 필요하다.
// array가 아닌 object인 이유는 함수에 입력한 인자를 기준으로 cache된 value가 있는 지 여부를 파악하는 것이기 때문에 key: value의 구조가 요구된다.
// memoize 구현함수에서 func 함수에 어떤 값이 들어갈 것인지 미리 알 수가 없기 때문에 arguments 키워드를 사용해야 한다.
// cache object의 key 값 중에서 arguments가 있는 지 찾아보고 key값에 없다면 그 arguments와 func 함수의 결과를 cache에 저장해야 한다.
// 중요한 것은 object의 key값을 arguments로 접근하기 위해서는 arguments를 string값으로 만들어서 접근해야 하기에 JSON.stringfy()를 사용해야 한다.
// 또한, func 함수에 들어가는 인자는 arguments이므로, .apply() 메소드에서 첫번째 값으로 null을 입력해도 무방하다.
```
<br/>
3\. **delay** _.delay(function, wait, *arguments)

 - setTimeout과 같이 wait 밀리초(1000분의 1초) 뒤에 function함수를 시행한다.

 - once 함수 예재  
```javascript
var log = _.bind(console.log, console);
_.delay(log, 1000, 'logged later');
=> 'logged later' // Appears after one second.
```

 - once 함수 구현  
```javascript
_.delay = function(func, wait) {
  var args = Array.prototype.slice.call(arguments, 2);
  return setTimeout(function() {
    func.apply(null, args);
  }, wait);
};
// 실행되어야 하는 function의 인자는 wait parameter뒤에 즉, delay 함수에서 3번째 index 이후에 부여된다.
// 따라서 arguments를 실제의 array로 변환시켜줄 때, 2번째 이후부터 slice하도록 설정한다.
// delay 함수에서 반환되어야 하는 것은 setTimeout으로 func 함수에 args를 인자로 넣어 반환값을 얻을 수 있다.
```
<br/>
