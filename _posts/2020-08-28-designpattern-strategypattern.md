---
layout: post
title:  "Design Pattern - Strategy Pattern"
summary: 전략 패턴
author: 서준석
date: '2020-08-28 20:20:00'
category: designpattern
thumbnail: /assets/img/designpattern/thumbnail_strategypattern.png
keywords: designpattern, strategypattern
permalink: /blog/designpattern-strategypattern
---
# Strategy Pattern - 전략 패턴

<img src="../assets/img/designpattern/basic.png" width="70%"/>
<hr/>

Interface
- 키보드나 디스플레이 따위로 사람과 컴퓨터를 연결하는 장치
- 기능에 대한 선언과 구현 분리
- 기능 구현 통로
  - 선언은 따로하고 구현은 다른 파일에서 한다.
<br/>

```java
public interface FunctionA{
    //기능에 대한 선언
    public void FuncA();
}

public class A_interface_implement implements FunctionA{
    // 기능을 구현
    // 기능을 사용할 수 있는 통로
    @Override
    public void FuncA(){
        System.out.println("기능 A");
    }
}

public class Main{
    public static void main(String[] args){
        FunctionA a = new FunctionA();
        a.FuncA();
    }
}
```

Deligate : 위임하다
* 특정 객체의 기능을 사용하기 위해 다른 객체의 기능을 호출하는 것 

```java
public class Bobj{
    FunctionA a;
    public Bobj(){
       a = new FunctionA(); 
    }
    public void FuncB(){
        a.FuncA();
        a.FuncA();
    }
}

public class Main{
    public static void main(String[] args){
        Bobj b = new Bobj();
        a.FunB();
    }
}
```

Strategy Pattern
- 여러 알고리즘을 하나로 추상적인 접근점을 만들어 접근점에서 서로 교환 가능하도록 하는 패턴

```java
public interface Weapon(){
    public void attack();
}

public class Knife implements Weapon{
    @Override
    public void attack(){
        System.out.println("검 공격");
    }
}

public class Sword implements Weapon{
    @Override
    public void attack(){
        System.out.println("칼 공격");
    }
}

public class Character{
    private Weapon weapon;

    public void setWeapon(Weapon weapon){
        this.weapon = weapon;
    }

    public void attack(){
        //Deligate : 공격이라는 기능을 Weapon에 따라 다르게 발생
        if(weapon == null){
          System.out.println("맨손 공격");
        }
        else{
          weapon.attack();
        }
    }
}

public class Main{
  public static void main(String[] args){
    Character c = new Character();

    c.attack();

    c.setWeapon(new Knife());
    c.attack();
    c.setWeapon(new Sword());
    c.attack();
  }
}
```
> 맨손 공격<br/>칼공격<br/>검 공격


* 새로운 무기를 추가하라는 유지보수 요청이 들어올 경우!
  * Weapon 인터페이스를 implements한 무기 Class를 생성한다.