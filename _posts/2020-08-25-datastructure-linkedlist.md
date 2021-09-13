---
layout: post
title:  "DataStructure - Linked List"
summary: 연결 리스트
author: 서준석
date: '2020-08-25 11:20:00'
category: datastructure
thumbnail: /assets/img/datastructure/thumbnail_linkedlist.png
keywords: datastructure, linked list
permalink: /blog/datastructure-linkedlist
---
# Linked List - 연결 리스트

<img src="../assets/img/datastructure/linkedlist.png"/>

<hr/>

## 1. 개념

* ### 노드(node)와 링크(link)를 구조화 시킨 것
  * 노드(node) : 데이터를 담고 있는 그릇
  * 링크(link) : 리스트의 순서를 유지해주는 연결고리

* ### 특징
  * 데이터를 순서대로 저장한다.
  * 요소를 계속 추가 가능하다.
* ### 배열과의 비교
  * 공통점 : 순차적으로 데이터를 저장하는 것
  * 차이점
    * 연결리스트 : 계속해서 동적으로 늘였다 줄였다 할 수있다.
    * 배열 : 선언할 때 저장할 공간을 미리 저장해야한다.
<br/>
<br/>

### 2. 코드 구현
```python
class Node:
    def __init__(self,data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    # 맨 뒤에 노드 삽입할때
    def append(self, data):
        new_node = Node(data)

        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node

    # 연결리스트를 문자열로 표현
    def __str__(self):
        res_str = "| "

        iterator = self.head

        while iterator is not None:
            res_str += f"{iterator.data} | "
            iterator = iterator.next

        return res_str

    # 해당 인덱스의 노드 검색
    def find_node_at(self,index):
        # 해당 인덱스의 노드 검색
        iterator = self.head
        for _ in range(index):
            iterator = iterator.next

        return iterator

    # 두 노드 사이에 삽입 할때
    def insert_after(self,previous_node,data):
        new_node = Node(data)

        #가장 마지막 순서 삽입
        if previous_node is self.tail:
            self.tail.next = new_node
            self.tail = new_node
        else:
            new_node.next = previous_node.next
            previous_node.next = new_node

    # 새로운 노드 데이터를 가장 앞에 삽입
    def prepend(self,data):
        new_node = Node(data)

        if self.head is None:
            self.tail = new_node
        else:
            new_node.next = self.head

        self.head = new_node

    # 노드 삭제 메소드
    def del_after(self,previous_node):
        data = previous_node.next.data

        if previous_node.next is self.tail:
            previous_node.next = None
            self.tail = previous_node
        else:
            previous_node.next = previous_node.next.next

        return data

    # 가장 앞에 노드 삭제
    def pop_left(self):
        data = self.head.data

        if self.head != self.tail:
            self.head = self.head.next
            self.head.next = self.head.next
        else:
            self.head = None
            self.tail = None

        return data

list = LinkedList()

list.append(1)
print(list)
list.prepend(2)
print(list)
node = list.find_node_at(0)
list.insert_after(node, 4)
print(list)
list.del_after(node)
print(list)
list.pop_left()
print(list)
list.pop_left()
print(list)
```
- ## 실행 결과
>| 1 |<br/>
| 2 | 1 |<br/>
| 2 | 4 | 1 |<br/> 
| 2 | 1 | <br/>
| 1 | <br/>
| <br/>

### 3. 시간복잡도
* ## 접근
  * 인덱스 n에 있는 데이터에 접근하려면 연결 리스트의 head부터 n번 후 노드를 찾아서 가야한다.<br/>
  즉, 최악의 경우에는 head노드에서 총 n-1번 다음 노드로 가야한다.<br/>
  걸리는 시간이 n에 비례하기 때문에 최악의 경우 O(n)의 시간 복잡도를 가진다.
* ## 탐색
  * 연결리스트와 배열의 탐색 방법은 같다.<br/>
  가장 앞 노드부터 다음 노드를 하나씩 보면서 원하는 데이터를 찾는다.<br/>
  그렇기 때문에 최악의 경우에는 접근과 마찬가지로 O(n)의 시간복잡도를 가진다.
* ## 삽입 / 삭제
  * 특정 값에 비례하지 않고 항상 일정하다.<br/>w
  O(1)의 시간복잡도를 가진다.