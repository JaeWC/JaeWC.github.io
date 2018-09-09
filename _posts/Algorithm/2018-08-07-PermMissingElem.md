---
layout: post
title: "[codility 3-2] PermMissingElem"
subtitle:   "Algorithm"
categories: algorithm
tags: codility
comments: true
---

> [문제출처](https://app.codility.com/programmers/lessons/3-time_complexity/perm_missing_elem/)

## 문제

An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:
    function solution(A);
that, given an array A, returns the value of the missing element.

For example, given array A such that:
  A[0] = 2
  A[1] = 3
  A[2] = 1
  A[3] = 5
the function should return 4, as it is the missing element.

Assume that:
 * N is an integer within the range [0..100,000];
 * the elements of A are all distinct;
 * each element of array A is an integer within the range [1..(N + 1)].

Complexity:
 * expected worst-case time complexity is O(N);
 * expected worst-case space complexity is O(1) (not counting the storage required for input arguments).


## 풀이과정
* 1부터 N까지 연속된 숫자가 random한 배열로 주어진다. 이 때, 주어진 array는 하나의 'Missing Element'가 존재한다.
* 1부터 N까지 모든 수를 더한 값과, 주어진 Array(A)의 원소들을 모두 더한 값을 비교하면 그 차이가 Missing Element가 된다.
* JavaScript의 문법으로 인해 1부터 N까지의 합은 '가우스 연산'으로, A의 합은 reduce 메소드로 구할 수 있을 것이다.<br/>
  (Python은 sum()을 통해 쉽게 주어진 List의 합을 구할 수 있다.)

## 작성코드
- Detected time complexity: O(N) or O(N * log(N))

```javascript
function solution(A) {
    if (A.length === 0) {
        return 1;
    }
    return (((A.length + 2) * (A.length + 1)) / 2) - A.reduce(function(accumulator, currentvalue) {
        return accumulator+currentvalue;
    })
}
```
