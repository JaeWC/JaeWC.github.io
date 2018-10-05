---
layout: post
title: "[What is Algorithm] What is Breadth First Search"
subtitle:   "Algorithm"
categories: algorithm
tags: understanding algorithm
comments: true
---

너비 우선 탐색(BFS: Breadth-First Search)을 사용하면 두 항목 간의 최단 경로를 찾을 수 있다. 



## What is Graph?

Graph는 node간 edge의 집합을 모형화한 것이다. Graph에서 node는 여러 다른 node와 바로 이어질 수 있으며, 바로 연결된 node들을 neighbor라고 한다. 

결국 그래프는 항목들이 서로 어떻게 연결되어 있는지를 모형화하는 방법이다.([What is Graph](https://github.com/JaeWC/TIL/blob/master/Algorithm/%5BDataStructure%5D%20What%20is%20Graph.md))



## Breadth-First Search

너비 우선 탐색은 그래프를 대상으로 하는 탐색 알고리즘이다. 너비 우선 탐색은 다음과 같은 질문에 답하는 데 도움이 된다.

- node A에서 node B로 가는 경로가 존재하는가?
- node A에서 node B로 가는 최단 경로는 무엇인가?

너비 우선 탐색이 진행될수록 탐색 범위는 출발점에서 멀어진다. 