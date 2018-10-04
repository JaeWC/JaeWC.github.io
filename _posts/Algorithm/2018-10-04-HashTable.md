---
layout: post
title: "[What is Algorithm] What is Hash Table"
subtitle:   "Algorithm"
categories: algorithm
tags: understanding algorithm
comments: true
---


## Hash Function

Hash Function(해시 함수)은 문자열(임의의 데이터 즉, 바이트 열)을 받아서 숫자로 반환하는 함수이다. 해시 함수는 문자열에 대해 숫자를 할당(mapping)한다. 

문자열을 넣었을 때 나오는 반환값에 특정한 패턴이 보이지 않는 것 같지만, Hash Function은 다음의 요건을  갖춰야 한다.

- 일관성이 있어야 한다.
- 다른 문자열은 다른 숫자를 반환해야 한다.

해시 함수는 특정 데이터가 저장된 위치를 정확하게 알려주는 도구(Helper Function)로 탐색을 할 필요가 없다.

- 단, 해시 함수는 주어진 배열이 얼마나 큰지 알고 있어야 한다.



## Hash Table

Hash Function과 Array를 합치면 Hash Table이라는 자료구조를 얻을 수 있다. 해시 테이블은 자료구조 그 자체 외에도 해시 함수라는 추가적인 논리구조를 갖는 Data Structure이다.([What is Hash Table](https://github.com/JaeWC/TIL/blob/master/Algorithm/%5BDataStructure%5D%20What%20is%20Hash%20table.md))

Array와 Linked List는 직접 메모리를 할당하여 데이터를 저장하지만, 해시 테이블은 해시 함수를 사용해서 보다 효율적으로 원소를 관리한다.



#### Using Hash Table as a Cache

Caching은 작업 속도를 올리는 일반적인 방법으로 모든 대형 웹 사이트는 캐싱을 사용한다. 또한 그 자료는 해시 테이블에 저장된다.

따라서 일반적으로 특정 웹에 접속할 때, 해시 테이블에 저장된 페이지가 있는지 여부를 확인해서 있을 경우 해시 테이블의 내용을 빠르게 전송해주며, 없을 때는 서버가 작업을 해서 결과를 보여준다.

```javascript
cache = {};

function get_page(url) {
    if (cache.hasOwnproperty(url)) {
        return cache[url]
    } else {
        data = get_data_from_server(url);
        cache[url] = data;
        return data;
    }
} 
```

위의 코드와 같은 방법으로 해시 테이블이 캐시 상황에서 작동한다.