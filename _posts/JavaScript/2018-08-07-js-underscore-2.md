---
layout: post
title: "[Underscore.js] 02. Array Function"
subtitle:   "Underscore"
categories: javascript
tags: Underscore
comments: true
---

## Array Functions

1\. **first** _.first(array, [n])

 - 주어진 Array에서 첫 번째 원소를 리턴해주는 함수이다.
 - 만약 n이 주어진다면, 앞에서부터 n개의 원소를 리턴해준다.

 - first 함수 예재  
```javascript
_.first([1, 2, 3, 4, 5];
 => 1
_.first([1, 2, 3, 4, 5], 3);
 => [1, 2, 3]
```

 - first 함수 구현  
```javascript
_.first = function(array, n) {
  return n === undefined ? array[0] : array.slice(0, n);
};
// 만약, n이 주어지지 않았다면 array의 첫 원소를 리턴하고,
// n이 주어졌다면 처음부터 n개의 원소를 리턴해준다.
```

2\. **last** _.last(array, [n])

 - first함수를 반대로 생각하면 된다.
 - 즉, 주어진 Array에서 마지막 원소를 리턴하고, 만약 n이 주어진다면 뒤에서부터 n개의 원소를 리턴해준다.

 - last 함수 예재  
```javascript
_.last([1, 2, 3, 4, 5];
 => 5
_.last([1, 2, 3, 4, 5], 3);
 => [3, 4, 5]
```

 - last 함수 구현  
```javascript
_.last = function(array, n) {
  return n === undefined ? array[array.length - 1] : n > array.length ? array : array.slice(array.length - n)
};
// 만약, n이 주어지지 않았다면 array의 마지막 원소를 리턴하고,
// n이 주어졌다면 뒤에서 n번째 원소부터 마지막까지 리턴해준다.
// 하지만 slice 함수는 주어진 인자가 음수일 때, array의 마지막 원소를 -1로 인식하므로, n이 array의 길이보다 큰 경우는 예외처리를 해준다.
```

3\. **indexOf** _.indexOf(array, value, [isSorted])

 - array에서 value가 위치한 index 값을 반환해주고, 만약 array에 value가 없다면 -1을 반환하는 함수이다.
 - 만약 주어진 array가 오름차순으로 나열된 것을 알고 있다면 isSorted 값에 true를 대입하여 binary search(이진 탐색)가 적용되도록 할 수 있다.
 - 또한, isSorted에 숫자를 대입하면 해당 숫자는 array의 index로 인식되어 해당 index이후에 value와 일치하는 값을 찾아서 반환해준다.

 - indexOf 함수 예재  
```javascript
_.indexOf([1, 2, 3], 2);
=> 1
```

 - indexOf 함수 구현  
```javascript
_.indexOf = function(array, target) {
  var result = -1;
  _.each(array, function(item, index) {
    if (item === target && result === -1) {
      result = index;
    }
  });
  return result;
};
// indexOf는 loop를 돌며 주어진 value값에 일치하는 원소가 있는 지 찾아야 하기 때문에 each 함수를 적용하여 쉽게 구현할 수 있다.
// value값이 array에 없다면 -1을 반환해주기 때문에 초기값으로 -1을 설정한 뒤,
// 찾아야하는 value와 같은 값이 있다면 그 index값을 반환해주면 된다.
```

4\. **uniq** _.uniq(array, [isSorted], [iteratee])

 - 주어진 array에서 처음 등장하는 원소들만 array에 남겨 중복되는 element가 없도록 만드는 함수이다.
 - 만약 주어진 array가 순서대로 나열되어 있다면 isSorted 값에 true를 대입하여 더 빠른 결과를 낼 수 있다.
 - 또한, 각 원소를 변형하여 uniq를 판단하려면 변형하려는 함수를 iteratee에 대입해주면 된다.

 - uniq 함수 예재  
```javascript
_.uniq([1, 2, 1, 4, 1, 3]);
=> [1, 2, 4, 3]
```

 - uniq 함수 구현  
```javascript
_.uniq = function(array) {
  array = array.sort();
  var result = [];
  for (var i = 0; i < array.length; i++) {
    if (array[i] !== array[i+1]) {
      result.push(array[i]);
    }
  }
  return result;
};
// 주어진 array를 순서대로 나열하여 각 element가 같은 값인지 여부를 확인할 수 있도록 한다.
// for 문으로 각 element를 확인해보며, 인접한 두 element가 다를 경우 그 원소를 empty array에 push해 준다.
// uniq 함수 자체는 주어진 array에서 처음으로 등장하는 원소만 array에 남기지만, 구현하는 코드의 경우에는 가장 마지막 원소를 array에 push한다.
```
