---
layout: post
title: "[Underscore.js] Underscore library with ES6"
subtitle:   "Underscore"
categories: javascript
tags: Underscore
comments: true
---



```javascript
_.identity = (val) => val;
```
```javascript
_.first = (array, n) =>  n === undefined ? array[0] : array.slice(0, n)

_.last = (array, n) => n === undefined ? array[array.length - 1] : n === 0 ? [] : array.slice(-n)
```
```javascript
_.each = (collection, iterator) => {
  if (Array.isArray(collection)) {
    for (let i = 0; i < collection.length; i++) {
    iterator(collection[i], i, collection);
    }
  } else {
    for (let prop in collection) {
      iterator(collection[prop], prop, collection);
    }
  }
};
```
```javascript
_.indexOf = (array, target) => {
  let result = -1;

  _.each(array, (item, index) => {
    if (item === target && result === -1) {
      result = index;
    }
  });

  return result;
};
```
```javascript
_.filter = (collection, test) => {
  let filterredArr = [];

  _.each(collection, (value, element) => {
    if (test(value)) filterredArr.push(value);
  });

  return filterredArr;
};

_.reject = (collection, test) => (_.filter(collection, x => !test(x)))
```
```javascript
_.uniq = (array) => {
  let uniqueArr = [];
  array = array.sort();

  for (let i = 0; i < array.length; i++) {
    if (array[i] !== array[i+1]) uniqueArr.push(array[i]);
  }

  return uniqueArr;
};
```
```javascript
_.map = (collection, iterator) => {
  let mappedArr = [];

  _.each(collection, (value) => mappedArr.push(iterator(value)));

  return mappedArr;
};

_.pluck = (collection, key) => _.map(collection, (item) => item[key])
```
```javascript
_.reduce = (collection, iterator, accumulator) => {
  let isFirst = true;

  _.each(collection,(item,idx,arr)=>{
    if(accumulator===undefined&&isFirst){
      accumulator = item;
      isFirst = false;
    } else {
      accumulator=iterator(accumulator,item,idx,arr)
    }
  })

  return accumulator;
};
```
```javascript
_.contains = (collection, target) => _.reduce(collection, (wasFound, item)=> wasFound ? true : item === target ,false)
```
```javascript
_.every = (collection, iterator) =>
  _.reduce(collection, (isEvery, item) => {
    iterator = iterator || _.identity;
    return (!iterator(item)) ? false : isEvery;
  }, true)

_.some = (collection, iterator) =>
  _.reduce(collection, (isSome, item) => {
    iterator = iterator || _.identity;
    return (iterator(item)) ? true : isSome;
  }, false)
```
```javascript
_.extend = function(obj, ...arg) {
  let extendedObj = obj;

  for( let i = 0 ; i < arg.length ; i++){
    for( let prop in arg[i]){
      extendedObj[prop] = arg[i][prop]
    }
  }
	return extendedObj;
}

_.defaults = function(obj, ...arg) {
  let defaultObj = obj;

  for (let i = 1; i < arg.length; i++) {
    for (let prop in arguments[i]) {
      if (defaultObj[prop] === undefined) defaultObj[prop] = arguments[i][prop];
    }
  }

  return defaultObj;
};
```
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
```
```javascript
_.memoize = (func) => {
  let cache = {};

  return function(...arg) {
    if (!cache.hasOwnProperty(JSON.stringify(arg))) {
      cache[JSON.stringify(arg)] = func.apply(null, arg);
    }
    return cache[JSON.stringify(args)]
  }
};
```
```javascript
_.delay = (...args) => {
  setTimeout.apply(null, args);
};
```
```javascript
_.shuffle = (array) => {
  let shuffledArr = [];
  let randomIndex = Math.round(Math.random() * (array.length) + 1);

  for (let i = 0; i < array.length; i++) {
    shuffledArr.splice(randomIndex, 0, array[i]);
  }

  return shuffledArr;
};
```
```javascript
_.invoke = (collection, functionOrKey, args) => {
  if (typeof functionOrKey === 'function') {
    return _.map(collection, (element) => functionOrKey.call(element))
  } else if (typeof collection[0] === 'string') {
    return _.map(collection, (element) => String.prototype[functionOrKey].call(element))
  }
};
```
```javascript
_.sortBy = function(collection, iterator) {
  let temp;

  if (typeof iterator !== 'function') {
    if (typeof String.prototype[iterator] === 'function') {
      iterator = String.prototype[iterator].call(x);
    } else {
      iterator = (x) => x.length;
    }
  }

  for (let i = 0; i < collection.length; i++) {
    for (let j = i + 1; j < collection.length; j++) {
      if (String(iterator(collection[i])) > String(iterator(collection[j]))) {
        temp = collection[i];
        collection[i] = collection[j]
        collection[j] = temp
      }
    }
  }
  return collection
};
```
```javascript
_.zip = function(...arg) {
  let temp = _.map(arg,(item)=> item.length)
  const maxLength = Math.max.apply(null, temp);

  let zippedArr = [];
  for (var i = 0; i < maxLength; i++) {
    var innerArr = [];
    for (var j = 0; j < arguments.length; j++) {
      innerArr.push(arguments[j][i]);
    }
    zippedArr.push(innerArr);
  }

  return zippedArr;
};
```
```javascript
_.flatten = (nestedArray, result) => {
  result = result || [];

  for (var i = 0; i < nestedArray.length; i++) {
    if (Array.isArray(nestedArray[i])) {
      _.flatten(nestedArray[i], result);
    } else {
      result.push(nestedArray[i])
    }
  }

  return result;
};
```
```javascript
_.intersection = function(...arg) {
	let allElem = _.uniq(_.flatten(arg))

	return _.filter(allElem, (everyElem) => (_.every(arg, (argElem) => argElem.includes(everyItem))))
};

_.difference = function(array) {
  let arg = Array.prototype.slice.call(arguments,1)

  return _.filter(arguments[0],function(elem) {
    return !_.some(arg, function(argElem) {
      return argElem.includes(elem)
    })
  })
};
```
```javascript
_.throttle = (func, wait) => {
	var used = true;    // 함수가 호출될 때마다 계속 실행되는 것을 제한하는 Flag

	return () => {
		if (!used) {      // used가 false라면, 즉 함수가 실행된 적이 없다면, callback 함수를 실행
			func();
			used = true;    // callback 함수를 다시 실행할 수 없도록 제한하는 역할
		}
		setTimeout(() => {
			used = false;    // 일정시간이 경과하면 callback 함수를 다시 실행 가능하도록 조건을 변경
		}, wait);
	}
};
```
