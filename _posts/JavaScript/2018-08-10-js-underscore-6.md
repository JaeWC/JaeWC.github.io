---
layout: post
title: "[Underscore.js] 06. underscore Advanced"
subtitle:   "Underscore"
categories: JS
tags: Underscore
comments: true
---

## Collection Functions

1\. **invoke** _.invoke(list, methodName, *arguments)

 - list의 원소들에 대하여 methodName으로 주어진 메소드를 호출하여 그 결과를 반환하는 함수이다.

 - invoke 함수 예재  
```javascript
_.invoke([[5, 1, 7], [3, 2, 1]], 'sort');
=> [[1, 5, 7], [1, 2, 3]]
```

 - invoke 함수 구현  
```javascript
_.invoke = function(collection, functionOrKey, args) {
  if (typeof functionOrKey === 'function') {
    return _.map(collection, function(element) {
      return functionOrKey.apply(element);
    })
  } else if (typeof collection[0] === 'string') {
    return _.map(collection, function(element) {
      return String.prototype[functionOrKey].apply(element);
    })
  } else if (Array.isArray(collection[0])) {
    return _.map(collection, function(element) {
      return Array.prototype[functionOrKey].apply(element);
    })
  } else {
    return _.map(collection, function(element) {
      return Object.prototype[functionOrKey].apply(element);
    })
  }
};
// methodName(구현 코드에서는 functionOrKey)이 내장 메소드일 수도 있고, 직접 구현한 함수일 수도 있다.
// 따라서, functionOrKey의 타입이 function인지 여부를 먼저 살펴본 뒤, 함수일 경우 각 원소의 반환값을 출력한다.
// 만약에 내장 메소드가 string 값으로 주어진 경우, 예를 들면 'sort'나 'toLowerCase'일 때는 prototype을 사용하여 해당 매소드를 적용할 수 있다.
// array로 감싸진 collection의 원소가 어떤 type인지에 따라 prototype도 달라지므로 이에 대한 구분이 필요하다.
```

## Array Functions

1\. **zip** _.zip(*arrays)

 - 주어진 array들의 값 중에서 같은 index 값을 갖는 값들을 하나로 합친 array들을 반환하는 함수이다.
 - 서로 다른 data set을 같은 index에 따라서 하나로 합쳐서 관리 및 가공할 경우에 유용한 함수이다.

 - zip 함수 예재  
```javascript
_.zip(['moe', 'larry', 'curly'], [30, 40, 50], [true, false, false]);
=> [["moe", 30, true], ["larry", 40, false], ["curly", 50, false]]
```

 - zip 함수 구현  
```javascript
_.zip = function() {
  var temArray = []
  for (var i = 0; i < arguments.length; i++) {
    temArray.push(arguments[i].length);
  }
  var maxLength = Math.max.apply(null, temArray);
  var zipped = [];
  for (var l = 0; l < maxLength; l++) {
    var innerArray = [];
    for (var i = 0; i < arguments.length; i++) {
      if (arguments[i][l] === undefined) {
        innerArray.push(undefined);
      } else {
        innerArray.push(arguments[i][l]);
      }
    }
    zipped.push(innerArray);
  }
  return zipped;
};
// zip 함수는 여러개의 array를 합쳐서 하나의 array로 만들되, 주어진 여러 array들을 합칠 때에는 같은 index에 해당하는 값들을 inner array로 묶어야 한다.
// 주어지는 array 값들의 길이가 모두 달라질 것이므로 해당하는 index에 맞는 값이 없을 경우에는 undefined를 추가해주면 된다.
// 따라서 우선은 임의의 빈 array를 만들어서 주어진 array들 중에서 가장 길이가 긴 array의 값을 찾아서 maxLength라는 변수로 정할 수 있다.
// 최종적으로 반환해주는 array를 zipped array로 만들어서 각 array들의 같은 index값을 zipped 안의 innerArray에 넣어주되,
// 길이가 달라서 값이 없는 경우에는 undefined를 넣어주면 된다.
```
<br/>
2\. **flatten** _.flatten(array, [shallow])

 - nested array 즉, 여러 층으로 만들어진 array를 하나의 층 즉, 하나의 array안에 포함시키는 함수이다.
 - 이 때, nested된 array의 정도는 중요하지 않으나 shallow에 true값이 부여되면, single level로 통일된다.

 - flatten 함수 예재  
```javascript
_.flatten([1, [2], [3, [[4]]]]);
=> [1, 2, 3, 4];  
_.flatten([1, [2], [3, [[4]]]], true);
=> [1, 2, 3, [[4]]];
```

 - flatten 함수 구현  
```javascript
_.flatten = function(nestedArray, result) {
  result = result || [];
  var idx = result.length;
  for (var i = 0; i < nestedArray.length; i++) {
    var value = nestedArray[i];
    if (Array.isArray(value)) {
      _.flatten(value, result);
    } else {
      result.push(value);
    }
  }
  return result;
};
// flatten 함수는 기본적으로 array의 첫번째 값 부터 확인하며 array가 아닌 값인 경우에만 새로운 배열에 추가시키고,
// 확인하는 값이 배열이라면 다시 그 배열의 원소를 찾아가면서 값으로만 구성된 것을 새로운 배열에 추가해야 한다.
// 이 때, 계속 확인하게 되는 값은 배열 속의 배열이 반복되는 것이기 때문에 recursion 즉, 재귀를 사용하여 확인해볼 수 있다.
// 추가적으로 값을 추가하게되는 result 값은 재귀를 하면서 기존의 값에 새로운 값을 추가해야 한다.
// 그렇기 때문에 최초 push가 가능하도록 빈 array를 설정하고, 그 이후로는 result 값을 가져올 수 있도록 한다.
```
<br/>
3\. **intersection** _.intersection(*arrays)

 - 주어진 array들에서 원소들이 공통으로 존재하는 원소들을 출력하는 함수이다. 즉, 교집합을 반환해준다.

 - intersection 함수 예재  
```javascript
_.intersection([1, 2, 3], [101, 2, 1, 10], [2, 1]);
=> [1, 2]
```

 - intersection 함수 구현  
```javascript
_.intersection = function() {
  var resultArray = [];
  var firstLength = arguments[0].length;
  for (var j = 0; j < firstLength; j++) {
    for (var i = 1; i < arguments.length; i++) {
      var temp = false;
      if (_.contains(arguments[i], arguments[0][j])) {
        temp = true;
      }
    } if (temp) {
      resultArray.push(arguments[0][j]);
    }
  }
  return resultArray;
};
// 주어진 array들 중에서 첫번째 array의 값이 다른 array에 포함되었는 지 확인하고, 포함된 경우 결과값으로 출력할 array에 추가하면 된다.
// 모든 array에 공통적으로 있는 값을 찾아야 하기 때문에 임의로 첫번째 array의 길이만큼만 검토해보면 된다.
// contains 함수로 2번쨰 이후의 array에 특정 값이 있는지 확인하면 되고, 특정 값이 있어서 true가 반환될 경우 temp라는 임의의 변수를 true로 바꾼다.
// 모든 array를 확인하며 temp가 true로 반환되는 경우에만 결과로 출력해주면 된다.
```
<br/>
4\. **difference** _.difference(arrays, *others)

 - 첫번째로 주어진 arrays 중에서 다른 array에는 없는 값 만을 반환해주는 함수이다.

 - difference 함수 예재  
```javascript
_.difference([1, 2, 3, 4, 5], [5, 2, 10]);
=> [1, 3, 4]
```

 - difference 함수 구현  
```javascript
_.difference = function(array) {
  var firstLength = arguments[0].length;
  for (var j = 0; j < firstLength; j++) {
    for (var i = 1; i < arguments.length; i++) {
      var temp = false;
      if (_.contains(arguments[i], arguments[0][j])) {
        temp = true;
        break;
      }
    } if (temp) {
      arguments[0][j] = undefined;
    }
  }
  return _.filter(arguments[0], function(elem) {
    return elem !== undefined;
  });
};
// 기본적인 함수 구현 알고리즘은 intersection 함수와 유사하다.
// intersection 함수는 공통적으로 포함된 값들을 출력했다면, difference 함수는 첫번째 array의 원소 중에서 다른 array 내에 있는 원소는 제외해야 한다.
// 따라서 한번이라도 contains 함수에 true가 출력되는 경우엔 break로 loop를 정지시켜 해당 원소를 undefined로 만들어준 뒤 filter를 하면 된다.
// undefined로 바꿔주는 이유는 첫번쨰 array의 index값을 돌면서 포함 여부를 찾고 있기에 index값의 혼란을 없애기 위한 과정이다.
```
<br/>
