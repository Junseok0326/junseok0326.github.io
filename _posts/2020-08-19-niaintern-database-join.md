---
layout: post
title:  "Join 개념 및 종류"
summary: 공공데이터 인턴 교육
author: 서준석
date: '2020-08-19 12:31:00 +0530'
category: database
thumbnail: /assets/img/publicdata/join.png
keywords: database, nia, sql, join
permalink: /blog/database_join
---
# Join

## 1. 개념
* 조인은 관계형 DB에서 가장 기본적이고 중요한 기능
* 집합간의 곱
* 관계형 DB에서는 서로 독립적인 Data들간의 정보연결을 위해 Join을 이용해 필요 시 다양한 정보를 참조하고 창출
* 연산자에 따라 Equi Join, Non-Equi Join, Anti Join 등 다양

### 필요성
* Data 중복 제거
* 여러 Entity로 Data가 나눠서 저장
* 연결 관계를 통해 여러 Entity의 Data를 조회

## 2. 종류
1. Natural Join
    * 두 테이블에서 Data 유형과 이름이 일치하는 열을 기반으로 자동으로 테이블을 Join, ANSI 표준
    * Join은 두 테이블의 이름과 Data 유형이 동일한 열에서만 발생
    * 둘 중 하나라도 다를 경우 Natural Join 구문에서 오류 발생
2. Equi Join
    * 등호 연산자가 포함된 Join 조건이 있는 Join
    * 지정 열에 동등 값이 있는 행을 결합
3. Non-Equi Join
    * <= 및 >= 등의 범위 조건을 이용한 Join
4. Outer Join
    * Outer Join 대상 Table의 자료가 존재할 경우 그 정보를 출력하고 없으면 기존 자료만 출력
    * 한쪽 집합이 기준이 되어 다른 쪽 집합의 연결되는 조건에 상관없이 기준이 되는 집합은 무조건 추출되는 Join
    * Outer Join의 기준이 되는 집합은 항상 Join에 성공
    * 종류
        1. Left Outer Join
        2. Right Outer Join
        3. Full Outer Join
5. Self Join
    * 테이블 자체 조인
6. Cross Join
    * 두 테이블의 Cartesian product를 생성하는 Join
    * 두 테이블 간에는 WHERE 조건을 지정하지 않는다.

### 3. 메서드
* 조인 방식은 두 행 소스 간의 관계를 정의
* 두 데이터 소스에서 데이터를 결합하는 방식
* 객체의 관련 방식을 정의하는 Join 술어를 통해 제어
* 유형
    1. Nested Loop Join
        * 소규모 Data를 Join하려고 할 때 Join 조건이 두번째 Table을 엑세스하기에 효율적인 방법인 경우 유용
        * 두 Table 중 하나는 Outer Join 또는 Driving Join 또는 Left Table로 정의
        * 다른 Table은 Inner Table 또는 Right Table이라 함
        * 단일 테이블 술어를 만족하는 Outer Table의 각 행에 대해 Join 술어를 만족하는 Inner Table의 모든 행이 검색
    2. Hash Join
        * 처리량이 많은 자료에 대한 Join시 유리
        * 가장 작은 행 소스를 사용해 Hash Table 생성
        * 두번째 행 소스가 Hashing 처리되고 Hash Table에 대한 검사
        * Probe Table의 Join Column에 Index가 필요 없음
        * Build Table은 크기가 상대적으로 작은 것이 성능에 유리
        * 매우 많은 자료를 가진 Table이 Build Table이 될 경우 상당한 성능 저하 발생
        * = 조건에서만 사용 가능
        * 사용자의 요구 조건과 관계없이 Build Table은 모두 읽어야하며 Probe Table은 일부만 읽어도 원하는 처리가 가능하기도 함
        * 처리 순서가 중요
    3. Sort Merge Join
        * 대량의 자료 처리시 Nested Join보다 우수한 성능을 보이지만 Hash Join보다는 성능이 떨어짐
        * Table을 읽으며 Join Key를 중심으로 Sort 후 각각의 값을 비교해 일치 자료를 반환
        * Join Column에 대한 Index가 필요 없음
        * 사용자의 요구 조건과 무관하게 양쪽의 Table을 모두 읽고 Sort를 해야 함
        * 처리 순서는 성능과 무관

>### 정리
> * Join은 양쪽 테이블에 Join Key로 매칭되는 Data를 반환하는 작업
> * Join Key를 연결시키는 연산유형에 따라 여러가지 Join 수행
> * Join Key로 매칭되는 Data 뿐만 아니라 매칭되지 않는 Data도 반환하는 Join을 Outer Join이라 함
> * 양쪽 테이블을 Join을 통해 연결시키는 Join방법에 따라 NLJ, HJ, SMJ 방법이 있음
> * Join시 어느 쪽 Table을 먼저 읽느냐에 따라 처리성능이 달라짐