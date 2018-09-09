---
layout: post
title: "[Underscore.js] 03. Collection Function"
subtitle:   "Underscore"
categories: javascript
tags: Underscore
comments: true
---

## Collection Functions

1\. **each** _.each(list, iteratee, [context])

 - list의 각 원소들을 반복하여 iteratee함수에 대입하여 그 결과값을 반환해주는 함수이다.
 - list: collection으로써, 배열이나 객체가 될 수 있다.
 - iteratee: iteratee 함수는 (element, index, list)를 인자로 받지만, list가 object로 주어질 경우에는 (value, key, list)를 받게된다.
 - 만약 context가 주어진다면 iteratee 함수는 context 객체에 binding 된다.(이는 iteratee 함수에 있는 this로 바인딩 되는 것)

 - each 함수 예재  
```javascript
_.each([1, 2, 3], function(element, index) {
  var result = 'Element: ' + element + ', Index: ' + index;
  console.log(result);
  });
// Element: 1, Index: 0
// Element: 2, Index: 1
// Element: 3, Index: 3
_.each({One: 1, Two: 2, Three: 3}, function(value, key) {
  var result = ‘The value is ‘+ value + ‘ where the key is ‘ + key;
  console.log(result);
  });
// The value is 1 where the key is One
// The value is 2 where the key is Two
// The value is 3 where the key is Three
```

 - each 함수 구현  
```javascript
_.each = function(collection, iterator) {
  if (Array.isArray(collection)) {
    for (var i = 0; i < collection.length; i++) {
      iterator(collection[i], i, collection);
    }
  } else {
    for (var i in collection) {
      iterator(collection[i], i, collection);
    }
  }
};
// each 함수는 collection이 array인지 object인지에 따라 iteratee 함수에 다른 argument를 대입시켜야 하기 때문에
// each 함수를 직접 구현할 때에도 collection이 array인지 object인지 구분해서 인자를 대입해줘야 한다.
```
<br/>
2\. **filter** _.filter(list, predicate, [context])

 - list의 원소 중에서 predicate함수의 truth 테스트를 통과한 원소들만 반환해주는 함수이다
 - predicate: list의 각 element에 대하여 그 결과값이 true인지, false인지 확인하는 일종의 test함수이다.
 - 만약 context가 주어진다면 iteratee 함수는 context 객체에 binding 된다.(이는 iteratee 함수에 있는 this로 바인딩 되는 것)

 - filter 함수 예재  
```javascript
_.filter({a:1, b:2, c:3, d:4}, function(num){ return num % 2 == 0; });
 => [2, 4]
_.filter([0,1,2,3], function(item) { return this[item] % 5 == 0 ;}, [5, 7, 10, 15])
 => [0, 2, 3]
```

 - filter 함수 구현  
```javascript
_.filter = function(collection, test) {
  var result = [];
  _.each(collection, function(element) {
    if(test(element)) {
      result.push(element);
    }
  });
  return result;
};
// 최종 결과값은 array로 반환되기 때문에 새로운 result 값으로 empty array를 선언해준 뒤,
// each함수로 collection의 원소가 test함수에 대입되어 true를 반환하는 경우에만 새로운 array에 push해준다.
```
<br/>
3\. **reject** _.reject(list, predicate, [context])

 - filter 함수를 반대로 생각하면 된다. 즉, predicate 함수에서 false를 반환해주는 원소들만 반환해주는 함수이다.

 - filter 함수 예재  
```javascript
_.reject({a:1, b:2, c:3, d:4}, function(num){ return num % 2 == 0; });
 => [1, 3]
_.reject([0,1,2,3], function(item) { return this[item] % 5 == 0 ;}, [5, 7, 10, 15])
 => [1]
```

 - filter 함수 구현  
```javascript
_.reject = function(collection, test) {
  var result = [];
  _.each(collection, function(element) {
    if(!test(element)) {
      result.push(element);
    }
  });
  return result;
};
// test함수에서 false를 반환하는 경우에만 새로운 array에 push해주는 것으로 filter 구현 함수를 수정하면 된다.
```
<br/>
4\. **map** _.map(list, iteratee, [context])

 - list의 모든 원소들을 iteratee함수에 대입하여 반환된 값들로 구성된 새로운 array를 만드는 함수이다.
 - iteratee 함수는 element(or value), index(or key), list의 3가지 인자를 받는다.

 - map 함수 예재  
```javascript
_.map({one: 1, two: 2, three: 3}, function(num, key){ return num * 3; });
 => [3, 6, 9]
_.map([0,1,2,3], function(item) { return this[item] * 3 ;}, [5, 7, 10, 15]);
 => [15, 21, 30, 45]
```

 - map 함수 구현  
```javascript
_.map = function(collection, iterator) {
  var result = [];
  _.each(collection, function(item, index, collection) {
    result.push(iterator(item));
  })
  return result;
};
// 주어진 collection의 모든 원소들을 iterator에 대입하여 반환된 값을 새로 선언한 result array에 push해 줄 수 있다.
// map 함수는 새로운 array를 만들고, 새로운 array의 원소는 기존의 list에서 element(or value)인 값들 이기에 iterator가 첫 번째 item 인자만 받아도 된다.
```
<br/>
5\. **pluck** _.pluck(list, propertyName)

 - list에서 propertyName이 가지고 있는 모든 value 값을 반환해주는 함수이다.

 - pluck 함수 예재  
```javascript
var stooges = [{name: 'moe', age: 40}, {name: 'larry', age: 50}, {name: 'curly', age: 60}];
_.pluck(stooges, 'name');
=> ["moe", "larry", "curly"]
var stooges = {'first': {name: 'moe', age: 40}, 'second': {name: 'larry', age: 50}, 'third': {name: 'curly', age: 60}};
_.pluck(stooges, 'name');
=> ["moe", "larry", "curly"]
```

 - pluck 함수 구현  
```javascript
_.pluck = function(collection, key) {
  return _.map(collection, function(item) {
    return item[key];
  });
};
// 주어진 collection의 각 원소들에 대하여 찾고자하는 key값에 대응하는 value를 찾기 위하여 item[key]를 리턴해준다.
// underscore 페이지의 설명에 따르면, pluck함수는 map함수의 흔한 예시라고 한다.
```
<br/>
6\. **reduce** _.reduce(list, iteratee, [memo], [context])

 - list의 각 원소들을 iteratee 함수에 대입하여 하나의 값을 리턴해주는 함수이다.
 - memo: iteratee 함수의 초기 값을 의미하는 인자로 생략 가능하다.
 - iteratee 함수는 memo, element(or value), index(or key), list를 인자로 받게 된다.
 - memo가 생략된 경우에는 list의 첫번째 원소가 memo로 사용되지만, memo가 입력된 경우에는 입력된 memo를 사용하게 된다. 

 - reduce 함수 예재  
```javascript
var sum = _.reduce([1, 2, 3], function(memo, num){ return memo + num; }, 0);
=> 6
var sum = _.reduce([1, 2, 3, 4], function(memo, num){ return memo + num; });
=> 10
```

 - reduce 함수 구현  
```javascript
_.reduce = function(collection, iterator, accumulator) {
  if (accumulator === undefined) {
    accumulator = collection[0];
    for (var i = 1; i < collection.length; i++) {
      accumulator = iterator(accumulator, collection[i]);
    }
  } else {
    for (var i = 0; i < collection.length; i++) {
      accumulator = iterator(accumulator, collection[i]);
    }
  }
  return accumulator;
};
// accumulator 즉, 초기값(memo)이 주어진 경우와 생략된 경우로 나누어서 구현 함수를 작성해야 한다.
// 함수 자체에 초기값 인자가 주어지지 않았다면, collection의 첫번째 원소가 초기값이 되고 iterator함수는 collection의 2번째 원소부터 인자로 받게 된다.
// 만약 초기값이 주어졌다면, iterator함수는 collection의 첫번째 원소부터 인자로 받게 된다.
```
<br/>
7\. **contains** _.contains(list, value, [fromIndex])

 - list안에 value가 있는지 여부를 확인하는 함수이다. 만약 value가 있으면 true를 리턴한다.
 - fromIndex가 주어진다면, value가 있는지 찾기 시작하는 기준 index가 된다.

 - contains 함수 예재  
```javascript
_.contains([1, 2, 3], 3);
=> true
```

 - contains 함수 구현  
```javascript
_.contains = function(collection, target) {
  collection = Object.values(collection);
  return _.reduce(collection, function(wasFound, item) {
    if (wasFound) {
      return true;
    }
    return item === target;
  }, false);
};
// array의 경우에도 Object.values() 메소드가 value를 반환해주기 때문에 array와 object를 나누어서 구현할 이유가 사라졌다.
// contains 함수는 결과적으로 collection에 target 원소가 있으면 true, 없으면 false의 하나의 값 만을 반환하기 때문에 reduce함수로 각 원소를 확인할 수 있다.
// reduce함수를 적용하여, 각 원소를 하나씩 돌아가면서 만약 target 원소가 있으면 return으로 바꿔주고, 일치하는 값이 없으면 초기값인 false를 반환한다.
```
<br/>
8\. **every** _.every(list, [predicate], [context])

 - list의 모든 원소들이 predicate함수의 truth 테스트를 통과할 경우에만 true를 반환하는 함수이다.
 - 만약에 확인하는 원소들 중에서 predicate 함수를 통과하지 못하는 경우, 그 즉시 false를 반환해준다.

 - every 함수 예재  
```javascript
_.every([2, 4, 5], function(num) { return num % 2 == 0; });
=> false
```

 - every 함수 구현  
```javascript
_.every = function(collection, iterator) {
  var testFunc = iterator || _.identity;
  return _.reduce(collection, function(checks, item) {
    if (checks === false) {
      return false;
    } else if (testFunc(item)) {
      checks = true;
    } else {
      checks = false;
    }
  return checks;
  }, true)
};
// iterator가 주어지는 경우와 주어지지 않는 경우(iteratee가 적용됨)가 있기 때문에 새로운 testFunc를 선언하여 각 원소의 true/fase를 확인한다.
// reduce 함수를 시행하여 초기값을 true로 설정한 뒤에 원소가 false인 경우를 발견하면 바로 false를 반환해줄 수 있도록 한다.
// 즉, 최우선적으로 checks 값에 false가 들어가면 every 함수가 false를 리턴해줄 수 있도록 하고,
// checks 값이 true라면 각 원소를 testFunc에 대입하여 checks 값을 판단해주면 된다.
```
<br/>
9\. **some** _.some(list, [predicate], [context])

 - list의 모든 원소들이 predicate함수의 truth 테스트를 모두 통과하지 못는 경우에만 false를 반환하는 함수이다.

 - some 함수 예재  
```javascript
_.some([2, 4, 5], function(num) { return num % 2 == 0; });
=> true
```

 - some 함수 구현  
```javascript
_.some = function(collection, iterator) {
  var testFunc = iterator || _.identity;
  return _.reduce(collection, function(checks, item) {
    if (checks === true) {
      return true;
    } else if (!testFunc(item)) {
      checks = flase;
    } else {
      checks = true;
    }
  return checks;
  }, false)
};
// reduce 함수를 시행하여 초기값을 false로 설정한 뒤에 원소가 true인 경우를 발견하면 바로 true를 반환하도록 every를 수정한다.
```
<br/>
10\. **shuffle** _.shuffle(list)

 - 주어진 list를 임의로 섞은 새로운 list를 반환하는 함수이다. 이때 임의로 섞는 방식은 'Fisher-Yates shuffle'(https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)을 이용한다.

 - shuffle 함수 예재  
```javascript
_.shuffle([1, 2, 3, 4, 5, 6]);
=> [4, 1, 6, 3, 5, 2]
```

 - shuffle 함수 구현  
```javascript
_.shuffle = function(array) {
  var randomIndex = Math.floor(Math.random() * array.length);
  var shuffledArray = [];
  for (var i = 0; i < array.length; i++) {
    shuffledArray.splice(randomIndex, 0, array[i])
  }
  return shuffledArray;
};
// shuffle 함수는 기존의 array를 임의로 섞어야 하기 때문에 임의의 index 값을 지정해줄 수 있도록 정수인 난수를 생성한다.
// 처음부터 randomIndex의 최대값을 array의 길이만큼 정했기 때문에 for loop을 돌면서도 사용할 수 있다.
// 기존의 array에서 순서대로 원소를 불러올 때, 새로운 array의 임의의 인덱스를 지정하여 값을 할당할 수 있다.
// splice메소드는 지정한 index 값이 주어진 array의 length보다 클 경우 가장 마지막에 원소를 배치하기 때문에 난수의 값이 길이보다 커지는 것은 문제없어진다.
```
