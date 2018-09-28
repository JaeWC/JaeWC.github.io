---
layout: post
title: "[What is Algorithm] What is Algorithm"
subtitle:   "Algorithm"
categories: algorithm
tags: understanding algorithm
comments: true
---

## Big-O Notation

Big-O notation은 알고리즘이 얼마나 빠른지 표시하는 특별한 방법이다. 다만 빅오 표기법은 속도를 시간 단위로 세는 것이 아니고 **연산 횟수를 비교하기 위한 것**이다.



#### Example: Searching Algorithm

|            단순 탐색             | 이진 탐색([binarySearch.js](https://github.com/JaeWC/TIL/blob/master/Algorithm/binarySearch.js)) |
| :------------------------------: | :----------------------------------------------------------: |
|   100개의 아이템 -> 100번 추측   |                 100개의 아이템 ->   7번 추측                 |
| 40억 개의 아이템 -> 40억 번 추측 |               40억 개의 아이템 ->   32번 추측                |
|         O(n) : 선형 시간         |                     O(log n) : 로그 시간                     |



#### Kinds of Big-O Notation

- O(1) : Constant
- O(log n) : Logarithmic (로그 시간: Binary Search)
- O(n) : Linear (선형 시간: Linear Search)
- O(n * log n) : 빠른 정렬 알고리즘 (Quick Sort)
- O(n^2) : Quadratic (느린 정렬 알고리즘: Selection Sort)
- O(n!) :  정말 느린 알고리즘



#### Reference

- [Big-O Cheat Sheet](http://bigocheatsheet.com/)

- [Wikipedia](https://en.wikipedia.org/wiki/Big_O_notation)