---
title: "[SQL] SELECT"
description: 
author: Enxec
date: 2022-09-25
categories: [Language, SQL]
tags: [sql, SELECT]
pin: false
math: true
mermaid: true
image:
  path: /thumbnail/sql-logo.png
  lqip: 
  alt: 
---

SELECT는 테이블 또는 개체의 속성을 작성할 때 사용된다. 테이블의 데이터는 속성 즉, 컬럼에 다 담겨 있으므로 SELECT가 쿼리문장에서 빠질래야 빠질 수 없다. 그럼 긴말 필요 없이 바로 SELECT를 어떻게 사용하고 활용하는지 알아보자.

## SELECT 문법
---
간단한 쿼리를 통해 SELECT문 사용법을 알아보자. 예시는 아래와 같다.

### 사용법

```sql
-- 테이블의 전체 컬럼에 대한 데이터를 가져올 때
SELECT [ALL / DISTINCT] *
  FROM 테이블명;

-- 테이블의 특정 컬럼에 대한 데이터를 가져올 때
SELECT [ALL / DISTINCT] 컬럼명, 컬럼명, 컬럼명, ...
  FROM 테이블명;
```

### 옵션
- ALL
  >Default 옵션으로 별도로 표시하지 않아도 된다. 즉, 중복된 데이터가 있어도 모두 출력한다.
- DISTINCT
  >중복된 데이터가 있을 경우 1건으로 처리해 출력한다.

### 예제
예제에 사용되는 릴레이션은 아래와 같다.

![DEPT 릴레이션](/posts/20220925/dept-relation.png "DEPT 릴레이션"){: width="100%"}
<div style="color: gray; text-align: center; margin-bottom: 30px;">DEPT 릴레이션</div>

<br>

```sql
-- 테이블의 전체 컬럼에 대한 데이터를 가져올 때
SELECT *
  FROM DEPT;
```

![테이블의 전체 컬럼에 대한 데이터를 가져올 때](/posts/20220925/dept-relation.png "테이블의 전체 컬럼에 대한 데이터를 가져올 때"){: width="100%"}

<br>

```sql
-- 테이블의 특정 컬럼에 대한 데이터를 가져올 때
SELECT DEPTNO, DNAME
  FROM DEPT;
```

![테이블의 특정 컬럼에 대한 데이터를 가져올 때](/posts/20220925/query-example1.png "테이블의 특정 컬럼에 대한 데이터를 가져올 때"){: width="100%"}

<br>

```sql
-- 테이블의 특정 컬럼에 대한 데이터를 중복제거하고 가져올 때
SELECT DISTINCT LOC
  FROM DEPT;
```

![테이블의 특정 컬럼에 대한 데이터를 중복제거하고 가져올 때](/posts/20220925/query-example2.png "테이블의 특정 컬럼에 대한 데이터를 중복제거하고 가져올 때"){: width="100%"}

<br>

## ALIAS 부여
---
SELECT문은 컬럼명을 명시할 때 ALIAS라는 것을 사용하여 컬럼에 일종의 별명을 부여할 수 있다. ALIAS 부여 시 지켜야할 조건은 다음과 같다.
- 컬럼명 바로 뒤에 온다.
- 컬럼명과 ALIAS 사이에 AS, as 키워드를 사용할 수 있다(옵션).
- 이중 인용부호는 ALIAS가 공백, 특수문자를 포함할 경우와 대소문자 구분이 필요할 때 사용한다.

### 사용법

```sql
SELECT 컬럼명 AS 별명, 컬럼명 AS 별명, 컬럼명 AS 별명, ...
  FROM 테이블명;

-- 공백, 특수문자를 포함하거나 대소문자 구분이 필요할 때
SELECT 컬럼명 AS "별명", 컬럼명 AS "별명", 컬럼명 AS "별명", ...
  FROM 테이블명;
```

### 예제
예제에 사용되는 릴레이션은 아래와 같다.

![DEPT 릴레이션](/posts/20220925/dept-relation.png "DEPT 릴레이션"){: width="100%"}
<div style="color: gray; text-align: center; margin-bottom: 30px;">DEPT 릴레이션</div>

<br>

```sql
SELECT DEPTNO AS 부서번호, DNAME AS 부서명, LOC AS 위치
  FROM DEPT;
```

![일반적인 Alias 사용](/posts/20220925/query-example3.png "일반적인 Alias 사용"){: width="100%"}

<br>

```sql
-- 공백, 특수문자를 포함하거나 대소문자 구분이 필요할 때
SELECT DEPTNO AS "DEPT NO", DNAME AS "Dname", LOC AS "위치^"
  FROM DEPT;
```

![공백, 특수문자를 포함하거나 대소문자 구분이 필요할 때](/posts/20220925/query-example4.png "공백, 특수문자를 포함하거나 대소문자 구분이 필요할 때"){: width="100%"}

<br>

## 산술 연산자
---
산술 연산자는 NUMBER와 DATE 자료형에 대해 적용되며, 일반적으로 수학의 사칙연산과 동일하다. 그리고 우선순위를 위한 괄호 적용이 가능하다. 일반적으로 산술 연산을 사용하거나 특정 함수를 적용하면 컬럼의 레이블이 길어지고, 기존의 컬럼에 대해 새로운 의미를 부여한 것이므로 적절한 ALIAS를 새롭게 부여하는 것이 좋다. 산술 연산자는 수학에서와 같이 (), *, /, +, - 의 우선순위를 가진다.  

SELECT문에서는 산술 연산자를 어떻게 활용하는지 살펴보자.

### 사용법

```sql
SELECT 컬럼명 - 컬럼명 AS "별명"
  FROM 테이블명;
```

### 예제
예제에 사용되는 릴레이션은 아래와 같다.

![EMP 릴레이션](/posts/20220925/emp-relation.png "EMP 릴레이션"){: width="100%"}
<div style="color: gray; text-align: center; margin-bottom: 30px;">EMP 릴레이션</div>

<br>

```sql
SELECT 연봉 - 커미션 AS "연봉 - 커미션"
  FROM EMP;
```

![산술 연산자 예제](/posts/20220925/query-example5.png "산술 연산자 예제"){: width="100%"}

<br>

## 합성 연산자
---
문자와 문자를 연결하는 합성 연산자를 사용하면 별도의 프로그램 도움 없이도 쿼리문장만으로도 유용한 리포트를 출력할 수 있다. 합성 연산자의 특징은 다음과 같다.
- 문자와 문자를 연결하는 경우 2개의 수직 바를 사용한다(Oracle).
- 문자와 문자를 연결하는 경우 + 표시를 사용한다(SQL Server).
- CONCAT (string1, string2) 함수를 사용할 수 있다(Oracle, SQL Server).
- 컬럼과 문자 또는 다름 컬럼과 연결한다.
- 문자 표현식의 결과에 의해 새로운 컬럼을 생성한다.

### 사용법

```sql
-- Oracle
SELECT 컬럼명 || '문자열' || 컬럼명 AS "사람별 직업정보"
  FROM 테이블명;

-- SQL Server
SELECT 컬럼명 + '문자열' + 컬럼명 AS "사람별 직업정보"
  FROM 테이블명;
```

### 예제
예제에 사용되는 릴레이션은 아래와 같다.

![EMP 릴레이션](/posts/20220925/emp-relation.png "EMP 릴레이션"){: width="100%"}
<div style="color: gray; text-align: center; margin-bottom: 30px;">EMP 릴레이션</div>

<br>

```sql
-- Oracle
SELECT ENAME || '의 직업은 ' || JOB AS "사람별 직업정보"
  FROM EMP;

-- SQL Server
SELECT ENAME + '의 직업은 ' + JOB AS "사람별 직업정보"
  FROM EMP;
```

![합성 연산자 예제](/posts/20220925/query-example6.png "합성 연산자 예제"){: width="100%"}

---

읽어주셔서 감사합니다. 😊 

__Reference__  
SQL 전문가 가이드 - Kdata 한국데이터산업진흥원