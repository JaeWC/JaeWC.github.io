---
layout: post
title: "[codility 4-2] FrogRiverOne"
subtitle:   "Algorithm"
categories: algorithm
tags: codility
comments: true
---

> [문제출처](https://app.codility.com/programmers/lessons/4-counting_elements/frog_river_one/)

## 문제
A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given an array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, we want to find the earliest moment when all the positions from 1 to X are covered by leaves). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:
  A[0] = 1<br/>
  A[1] = 3<br/>
  A[2] = 1<br/>
  A[3] = 4<br/>
  A[4] = 2<br/>
  A[5] = 3<br/>
  A[6] = 5<br/>
  A[7] = 4<br/>
In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:
**function solution(X, A);**
that, given a non-empty array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

For example, given X = 5 and array A such that:
  A[0] = 1<br/>
  A[1] = 3<br/>
  A[2] = 1<br/>
  A[3] = 4<br/>
  A[4] = 2<br/>
  A[5] = 3<br/>
  A[6] = 5<br/>
  A[7] = 4<br/>
the function should return 6, as explained above.

Assume that:
* N and X are integers within the range [1..100,000];
* each element of array A is an integer within the range [1..X].

Complexity:
* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(X) (not counting the storage required for input arguments).

## 풀이과정
* Frog는 목표지점(X+1)까지 도달해야 한다. Array A의 각 element는 K초에 떨어지는 낙옆의 개수로, 낙옆에 최종적으로 X까지 떨어져야 Frog는 목표지점으로 도달할 수 있다.
* X까지의 합과 배열 A의 중복되지 않는 원소들의 합이 같은 경우 목표지점에 도달할 수 있다. 이때 두개의 합이 같아지게 하는 마지막 index 값을 return 해줘야 한다.
* 필요한 것은 index 값이므로 Array이지만 for ... in 문을 사용하여, Array의 각 element가 중복지 않은 원소 만을 갖는 새로운 빈 배열에 있는 지 체크한다.
* 이 과정을 반복하며 빈 배열에는 새로운 원소들을 추가해주면서 동시에 Array의 합을 구해가며 목표지점까지의 합과 비교한다.

## 작성코드
- Detected time complexity: O(N)

```javascript
function solution(A) {
  var sumArray = 0;
  var goal = (X * (X + 1)) / 2;
  var leaveLocated = [];
  
  for (var i in A) {
    if (!leaveLocated[A[i]]) {
      leaveLocated[A[i]] = true;
      sumArray += A[i];
      
      if (sumArray === expected) {
        return Number(i);
      }
    }
  }
  return -1;
}
```
