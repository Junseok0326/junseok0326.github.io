---
layout: post
title:  "Java - Constructor"
summary: 자바 생성자에 대하여
author: 서준석
date: '2020-08-21 14:08:00'
category: java
thumbnail: /assets/img/java/thumbnail_constructor.png
keywords: algorithm, leetcode, easy problem
permalink: /blog/java-constructor
---
# Constructor - 생성자


### 1. 역할

* 인스턴스를 만들고 인스턴스의 속성(변수)들을 초기화시킨다.

* 클래스에 아무런 생성자가 없을 경우 컴파일러가 자동으로 파라미터 없는 생성자를 제공해준다.<br/>**그러나 생성자를 하나라도 정의하면 이 생성자는 사용불가**
<hr/>

### 2. 예시코드
``` java
public class Person{
    private String name;
    private int age;
    
    //생성자 오버로딩의 예시
    public Person(String pName, int pAge){
        this.name = pName;
        this.age = pAge;
    }
    public Person(String pName){
        this.name = pName;
        this.age = 0;
    }
    public Person(int pAge){
        this.name = "???";
        this.age = pAge;
    }
}

public class Main{
    public static void main(String[] args){
        Person p1 = new Person("서준석",25);
        Person p2 = new Person("서또니");
        Person p3 = new Person(24);
    }
}
```
<hr/>

### 3. 기본 생성자
생성자를 한 개도 정의 하지 않았을 때 JAVA에서 자동으로 생성해주는 것