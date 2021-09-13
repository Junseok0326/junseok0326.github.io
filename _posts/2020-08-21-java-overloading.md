---
layout: post
title:  "Java - Method OverLoading, OverRiding"
summary: 오버로딩과 오버라이딩에 대해
author: 서준석
date: '2020-08-21 13:15:00'
category: java
thumbnail: /assets/img/java/thumbnail_overloadride.png
keywords: algorithm, leetcode, easy problem
permalink: /blog/java-overloading&overriding
---
# OverLoading - 오버로딩

<img src="../assets/img/java/methodoverloading.png"/>

<hr/>

### 1. 개념

클래스 내에 같은 이름의 메소드를 2개 이상 정의

<hr/>

### 2. 예시코드
``` java
public class OverLoading{
    public void exam(String str){
        System.out.println(str);
    }

    public void exam(int a, int b){
        System.out.println(a+b);
    }
}
```
<br/><br/>

# OverRiding - 오버라이딩

<img src="../assets/img/java/methodoverriding.png"/>

## 1. 개념

상위 클래스가 가지고 있는 메소드를 하위 클래스가 재정의 해서 사용

<hr/>
