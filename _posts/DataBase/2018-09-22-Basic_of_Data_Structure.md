---
layout: post
title: "[Data Structure] What is Data Structure"
subtitle: "Basic of Data Structure"
categories: database
tags: data structure
comments: true
---

# What is Data Structure

자료 구조(Data Structure)는 데이터를 어떠한 공간에 어떻게 저장할 것인지가 설계되어 있는 것이다. JavaScript의 경우 Array와 Object가 대표적인 자료구조에 해당한다. 자료를 효율적으로 저장하는 것은 보다 효율적인 알고리즘을 사용할 수 있게 한다.



### Stack

> Stack Structure에 먼저 저장된 것이 가장 나중에 출력되는 구조이다. 

stack 구조의 예시로는 `전자 계산기 구현, 미로 찾기, 자연어 처리, 컴퓨터 메모리 관리`등이 있다.  ([What is Stack](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructure%5D%20What%20is%20Stack.md))



### Queue

> Queue Structure에 가장 먼저 저장된 것이 먼저 출력되는 구조로 FIFO(First In First Out) 형태이다.

Stack 구조와는 반대로 가장 나중에 저장된 것이 가장 먼저 출력되는 자료 구조로 우선순위가 필요한 모든 곳에서 사용된다. ([What is Queue](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructure%5D%20What%20is%20Queue.md))



### Linked List

> 각 Node가 data와 pointer를 갖고 연결된 방식으로 데이터를 저장하는 구조이다.

각 node에 있는 pointer 공간의 개수에 따라 Singly Linked List(각 node의 pointer는 다음 node를 가리킨다)와 Doubly Linked List(두 개의 pointer는 각각 앞의 node와 뒤의 node를 가리킨다)로 분류할 수 있다.

연결된 node의 중간 지점에서도 자료의 추가와 삭제가 **O(1)**의 시간에 가능하다는 장점이 있지만, 특정 위치의 데이터를 검색해내는데에는 **O(n)**의 시간이 걸리는 단점도 있다. ([What is Linked List](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructure%5DWhat%20is%20Linked%20List.md))



### Graph

> 꼭짓점과 꼭짓점을 잇는 변으로 구성되는 구조이다. ([What is Graph](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructure%5DWhat%20is%20Graph.md))



### Tree

> Graph 구조의 일종으로 서로 다른 두 노드를 잇는 길이 하나뿐인 그래프를 의미한다.

트리에서 최상위 노드를 루트 노드(root node)라고 한다. 또한 노드 A가 노드 B를 가리킬 때 A를 B의 부모 노드(parent node), B를 A의 자식 노드(child node)라고 한다. 자식 노드가 없는 노드를 잎 노드(leaf node)라고 한다. 잎 노드가 아닌 노드를 내부 노드(internal node)라고 한다. ([What is Tree](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructure%5D%20What%20is%20Tree.md))

이진 트리(Binary Tree)는 각각의 노드가 최대 두 개의 자식 노드를 가지는 트리 자료 구조를 말한다. ([Binary Search Tree](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructure%5D%20What%20is%20Tree.md#binary-search-tree))



### Hash Table

> 키를 값에 매핑할 수 있는 구조인, 연관 배열 추가에 사용되는 자료 구조이다.

해시 테이블은 해시 함수를 사용하여 색인(index)을 버킷(bucket)이나 슬롯(slot)의 배열로 계산한다. ([What is Hash Table](https://github.com/JaeWC/TIL/blob/master/Data/%5BDataStructue%5DWhat%20is%20Hash%20table.md)