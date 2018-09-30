---
layout: post
title: "[What is Algorithm] What is Selection Sort"
subtitle:   "Algorithm"
categories: algorithm
tags: understanding algorithm
comments: true
---

컴퓨터 메모리에 여러 개의 데이터를 저장해야 한다면 배열(Array)과 리스트(List)라는 두 가지 방법 중 하나를 사용해야 한다.



## Linked List and Array



#### Insertion at Last

###### Array

배열에 여러 개의 데이터를 순서대로 저장해야 한다면, 저장할 데이터를 메모리에 차례대로 붙여서 저장하면 된다. 

만약 새로운 데이터를 추가하고 싶어질 경우 기존의 데이터 공간 다음이 빈 메모리인지 확인해야 할 것이며, 빈 메모리를 찾아서 필요한 만큼 데이터를 저장해야 한다. 

이와 같이 메모리의 위치를 이동시키는 과정을 피하기 위해서는 여분의 메모리를 미리 할당해두는 것인데, 이는 메모리를 효율적으로 쓰지 못한다는 문제가 있다.



###### Linked List

연결 리스트의 각 원소에는 목록의 다음 원소에 대한 주소가 저장되어 있다. 즉, 여러 가지 임의의 메모리 주소들이 하나의 목록으로 연결되어 있다.([What is Linked List](https://github.com/JaeWC/TIL/blob/master/Algorithm/%5BDataStructure%5DWhat%20is%20Linked%20List.md)). 

연결 리스트는 마지막에 새로운 데이터를 추가하더라도 마지막 데이터 메모리의 주소를 저장하여 연결해두면 되기 때문에 배열과 같은 데이터 이동의 문제를 해결할 수 있다.



#### Insertion at Center

새로운 데이터를 중간에 추가하는 경우, 연결 리스트는 특정 위치 직전의 데이터에 기록된 메모리 주소를 변경하면 된다.

배열의 경우 다음에 오는 모든 데이터의 위치를 이동해야 한다.



#### Access

연결 리스트에서 마지막 데이터를 바로 읽을 수 없다. 연결 리스트는 그 다음 데이터의 주소 만을 알고 있기 때문에 마지막 데이터 데이터에 접근하려면 첫 번째 데이터부터 마지막까지 모두 읽어가야 한다.

배열은 모든 데이터의 주소 즉, index 값을 알고 있다. 따라서 특정 데이터를 읽어야 한다면 바로 접근이 가능하다.



#### Deletion

특정 데이터를 삭제하는 경우에도 연결 리스트는 직전 데이터가 가르키는 주소 만을 변경하면 되지만, 배열의 경우 데이터를 삭제시킨 이후 다른 데이터의 위치를 이동시켜야 한다.



|               | Array | Linked List |
| ------------- | :---: | :---------: |
| **Access**    | O(1)  |    O(n)     |
| **Insertion** | O(n)  |    O(1)     |
| **Deletion**  | O(n)  |    O(1)     |



## Selection Sort

[Selection Sort(선택 정렬)](https://github.com/JaeWC/TIL/blob/master/Algorithm/selectionSort.js)란 모든 데이터 항목을 살펴보고 필요한 값을 찾아서 새로운 목록에 기록하는 것을 반복하여 정렬된 데이터 목록을 얻는 정렬 방법을 의미한다.

선택 정렬의 경우 n개의 항목에 대하여 n번 반복 시행을 하기에 **O(n^2)**의 시간 복잡도를 갖는다. 

선택정렬은 분명 깔끔한 알고리즘이지만 빠르지 않다. 반면 Quick Sort(퀵 정렬)는 **O(n log n)**의 시간 복잡도를 갖는 정렬 알고리즘이다.