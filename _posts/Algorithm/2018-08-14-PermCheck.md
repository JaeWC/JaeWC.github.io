---
layout: post
title: "[codility 4-1] PermCheck"
subtitle:   "Algorithm"
categories: algorithm
tags: codility
comments: true
---

> [문제출처](https://app.codility.com/programmers/lessons/4-counting_elements/perm_check/)

## 문제
A non-empty array A consisting of N integers is given.

A permutation is a sequence containing each element from 1 to N once, and only once.

For example, array A such that:
 *   A[0] = 4 <br/>
 *   A[1] = 1 <br/>
 *   A[2] = 3 <br/>
 *   A[3] = 2 <br/>
is a permutation, but array A such that:
 *   A[0] = 4 <br/>
 *   A[1] = 1 <br/>
 *   A[2] = 3 <br/>
is not a permutation, because value 2 is missing.
The goal is to check whether array A is a permutation.

Write a function:
**function solution(A);**
that, given an array A, returns 1 if array A is a permutation and 0 if it is not.

For example, given array A such that:
 *   A[0] = 4 <br/>
 *   A[1] = 1 <br/>
 *   A[2] = 3 <br/>
 *   A[3] = 2 <br/>
the function should return 1.

Given array A such that:
 *   A[0] = 4 <br/>
 *   A[1] = 1 <br/>
 *   A[2] = 3 <br/>
the function should return 0.

Assume that:
 * N is an integer within the range [1..100,000];
 * each element of array A is an integer within the range [1..1,000,000,000].

Complexity:
 * expected worst-case time complexity is O(N);
 * expected worst-case space complexity is O(N) (not counting the storage required for input arguments).


## 풀이과정
* 

## 작성코드
- Detected time complexity: O(N) or O(N * log(N))

```javascript
function solution(A) {
    var len = A.length;
    var sum = (N * (N+1)) / 2;
    var cnt = [];
    for (var i in A) {
        sum -= A[i];
        if (tap[A[i]]) {
            return 0;
        }
        tap[A[i]] = true;
    }
    return +(sum==0);
}
```

## 작성코드 Final
- Detected time complexity: O(N) or O(N * log(N))

```javascript
function solution(A) {
    var cnt = [];
    var len = A.length;
    for (var i=0; i<len;i++) {
        cnt[i] = 0;   
    }
    for (var i=0; i<len;i++) {
        if (A[i] == 0 || A[i] > len) 
            return 0;       
        cnt[A[i]-1]++;         
        if(cnt[A[i]-1] > 1) 
            return 0;
    }
    return 1;
}
```
