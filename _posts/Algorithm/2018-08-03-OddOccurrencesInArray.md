---
layout: post
title: "[codility 2-2] OddOccurrencesInArray"
subtitle:   "Algorithm"
categories: algorithm
tags: codility
comments: true
---

> [문제출처](https://app.codility.com/programmers/lessons/2-arrays/odd_occurrences_in_array/)

## 문제

A non-empty zero-indexed array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9
the elements at indexes 0 and 2 have value 9,
the elements at indexes 1 and 3 have value 3,
the elements at indexes 4 and 6 have value 9,
the element at index 5 has value 7 and is unpaired.
Write a function:

def solution(A)

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9
  A[3] = 3  A[4] = 9  A[5] = 7
  A[6] = 9
the function should return 7, as explained in the example above.

Assume that:

N is an odd integer within the range [1..1,000,000];
each element of array A is an integer within the range [1..1,000,000,000];
all but one of the values in A occur an even number of times.
Complexity:

expected worst-case time complexity is O(N);
expected worst-case space complexity is O(1),

beyond input storage (not counting the storage required for input arguments).
Elements of input arrays can be modified.


## 풀이과정
① 주어진 Array의 길이에 따라 결과값이 달라질 수 있다.
② 주어진 Array에는 Number type의 원소들이 주어질 것이다. 따라서 원소들을 오름차순으로 정렬하여 비교할 것이다.

## 작성코드

```javascript
function solution(A) {
    if (A.length === 1) {
        return A[0];
    }
    A.sort()
    for (var i = 0; i < A.length; i+=2) {
        if (A[i] !== A[i+1]) {
            return A[i]
        }
    }
}
```
