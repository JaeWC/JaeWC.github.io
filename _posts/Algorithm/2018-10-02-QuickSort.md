---
layout: post
title: "[What is Algorithm] What is Quick Sort"
subtitle:   "Algorithm"
categories: algorithm
tags: understanding algorithm
comments: true
---

Divide and Conquer Strategy는 문제를 해결하는 새로운 사고 방식으로 새로운 문제를 풀어낼 수 있는 한가지 방법이 될 수 있다. Quick-sort는 분할 정복을 사용하는 전략 알고리즘이다.



## Divide and Conquer

Divide and Conquer Strategy(분할 정복 전략)은 문제 해결 방법 중에서 가장 유명한 재귀적 기술이다.([wikipedia](https://en.wikipedia.org/wiki/Divide_and_conquer_algorithm))

문제를 분할 정복 전략으로 풀어내기 위해서는 다음과 같은 두 가지 단계를 거쳐야 한다.

1. 기본 단계를 해결한다. 단, 이 부분은 가능한 한 간단한 문제이어야 한다.
2. 문제가 기본 단계가 될 때까지 나누거나 작게 만든다.



#### Quick Sort

[Quick Sort(퀵 정렬)](https://github.com/JaeWC/TIL/blob/master/Algorithm/quickSort.js)는 정렬 알고리즘으로 [선택 정렬](https://github.com/JaeWC/TIL/blob/master/Algorithm/selectionSort.js)보다 훨씬 빠르고 실제로도 자주 사용된다. 퀵 정렬은 분할 정복 전략을 사용하기 때문에 주어진 배열을 **기본 단계**가 될 때까지 나누어야 한다. 결국 Quick Sort는 다음과 같이 작동한다.

- Quick Sort의 기본 단계는 빈 배열 또는 원소가 하나인 배열이다.

- 우선, 배열에서 원소 하나를 고른다. 이 원소를 **Pivot(기준 원소)**이라 한다.
- 모든 원소를 Pivot보다 작은 원소와 큰 원소로 분류하는 **Partioning(분할)**을 진행한다.
  - 첫 분할 이후에 **Pivot보다 작은 하위 배열**, Pivot, **Pivot보다 큰 하위 배열**로 나뉜다.
  - 두 개의 정렬되지 않은 Sub-array(하위 배열)들이 정렬되어 있다면 전체 배열을 정렬하는 일이 쉬워진다.
- 두 개의 하위 배열에 대하여 퀵 정렬을 호출하여 기본 단계(`array.length < 2`)에 이르게 하면 된다.



## Big-O

Quick Sort는 Pivot을 어떻게 선택하느냐에 따라서 최악의 경우 O(n^2)의 시간 복잡도를 갖게 될 수도 있다.

실제로 `pivot = array[0]`으로 Quick Sort 알고리즘을 구현할 경우 브라우저 환경에서 `Uncaught RangeError: Maximum call stack size exceeded`의 에러 메시지를 발견하는 경우가 생긴다. 

물론 평균적인 경우 퀵 정렬은 O(n log n)의 실행 시간을 갖게 된다.



