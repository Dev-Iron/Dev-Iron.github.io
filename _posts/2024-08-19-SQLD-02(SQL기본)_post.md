---
title: SQLD 02 (SQL기본)
date: 2024-08-18 20:00:00 +09:00
categories: [SQLD]
tags: [sqld, sql, cs]     # TAG names should always be lowercase
---


## 2-1 관계형 데이터베이스 개요

**데이터베이스 (Database)와 DBMS(Database Management System)**
- **데이터베이스** : 데이터의 집합. 꼭 형식을 갖추지 않아도 엑셀 파일을 모아 둔다면 그것 또한 데이터베이스
- **DBMS** : 데이터를 효과적으로 관리하기 위한 시스템
  - 개인이 파일을 여러 개 묶어서 폴더에 보관하면 데이터를 찾고 관리하는데 많은 비용이 발생한다. 이를 보다 시스템적으로 작동하게 만든 시스템을 DBMS라고 한다. (ORACLE, MYSQL 등)

<br>

**관계형 데이터베이스 구성 요소**
- **계정** : 데이터의 접근 제한을 위한 여러 업무별/시스템별 계정이 존재
- **테이블** : DBMS의 DB 안에서 데이터가 저장되는 형식
- **스키마** : 테이블이 어떠한 구성으로 되어있는지, 어떠한 정보를 가지고 있는지에 대한 기본적인 구조를 정의

<br>

**테이블**
1) 정의
   - 엑셀에서의 워크시트처럼 행(로우)과 열(컬럼)을 갖는 2차원 구조로 구성, 데이터를 입력하여 저장하는 최소 단위
   - 컬럼은 속성이라고도 부름(모델링 단계마다 부르는 용어가 다름)

2) 특징
    - 하나의 테이블은 반드시 하나의 유저(계정) 소유여야 함
    - 테이블간 관계는 일대일(1:1), 일대다(1:N), 다대다(N:N)의 관계를 가질 수 있음
    - 테이블명은 중복될 수 없지만, 소유자가 다른 경우 같은 이름으로 생성 가능
    - Ex. SCOTT 소유의 EMP 테이블 존재. HR 소유의 EMP 테이블 생성 가능(같은 계쩡 내 동일한 객체명 생성 불가)
    - 테이블은 행 단위로 데이터가 입력, 삭제되며 수정은 값의 단위로 가능

<br>

> **TIP** 객체 : DBMS에서의 객체는 생성하고 변경할 수 있는 하나의 관리 대상을 나타냅니다.

<br>

**SQL(Structured Query Language)**
- 관계형 데이터베이스에서 데이터 조회 및 조작, DBMS 시스템 관리 기능을 명령하는 언어
- 데이터 정의(DDL), 데이터 조작(DML), 데이터 제어 언어(DCL) 등으로 구분
- SQL 문법은 대,소문자로 구분하지 X

<br>

**관계형 데이터베이스 특징**
- 데이터의 분류, 정렬, 탐색 속도가 빠름
- 신뢰성이 높고, 데이터의 무결성 보장
- 기존의 작성된 스키마를 수정하기가 어려움
- 데이터베이스의 부하를 분석하는 것이 어려움

<br>

**데이터 무결성(Integrity)**
- **데이터의 정확성과 일관성을 유지하고, 데이터에 결손과 부정합이 없음을 보증하는 것**
- 데이터베이스에 저장된 값과 그것이 표현하는 현실의 비즈니스 모델의 값이 일치하는 정확성을 의미함
- 데이터 무결성을 유지하는 것이 데이터베이스 관리시스템에 중요한 기능

<br>

**데이터 무결성 종류**
1. **개체 무결성** : 테이블의 기본키를 구성하는 컬럼(속성)은 NULL 값이나 중복값을 가질 수 없음
2. **참조 무결성** : 외래키 값은 NULL 이거나 참조 테이블의 기본키 값과 동일해야 한다. (외래키란 참조 테이블의 기본키에 정의된 데이터만 허용되는 구조)
3. **도메인 무결성** : 주어진 속성 값이 정의된 도메인에 속한 값이어야 함
4. **NULL 무결성** : 특정 속성에 대해 NULL을 허용하지 않는 특징
5. **고유 무결성** : 특정 속성에 대해 값이 중복되지 않는 특징
6. **키 무결성** : 하나의 릴레이션(관계)에는 적어도 하나의 키가 존재해야 함 (테이블이 서로 관계를 가질 경우 반드시 하나 이상의 조인키를 가짐)

<br>

- 도메인 : 각 컬럼(속성)이 갖는 범위 (제약조건)
- 릴레이션 : 테이블간 관계를 말함
- 튜플 : 하나의 행을 의미함
- 키 : 식별자

<br>

**ERD (Entity Relationship Diagram)**
- ERD란 테이블 간 서로의 상관 관계를 그림으로 표현한 것
- ERD의 구성요소에는 엔티티(Entity), 관계(Relationship), 속성(Attribute)가 있다.
- 현실 세계의 데이터는 엔티티, 관계, 속성 구성으로 모두 표현 가능

<br>
<br>

## 2-2 SELECT 문

**SQL 종류**
- SQL은 그 기능에 따라 다음과 같이 구분함

| 구분                               | 종류                          |
| ---------------------------------- | ----------------------------- |
| DDL (Data Definition Language)     | CREATE, ALTER, DROP, TRUNCATE |
| DML (Data Mainpulation Language)   | INSERT, DELETE, UPDATE, MERGE |
| DCL (Data Control Language)        | GRANT, REVOKE                 |
| TCL (Transaction Control Language) | COMMIT, ROLLBACK              |
| DQL (Data Query Language)          | SELECT                        |

- SELECT 문은 따로 SQL 종류 중 어디에도 속하지 않아서 SELECT 문을 위한 DQL 등장

<br>

**SELECT 문 구조**
- SELECT 문은 다음과 같이 6개 절로 구성
- 각 절의 순서대로 작성해야함 (GROUP BY 와 HAVING 은 서로 바꿀 수 있지만 보통 사용하지 않음)
- SELECT의 내부 파싱(문법적 해석) 순서는 나열된 순서와는 다름

```
1- SELECT 컬럼명 
2- FROM 테이블명 또느 뷰명
3- WHERE 조회 조건
4- GROUP BY 그룹핑 컬럼명
5- HAVING 그룹핑 필터링 조건
6- ORDER BY 정렬 컬럼명
```

<br>

### SELECT 절
- SELECT 문장을 사용하여 불러올 컬럼명, 연산 결과를 작성하는 절
- *를 사용하여 테이블 내 전체 컬럼명을 불러올 수 있음
- 원하는 컬럼을 , 로 나열하여 작성 가능(순서대로 출력됨)
- 표현식이란 원래의 컬럼명을 제외한 모든 표현 가능한 대상 (연산식, 기존 컬럼의 함수 변형식 포함)

<br>

**문법**

```
SELECT | 컬럼명 | 표현식
FROM 테이블명 또는 뷰명
```

**특징**
- SELECT 절에서 표시할 대상 컬럼에 **Alias(별칭) 지정 가능**
- 대소문자를 구분하지 않아도 인식한다.

```
Ex. 전체 조회
SELECT * 
    FROM EMP;

Ex. 특정 컬럼 조회
SELECT EMPNO, ENAME, SAL
    FORM EMP;

Ex. 표현식을 사용하여 원본과 다른 데이터 출력 가능
SELECT EMPNO, ENMAE, SAL * 1.1
    FROM EMP;
```

<br>

**컬럼 Alias(별칭)**
- 컬럼명 대신 **출력할 임시 이름 지정**(SELECT 절에서만 정의 가능, 원본 컬럼명은 변경되지 않는다.)
- **컬럼명 뒤에 AS와 함께 컬럼 별칭 전달 (AS는 생략 가능)**

<br>

**특징 및 주의사항**
- SELECT 문보다 늦게 수행되는 **ORDER BY 절에서만 컬럼 별칭 사용 가능**(그 외 절에서 사용시 에러 발생)
- 한글 사용 가능(한글 지원 캐릭터셋 설정시)
- 이미 존재하는 예약어는 별칭으로 사용 불가
- Ex. avg, count, decode, SELECT, FROM 등

> 다음의 경우 별칭에 반드시 쌍따옴표 전달 필요  
1) 별칭에 공백을 포함하는 경우  
2) 별칭에 특수문자를 포함하는 경우 ("_" 제외)  
3) 별칭 그대로 전달할 경우 (입력한 대소를 그대로 출력하고자 할 때)  


```
Ex. 별칭 사용 예 (AS 생략가능)
SELECT EMPNO AS 사번, ENAME 사원이름, SAL * 1.1 AS NEW_SAL
    FORM EMP;

Ex. 별칭 선언 시 쌍따옴표가 필요한 경우 
SELECT EMPNO, ENAME, SLA * 1.1 AS "NEW SAL"
    FROM EMP;
```

<br>

### FROM 절
- 데이터를 불러올 테이블명 또는 뷰명 전달
- 테이블 여러 개 전달 가능(컴마로 구분) -> 조인 조건 없이 테이블명만 나열 시 카타시안 곱 발생 주의
- **테이블 별칭 선언 가능 (AS 쓰지 않음)
  - 테이블 별칭 선언 시 컬럼 구분자는 테이블 별칭으로만 전달 (테이블명으로 사용 시 에러 발생)
- **ORACLE 에서는 FROM 절 생략 불가 (의미상 필요 없는 경우 DUAL 테이블 선언)**
  - ORACLE 23c 버전부터는 생략 가능
- **MYSQL 에서는 FROM 절 필요 없을 경우 생략 가능 (오늘 날짜 조회 시)**

```
Ex. 테이블 별칭 사용 예제
SELECT E.ENAME, E.SAL, E.DEPTNO
    FORM EMP E 
        WHEREE.DEPTNO = 10;
```

<br>

> 뷰 : 테이블과 동일하게 데이터를 조회할 수 있는 객체이지만 테이블처럼 실제 데이터가 저장된 것이 아닌, SELECT 문 결과에 이름을 붙여 그 이름만으로 조회가 가능하도록 한 기능

<br>
<br>

## 2-3 함수

**함수 정의**
- input value 가 있을 경우 그에 맞는 output value를 출력해주는 객체
- **input value 와 output value의 관계를 정의한 객체**
- from 절을 제외한 모든 절에서 사용 가능

<br>

**함수 기능**
- 기본적인 쿼리문을 더욱 강력하게 해줌
- 데이터의 계산을 수행
- 개별 데이터의 항목을 수정
- 표시할 날짜 및 숫자 형식을 지정
- 열 데이터의 유형 (data type)을 변환

<br>

**함수의 종류 (입력값의 수에 따라)**
- 단일행 함수와 복수행 함수로 구분
- **단일행 함수** : input 과  output 의 관계가 1:1 
- **복수행 함수** : 여러 건의 데이터를 동시에 입력 받아서 하나의 요약값을 리턴 (**그룹함수 또는 집계함수라고도 함**)

<br>

**입/출력값의 타입에 따른 함수 분류**  

1) 문자형 함수  
   - 문자열 결합, 추출, 삭제 등을 수행  
   - 단일행 함수 형태  
   - output은 대부분 문자값 (LENGTH, INSTR 제외)  


![문자함수](/assets/img/문자함수_종류.png)


<br>

**SQL-SERVER**
   - SUBSTR -> SUBSTRING
   - LENGTH -> LEN
   - INSTR -> CHARINDEX

<br>

2) 숫자형 함수
   - 숫자를 입력하면 숫자 값을 반환
   - 단일행 함수와 형태의 숫자함수
   - ORACLE과 SQL-Server 함수 거의 동일


![숫자함수](/assets/img/숫자함수_종류.png)

<br>

3) 날짜형 함수
    - 날짜 연산과 관련된 함수
    - ORACLE과 SQL-Server 함수 거의 다름

![날짜함수](/assets/img/날짜함수_종류.png)

<br>

**SQL-SERVER**
   - SYSDATE -> GETDATE
   - ADD_MONTHS -> DATEADD (월 뿐만 아니라 모든 단위 날짜 연산 가능)
   - MONTHS_BETWEEN -> DATEDIFF (두 날짜 사이의 년, 월, 일 추출)

<br>

4) 변환 함수
   - **값의 데이터 타입을 반환**
   - 문자를 숫자로, 숫자를 문자로, 날짜를 문자로 변경

![변환함수](/assets/img/변환함수_종류.png)

<br>

**SQL-SERVER**
   - TO_NUMBER, TO_DATE, TO_CHAR -> CONVERT (포맷 전달 시)
   - 단순 변환일 경우 주로 CAST 사용

<br>

5) 그룹 함수
    - 다중행 함수
    - **여러 값이 input 값으로 들어가서 하나의 요약된 값으로 리턴**
    - GROUP BY와 함께 자주 사용됨
    - ORACLE과 SQL-Server 거의 동일

![그룹함수](/assets/img/그룹함수_종류.png)

<br>

**SQL-SERVER**
   - VARIANCE -> VAR
   - STDDEV -> STEDV

<br>

6) 일반 함수
    - 기타 함수 (널 치환 함수 등)

![일반함수](/assets/img/일반(기타)함수_종류.png)

<br>

**Ex. DECODE 사용 예제 01**
```
SELECT DEPTNO,
    DECODE(DEPTNO, 10, '인사부', 20, '재무부') AS DENAME
FROM EMP;
```

![DECODE](/assets/img/DECODE_01.png)

> 설명 : 부서번호가 10번이면 인사부, 20번이면 재무부, 나머지는 널 리턴

<br>

**Ex. DECODE 사용 예제 02**
```
SELECT DETPNO, JOB,
    DECODE(DEPTNO, 10, 
        DECODE(JOB, 'CLERK', 'A', 'B'), 'C') AS RESULT
FROM EMP;
```

![DECODE](/assets/img/DECODE_02.png)

> 설명 : DEPTNO가 10이면서 JOB이 CLERK이면 'A', DEPTNO가 10이면서 CLERK가 아니면 'B', DEPTNO가 10이 아니면 'C'


<br>
<br>

**Ex. NVL, NVL2 사용 예제**
```
SELECT COMM,
    NVL(COMM, 0),
    NVL2(COMM, COMM * 1.1, 500)
FROM EMP;
```

![NVL](/assets/img/NVL_.png)

> 설명 : NVL2의 경우 NVL이랑 다르게 COMM의 값이 널이 아닐 때도 치환값 정의 가능  
> ->  NVL2의 경우 COMM이 널이 아니면 10% 인상값, 널이면 500 리턴

<br>

**Ex. COALESCE 사용 예제**
``` 
SELECT DEPTNO1,
    DEPTNO2,
    COALESCE(DEPTNO1, DEPTNO2, 0) AS RESULT
FROM STUDENT;
```

![COALESEC](/assets/img/COALESCE_.png)

> 설명 : DEPTNO1과 DEPTNO2 중 널 아닌 값 출력 (둘 다 널이 아니면 맨 앞 순서대로 출력). 모두 널이면 0 출력

<br>


**Ex. CASE 문 사용 예제 01**
```
SELECT SAL,
    CASE WHEN SAL < 2000 THEN 'C'
         WHEN SAL < 3000 THEN 'B'
                         ELSE 'A'
    END AS SAL_GRADE
FROM EMP;
```

![CASE](/assets/img/CASE_01.png)

> 설명 : CASE 문을 사용하여 여러 조건 (대소 비교 가능)에 대한 치환 및 연산 가능

<br>

**Ex. CASE 문 사용 예제 02**
```
SELECT DEPTNO,
    CASE DEPTNO WHEN 10 THEN '인사부'
                WHEN 20 THEN '총무부'
                WHEN 30 THEN '재무부'
                        ELSE '기타'
    END AS DNAME1,
    CASE WHEN DEPTNO = 10 THEN '인사부'
         WHEN DEPTNO = 20 THEN '총무부'
         WHEN DEPTNO = 30 THEN '재무부'
                          ELSE '기타'
    END AS DNAME2
FROM EMP;
```

![CASE](/assets/img/CASE_02.png)

> 설명 : 동등비교 시 위처럼 비교대상 (DEPTNO)를 CASE와 WHEN사이에 배치하면서 WHEN절 마다 반복하지 않아도 됨 (이 때 DEPTNO, 데이터 타입과 WHEN 절의 명시된 비교대상의 데이터 타입 반드시 일치해야함)


<br>
<br>

## 2-4 WHERE 절


**WHERE 절** 
- 테이블의 데이터 중 **원하는 조건에 맞는 데이터만 조회하고 싶을 경우 사용** (엑셀의 필터 기능과 유사)
- 여러 조건 동시 전달 가능 (AND와 OR로 조건 연결)
- **NULL 조회 시 IS NULL /IS NOT NULL 연산자 사용 (= 연산자로 조회 불가)**
- 연산자를 사용하여 다양한 표현이 가능
- 조건 전달 시 비교 대상의 데이터 타입 일치하는 것이 좋음
- Ex. EMP 테이블의 부서번호 컬럼의 데이터 타입은 숫자인데 문자 상수로비교 시 성능 문제 발생할 수 있음

<br>

| 연산자 종류           | 설명                                               |
| --------------------- | -------------------------------------------------- |
| =                     | 같은 조건을 검색                                   |
| !=, ><                | 같지 않은 조건을 검색                              |
| >                     | 큰 조건을 검색                                     |
| >=                    | 크거나 같은 조건을 검색                            |
| <                     | 작은 조건을 검색                                   |
| <=                    | 작거나 같은 조건을 검색                            |
| BETWEEN a AND b       | A와 B사이에 있는 범위 값을 모두 검색               |
| IN(a, b, c)           | A 이거나 B 이거나 C 인 조건을 검색                 |
| LIKE                  | 특정 패턴을 가지고 있는 조건을 검색                |
| IS NULL / IS NOT NULL | NULL 값을 검색 / NULL이 아닌 값을 검색             |
| A AND B               | A 조건과 B 조건을 모두 만족하는 값만 검색          |
| A OR B                | A 조건이나 B 조건 중 한가지라도 만족하는 값을 검색 |
| NOT A                 | A가 아닌 모든 조건을 검색                          |


<br>

**문법** 

```
SELECT * | 컬럼명 | 표현식
FROM 테이블명 또는 뷰명
WHERE 조회할 데이터 조건
```

<br>

**주의사항**
- 문자나 날짜 상수 표현 시 반드시 홑따옴표 사용 (다른 절에서도 동일 적용)
- ORACLE은 문자 상수의 경우 대소문자를 구분
- MYSQL은 기본적으로 문자상수의 대소문자를 구분하지 X

<br>

Ex. 이름이 SMITH인 직원 조회 (조건절에 문자 상수 사용)
```
SELECT EMPNO, ENAME, SAL
FROM EMP
WHERE ENAME = 'SMITH';
```

> 설명 : ORACLE의 경우 테이블에 데이터는 실젤 대문자로 저장되어 소문자로 조회 시 데이터 출력 안됨
<br>


EX. SAL이 1500 이상인 사원 정보 조회 (숫자 상수 전달)
```
SELECT EMPNO, ENAME, SAL
FROM EMP
WHERE SAL >= 1500;
```

<br>

Ex. COMM 값이 NULL 인 직원 정보 출력
```
SELECT EMPNO, ENAME, SAL, COMM
FROM EMP
WHERE COMM IS NULL;
```

<br>

**IN 연산자**
- 포함 연산자로 여러 상수와 일치하는 조건 전달 시 사용
- 상수를 괄호로 묶어서 동시에 전달 (문자와 날짜 상수의 경우 반드시 홑따옴표)

```
EX. SMITH와 SCOTT의 직원 정보 출력
SELECT EMPNO, ENMAE, SAL
FROM EMP
WHERE ENMAE = 'SMITH' OR ENAME = 'SCOTT';

Ex. 조건식을 IN 연산자로 변경
SELECT EMPNO, ENMAE, SAL
FORM EMP
WHERE ENMAE IN ('SMITH', 'SCOTT');
```

> 설명 : ( ) 안의 상수도 문자상수오 ㅏ날짜 상수는 홑따옴표 필수

<br>

**BETWEEN A AND B**
- A 보다 크거나 같고 B 보다 작거나 같은 조건을 만족
- A 와 B 에는 범위로 묶을 상수값 전달

```
Ex. SAL이 2000 이상 3000 이하인 직원 정보 출력
SELECT EMPNO, ENAME, SAL
FROM EMP
WHERE SAL >= 2000 AND SAL <= 3000;

Ex. 조건식을 BETWEEN 연산자 사용
SELECT ENPNOM ENAME, SAL
FROM EMP
WHERE BETWEEN 2000 AND 3000;
```

<br>

**LIKE 연산자**
- 정확하게 일치하지 않아도 되는 패턴 조건 전달 시 사용
- %와 _와 함께 사용됨
1) % : 자리수 제한 없는 모든이라는 의미
2) _ : _ 하나 당 한 자리수를 의미하며 모든 값을 표현함

```
Ex. Like 연산자

ENAME LIKE 'S%' : 이름이 S로 시작하는
ENAME LIKE '%S%' : 이름이 S를 포함하는
ENAME LIKE '%S' :  이름이 S로 끝나는
ENAME LIKE '_S%' : 이름의 두 번째 글자가 S인 (맨 앞이 _인것 주의. %이면 자리수 상관없이 S를 포함하기만하면 됨)
ENAME LIKE '__S__' : 이름의 가운데 글자가 S이며 일므의 길이가 5글 자인
```

<br>

**NOT 연산자**
- 조건 결과의 반대집합. 즉, 여집합을 출력하는 연산자
- NOT 뒤에 오는 연산 결과의 반대 집합 출력
- 주로 NOT IN, NOT BETWEEN A AND B, NOT LIKE, NOT NULL 로 사용

```
Ex. NOT 연산자의 사용 01
SELECT EMPNO, ENAME, SAL
FROM EMP
WHERE SAL NOT BETWEEN 1000 AND 3000;
```
> 설명 : 1000 이상 3000이하의 반대 집합 -> 1000미만 또는 3000 초과

<br>
<br>

## 2-5 GROUP BY 절

**GORUP BY 절**
- **각 행을 특정 조건에 따라 그룹으로 분리하여 계산하도록 하는 구문식**
- GROUP BY 절에 그룹을 지정할 컬럼을 전달 (여러 개 전달 가능)
- 만약 그룹 연산에서 제외할 대상이 있다면 미리 WHERE 절에서 해당 행을 제외함
    - (WHERE 절이 GROUP BY 절보다 먼저 수행되므로)
- **그룹에 대한 조건은 WHERE 절에서 사용할 수 없음**
- SELECT 절에 집계 함수를 사용하여 그룹연산 결과 표현
- **GROUP BY 절을 사용하면 데이터가 요약되므로 요약되기 전 데이터와 함께 출력할 수 없음**

**문법**
```
SELECT * | 컬럼명 | 표현식
FROM 테이블명 또는 뷰명
WHERE 조회할 데이터 조건
GROUP BY 그룹핑 컬럼명
HAVING 그룹핑 대상 필터링 조건;
```

Ex. 부서별(DEPARTMENT_ID) 급여 총 합과 급여 평균 출력
```
SELECT DEPARTMENT_ID, SUM(SALARY),
    ROUND(AVG(SALARY))
FROM EMPLOYEES
GROUP BY DEPARTMENT_ID;
```

<br>

Ex. 직군(JOB_ID)별 급여 총 합과 급여 평균 출력
```
SELECT JOB_ID, SUM(SALARY),
    ROUND(AVG(SALARY))
FROM EMPLOYEES
GROUP BY JOB_ID;
```

<br>

**HAVING 절**
- **그룹 함수 결과를 조건으로 사용할 때 사용하는 절**
- WHERE 절을 사용하여 그룹을 제한할 수 없으므로 HAVING 절에 전달
- HAVING 절이 GROUP BY 절 앞에 올 수는 있지만 뒤에 쓰는 것을 권장
- 내부적 연산 순서가 SELECT 절보다 먼저이므로 SELECT 절에서 선언된 Alias 사용 불가

Ex. 그룹 함수 조건을 WHERE 절에 전달하는 경우 발생한 에러
```
SELECT DEPARTMENT_ID,
    SUM(SALARY)
FROM EMPLOYEES
WHERE SUM(SALARY) > 20000
GORUP BY DEPARTMENT_ID;
```

<br>

Ex. 그룹 함수 조건 HAVING 절에 전달
```
SELECT DEPARTMENT_ID,
    SUM(SALARY)
FROM EMPLOYEES
GROUP BY DEPARTMENT_ID
HAVING SUM(SALARY) > 2000;
```

<br>

Ex. WHERE 절과 HAVING 절 동시 사용
```
SELECT DEPARTMENT_ID,
    SUM(SALARY)
FROM EMPLOYEES
WHERE DEPARTMENT_ID IN (10, 30, 40, 110)
GROUP BY DEPARTMENT_ID;
```

> 설명 : **순서상 WHERE 절을 먼저 수행, 원하는 데이터만 필터링 한 후 GROUP BY에 의해 그룹연산을 수행한 뒤 HAVING 절에서 만족하는 데이터만 선택하여 출력함**

<br>
<br>

## 2-6 ORDER BY 절

**ORDER BY 절**
- 데이터는 입력된 순서대로 출력되나, **출력되는 행의 순서를 사용자가 변경하고자 할 때 ORDER BY 절을 사용**
- ORDER BY 뒤에 명시된 컬럼 순서대로 정렬 -> 1차 정렬, 2차 정렬 전달 가능
- 정렬 순서를 오름차순(ASC), 내림차순(DESC)으로 전달 (생략 시 오름차순 정렬)
- 유일하게 SELECT 절에 정의한 컬럼 별칭 사용 가능
- SELECT 절에 선언된 순서대로의 숫자로도 사용 가능

**문법**

```
SELECT * | 컬럼명 | 표현식
FROM 테이븖여 또는 뷰명
WHERE 조회할 데이터 조건
GROUP BY 그룹핑 컬럼명
HAVING 그룹핑 대상 필터렁 조건
ORDER BY 정렬컬럼명 [ASC | DESC];
```

<br>

**정렬 순서(오름차순)**
- 한글 : 가, 나, 다, 라 ...
- 영어 : A, B, C, D ...
- 숫자 1, 2, 3, 4 ...
- 날짜 : 과거 날짜부터 시작해서 최근 날짜로 정렬

<br>

Ex. 문자 정렬 예제
```
SELECT EMPLOYEE_ID, FIRST_NAME, HIRE_DATE
FROM EMPLOYEES
ORDER BY FIRST_NAME;
```

<br>

Ex. 날짜 정렬 (오름차순 : 오래된 순서대로)
```
SELECT EMPLOYEE_ID, FIRST_NAME, HIRE_DATE
FROM EMPLOYEES
ORDER BY HIRE_DATE;
```

<br>

**복합 정렬**
- **먼저 정렬한 값의 동일한 결과가 있을 경우 추가적으로 정렬 가능**
    - 1차 정렬한 값이 같은 경우 그 값 안에서 2차 정렬 컬럼값의 정렬이 일어남

<br>

Ex. 복합정렬 예시
```
SELECT FRIST_NAME, SALARY, HIRE_DATE
FROM EMPLOYEES
WHERE SALARY > 10000 
    AND DEPARTMENT_ID = 90
ORDER BY SALARY DESC, HIRE_DATE ASC;
```

<br>

Ex. 컬럼 별칭을 사용한 정렬
```
SELECT EMPLOYEE_ID AS EID, SALARY, DEPARTMENT_ID
FROM EMPLOYEES E
WHERE DEPARTMENT_ID = 100
ORDER BY EID DESC;
```

> 설명 : **SELECT 절보다 늦게 수행되는 구문은 ORDER BY 절 뿐이므로 ORDER BY 절만 SELECT 절에서 정의된 컬럼 별칭 사용 가능**

<br>
<br>


## 2-7 조인

**JOIN (조인)**
- **여러 테이블의 데이터를 사용하여 동시 출력하거나 참조 할 경우 사용**
- **FROM 절에 조인할 테이블 나열**
- ORALCE 표준은 테이블 나열 순서 중요하지 X, (ANSI 표준은 OUTER JOIN 시 순서 중요)
- WHERE 절에서 조인 조건을 작성 (ORALCE)
- **동일한 열 이름이 여러 테이블에 존재할 경우 열 이름 앞에 테이블 이름이나 테이블 Alias 붙임**
- N 개의 테이블을 조인하려면 최소 N-1 개의 조인 조건이 필요
- ORACLE 표준과 ANSI 표준이 서로 다름

<br>

**조인 종류**
1. **조건의 형태에 따라**  
   1) **EQUI JOIN (등가 JOIN)** : JOIN 조건이 동등 조건인 경우  
   2) **NON EQUI JOIN** : JOIN 조건이 동등 조건이 아닌 경우  

2. **조인 결과에 따라**  
    1) **INNER JOIN** : JOIN 조건에 성립하는 데이터만 출력하는 경우  
    2) **OUTER JOIN** : JOIN 조건에 성립하지 않는 데이터도 출력하는 경우  
    (LEFT/RIGHT/FULL OUTER JOIN)

3. **NATURAL JOIN** : 조인조건 생략 시 두 테이블에 같은 이름으로 자연 연결되는 조인
4. **CROSS JOIN** : 조인조건 생략 시 두 테이블의 발생 가능한 모든 행을 출력하는 조인
5. **SELF JOIN** : 하나의 테이블을 두 번 이상 참조하여 연결하는 조인

<br>

**EQUI JOIN (등가 JOIN)**
- **조인 조건이 '='(equal) 비교를 통해 같은 값을 가지는 행을 연결하여 결과를 얻는 조인 방법**
- SQL 명령문에서 가장 많이 사용하는 조인 방법
- FROM 절에 조인하고자 하는 테이블을 모두 명시
- FROM 절에 명시하는 테이블은 모두 별칭(Alias) 사용 가능
- WHERE 절에 두 테이블의 공통 컬럼에 대한 조인 조건을 나열

**문법**
```
SELECT 테이블1.컬럼, 테이블2.컬럼
FROM 테이블1, 테이블2
WHERE 테이블1.컬럼 = 테이블2.컬럼;
```

<br>

Ex. EMP 테이블과 DEPT 테이블을 사용하여 각 직원의 이름과 부서명을 함께 출력
```
SELECT E.DEPTNO, D.ENAME,
FROM EMP E, DEPT D 
WHERE E.DEPTNO = D.DEPTNO;
```
<br>

**NON-EQUI JOIN**
- 테이블을 연결짓는 조인 컬럼에 대한 **비교 조건이 '<', BETWEEN A AND B 와 같이 '=' 조건이 아닌 연산자를 사용**하는 경우의 조인 조건

**문법**
```
SELECT 테이블1.컬럼, 테이블2.컬럼
FROM 테이블1, 테이블2
WHERE 테이블1.컬럼 비교조건 테이블2.컬럼;
```
Ex. EMP 테이블의 급여를 확인하고 SAL_GRADE에 있는 급여 등급 기준에 따라 직원 이름과 급여, 급여등급 출력
```
SELECT E.ENAME, E.SAL, S.GRADE
FROM EMP E, SALGRADE S
WHERE E.SAL BETWEEN S.LOSAL AND HISAL;
```

<br>

**세 테이블 이상의 조인**
- 관계를 잘 파악하여 모든 테이블이 연결되도록 조인 조건 명시
- N 개 테이블의 경우 최소 N-1 개의 조인 조건 필요

Ex. EMPLOYEES, DEPARTMENTS, LOCATIONS 테이블 조인

```
SELECT *
FROM EMPLOYEES E, DEPARTMENTS D, LOCATIONS L
WHERE E.DEPARTMENT_ID = D.DEPARTMENT 
    AND D.LOCATION_ID = L.LOCATION_ID;

```


**SELF JOIN**
- 한 테이블 내 각 행끼리 관계를 갖는 경우 조인 기법
- 한 테이블을 참조할 때마다(필요할 때마다) 명시해야 함
- 테이블명이 중복되므로 반드시 테이블 별칭 사용

Ex. EMPLOYEES 테이블에서의 각 직원 이름과 매니저 이름을 함께 출력
```
SELECT E1.EMPLOYEE_ID, E1.FIRST_NAME, E1.LAST_NAME, E1.MANAGER_ID, E2.EMPLOYEE_ID, E2.FIRST_NAME , E2.LAST_NAME
FROM EMPLOYEES E1, EMPLOYEES E2
WHERE E1.MANAGER_ID = E2.EMPLOYEES
```

<br>
<br>


## 2-8 표준 조인

**표준 조인**
- ANSI 표준으로 작성되는 INNER JOIN, CROSS JOIN, NATURAL JOIN, OUTER JOIN을 말함

<br>

**INNER JOIN**
- 내부 조인이라고 하며, 조인 조건이 일치하는 행만추출 (ORACLE 조인 기본)
- ANSI 표준의 경우 FROM 절에 INNER JOIN 혹은 줄여서 JOIN을 명시
- ANSI 표준의 경우 **USING 이나 ON 조건절을 필수적으로 사용

<br>

**ON 절**
- 조인할 양 컬럼의 컬럼명이 서로 다르더라도 사용 가능
- **ON 조건의 괄호는 옵션(생략 가능)**
- 컬럼명이 같을 경우 테이블 이름이나 별칭을 사용하여 명확하게 지정 (테이블 출처 명확히)
- ON 조건절에서 조인조건 명시, WHERE 절에서는 일반조건 명시 (WHERE 절과 ON 절을 쓰임에 따라 명확히 구분)

<br>

**문법**
```
SELECT 테이블1.컬럼명, 테이블2.컬럼명
FROM 테이블1 INNER JOIN 테이블2
ON 테이블1.조인컬럼 = 테이블2.조인컬럼;
```

Ex. EMP 테이블과 DEPT 테이블을 사용하여 각 직원의 이름과 부서명을 함께 출력 (EQUI JOIN)
```
SELECT E.ENAME, D.DNAME
FROM EMP E JOIN DEPT D
ON E.DEPTNO = D.DEPTNO
```

<br>

**USING 조건절**
- 조인할 컬럼명이 같을 경우 사용
- **Alias 나 테이블 이름 같은 접두사 붙이기 불가**
- **괄호 필수**

<br>

**문법**
```
SELECT 테이블1.컬럼명, 테이블2.컬럼명
FROM 테이블1 INNER JOIN 테이블2
USING (동일한컬럼명);
```

Ex. USING 절을 이용한 사원이름과 부서이름 조회
```
SELECT E.ENAME, D.DNAME
FROM EMP E JOIN DEPT D
USING (DEPTNO);
```

<br>

**NATURAL JOIN**
- 두 테이블 간의 **동일한 이름을 가지는 모든 컬럼들에 대해 EQUI JOIN을 수행**
- **USING, ON, WHERE 절에서 조건 정의 불가**
- JOIN에 사용된 컬럼들은 **데이터 유형이 동일해야 하며 접두사를 사용불가**

<br>

**문법**
```
SELECT 테이블1.컬럼명, 테이블2.컬럼명
FROM 테이블1 NATURAL JOIN 테이블2;
```

Ex. NATURAL 조인을 이용한 사원 이름, 부서명 출력
```
SELECT E.NAME, D.NAME
FROM EMP E NATURAL JOIN DEPT D
```

Ex. NATURAL JOIN 시 주의
```
SELECT *
FROM STUDENT NATURAL JOIN PROFESSOR;
```

> 중복된 열: NATURAL JOIN에서 *을 사용하면 동일한 이름을 가진 열이 중복될 수 있으며, 이로 인해 결과가 복잡하거나 읽기 어려울 수 있습니다.
> 빈 집합: 공통 열이 없는 경우, 조인 결과가 빈 집합이 될 수 있습니다.


<br>

**CROSS 조인**
- 테이블 간 **JOIN 조건이 없는 경우 생성 가능한 모든 데이터들의 조합 (Cartesian product, 카타시안 곱) 출력**
- 양쪽 테이블 행의 수의 곱한 수의 데이터 조합 발생 (m * n)

<br>

**문법**
```
SELECT 테이블1.컬럼명, 테이블2.컬럼명
FROM 테이블1 CROOS JOIN 테이블2
```

Ex. CROSS 조인 예시
```
SELECT E.ENAME, D.DNAME
FROM EMP E CROSS JOIN DEPT D; 
```

> 설명 : 예를 들어, EMP 테이블 4건, DEPT 테이블 4건 이라면 4 * 4 = 16의 결과가 출력됨

<br>

**OUTER JOIN**
- INNER JOIN 과 대비되는 조인방식
- JOIN 조건에서 동일한 값이 없는 행도 반환할 때 사용
- 두 테이블 중 한쪽에 NULL을 가지면 EQUI JOIN 시 출력되지 않음 -> 이를 출력 시 OUTER JOIN 사용
- 테이블 기준 방향에 따라 LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN 으로 구분



**OUTER JOIN 종류**
1) LEFT OUTER JOIN
   - FROM 절에 나열된 왼쪽 테이블에 해당하는 데이터를 읽은 후, 우측 테이블에서 JOIN 대상 읽어옴
   - 즉, **왼쪽 테이블이 기준**이 되어 오른쪽 데이터를 채우는 방식
   - **우측 값에서 같은 값이 없는 경우 NULL 값으로 출력**

2) RIGHT OUTER JOIN
    - LEFT OUTER JOIN의 반대
    - 즉, **오른쪽 테이블 기준**으로 왼쪽 테이블 데이터를 채우는 방식
    - FROM 절에 테이블 순서를 변경하면 LEFT OUTER JOIN 으로 수행 가능

3) FULL OUTER JOIN
    - 두 테이블 전체 기준으로 결과를 생성하여 중복 데이터는 삭제 후 리턴
    - LEFT OUTER JOIN 결과와 RIGHT OUTER JOIN 결과의 UNION 연산 리턴과 동일함
    - ORACLE 표준에는 없음

<br>

Ex. LEFT OUTER JOIN

ORACLE
```
SELECT * 
FROM STUDNET S, PROFESSOR P
WHERE S.PROFNO = P.PROFNO(+)
    AND S.GRADE IN (1,4);
```

<br>

ANSI
```
SELECT S.STUDNO, S.NAME AS 학생명, S.GRADE, S.PROFNO, P.PROFNO, P.NAME AS 교수명
FROM STUDENT S LEFT OUTER JOIN PROFESSOR P
    ON S.PROFNO = P.PROFNO
WHERE S.GRADE IN (1,4);
```

<br>

Ex. FULL OUTER JOIN

ORACLE
```
SELECT S.STUDNO, S.NAME AS 학생명, S.GRADE, S.PROFNO, P.PROFNO, P.NAME AS 교수명
FROM STUDENT S, PROFESSOR P
WHERE S.PROFNO = P.PROFNO(+)
UNION
SELECT S.STUDNO, S.NAME AS 학생명, S.GRADE, S.PROFNO, P.PROFNO, P.NAME AS 교수명
FROM STUDENT S, PROFESSOR P
WHERE S.PROFNO(+) = P.PROFNO
```

<br>

ANSI
```
SELECT S.STUDNO, S.NAME AS 학생명, S.GRADE, S.PROFNO, P.PROFNO, P.NAME AS 교수명
FROM STUDENT S FULL OUTER JOIN PROFESSOR P
    ON S.PROFNO = P.PROFNO;
```

<br>
<br>

