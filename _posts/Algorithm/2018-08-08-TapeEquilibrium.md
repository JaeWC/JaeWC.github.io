---
layout: post
title: "[codility 3-3] TapeEquilibrium"
subtitle:   "Algorithm"
categories: algorithm
tags: codility
comments: true
---

> [문제출처](https://app.codility.com/programmers/lessons/3-time_complexity/tape_equilibrium/)

## 문제

A non-empty array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The difference between the two parts is the value of: \|(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])\|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.<br/>

For example, consider array A such that:

  A[0] = 3 <br/>
  A[1] = 1 <br/>
  A[2] = 2 <br/>
  A[3] = 4 <br/>
  A[4] = 3 <br/>
  
We can split this tape in four places:

 * P = 1, difference = \|3 − 10\| = 7 
 * P = 2, difference = \|4 − 9\| = 5 
 * P = 3, difference = \|6 − 7\| = 1 
 * P = 4, difference = \|10 − 3\| = 7 
 
Write a function:

function solution(A);

that, given a non-empty array A of N integers, returns the minimal difference that can be achieved.

For example, given:
  A[0] = 3
  A[1] = 1
  A[2] = 2
  A[3] = 4
  A[4] = 3
the function should return 1, as explained above.

Assume that:
 * N is an integer within the range [2..100,000];
 * each element of array A is an integer within the range [−1,000..1,000].

Complexity:
 * expected worst-case time complexity is O(N);
 * expected worst-case space complexity is O(N) (not counting the storage required for input arguments).


## 풀이과정
* N개의 element가 있는 array가 주어질 때, 특정한 기준점(문제에서는 P)을 기점으로 왼편에 있는 원소들의 합과 오른편의 원소들의 합의 차이를 구해야 한다.
* 왼쪽과 오른쪽 영역의 합을 구해서 그 차이의 절대값을 모두 비교하여 최소값을 구해야 하기 때문에 loop(for 문)를 돌게 된다.
* 최초 작성 코드는 for 문을 돌 때 마다 각 영역의 합을 구하는 연산을 처음부터 시행하게 되어 array의 크기가 커질 때 Timeout Error가 발생하였다.
* 따라서 최초에 왼쪽 영역은 0, 오른쪽 영역은 array의 전체 합이라 가정한뒤, for문을 돌면서 array의 각 원소를 더하고 빼주면서 그 차이를 비교해볼 수 있다.

## 작성코드
- Detected time complexity: O(N * N)
- Timeout Error

```javascript
function solution(A) {
    function difference(i) {
        return Math.abs(
            A.slice(i).reduce(function(accumulator, currentvalue) {
        return accumulator+currentvalue;
    }) - A.slice(0, i).reduce(function(accumulator, currentvalue) {
        return accumulator+currentvalue;
    }))
    }
    
    var minimalDifference = difference(1);
    
    for (var i = 2; i < A.length; i++) {
        if (difference(i) < minimalDifference) {
        minimalDifference = difference(i);
        }
    }
    return minimalDifference;
}
```

## 작성코드 Final
- Detected time complexity: O(N)

```javascript
function solution(A) {
    var sumLeft = 0;
    var sumRight = A.reduce(function(accum, curr) { return accum + curr; });
    var result = 100001;
    for (var i = 0; i < A.length - 1; i++) {
        sumLeft += A[i];
        sumRight -= A[i];
        var minDiff = Math.abs(sumLeft - sumRight);

        if (result > minDiff) {
            result = minDiff;
        }
    }
    return result;
}
```
