---
title: 데이터 조작어 (DML, Data Manipulation Language) 란?
date: 2024-08-11 20:05:00 +09:00
categories: [DBMS]
tags: [sql, db, dbms, dml]     # TAG names should always be lowercase
---

## 데이터 조작어 (DML, Data Manipulation Language)란?
**데이터 조작어(DML, Data Manipulation Language)**는 데이터베이스 내에서 데이터를 삽입, 수정, 삭제 및 조회하는 데 사용되는 SQL 명령어들의 집합입니다. DML은 데이터베이스에 저장된 데이터를 직접적으로 다루는 역할을 하며, 사용자가 데이터를 어떻게 관리할지 결정하는 데 중요한 역할을 합니다. DML 명령어는 데이터베이스와의 상호작용을 통해 데이터를 처리하고, 이 데이터는 다양한 애플리케이션에서 활용됩니다.

<br>
<br>

## DML의 사용 의도
DML은 데이터베이스 내의 데이터를 조작하고 관리하는 데 사용됩니다. 이를 통해 사용자는 데이터를 추가, 수정, 삭제하거나 필요한 정보를 조회할 수 있습니다. DML은 데이터베이스에서 데이터를 직접적으로 다루기 때문에, 애플리케이션의 핵심 로직에서 자주 사용됩니다.

- **데이터 조회** : 사용자가 필요로 하는 데이터를 검색하고 결과를 반환하기 위해 DML의 SELECT 명령어를 사용합니다.
- **데이터 삽입** : 새로운 데이터를 데이터베이스에 추가할 때 DML의 INSERT 명령어를 사용합니다.
- **데이터 수정** : 기존 데이터의 내용을 변경해야 할 때 DML의 UPDATE 명령어를 사용합니다.
- **데이터 삭제** : 더 이상 필요 없는 데이터를 삭제할 때 DML의 DELETE 명령어를 사용합니다.

<br>
<br>

## DML의 종류
DML은 데이터베이스 내에서 데이터를 조작하기 위한 다양한 명령어를 제공합니다. 주요 DML 명령어는 다음과 같습니다:

- **SELECT** : 데이터베이스에서 데이터를 조회합니다. 데이터를 검색하여 특정 조건에 맞는 데이터를 가져올 때 사용됩니다.
- **INSERT** : 새 데이터를 테이블에 삽입합니다. 새로운 레코드를 추가할 때 사용됩니다.
- **UPDATE** : 기존 데이터를 수정합니다. 테이블 내의 데이터를 변경할 때 사용됩니다.
- **DELETE** : 테이블에서 데이터를 삭제합니다. 특정 조건에 맞는 데이터를 제거할 때 사용됩니다.

<br>
<br>

## DML 문법의 구조
DML 명령어는 데이터 조작의 구체적인 작업을 수행하기 위한 문법 구조를 가집니다. 각 명령어는 목적에 따라 다르며, 조건절이나 정렬 옵션 등을 추가하여 더욱 세부적으로 데이터를 다룰 수 있습니다.


### SELECT 문법 구조

```
SELECT 컬럼명1, 컬럼명2, ...
FROM 테이블명
WHERE 조건
ORDER BY 컬럼명 [ASC | DESC];
```

<br>

```
Ex.
SELECT * 
FROM TBL_MEMBER
WHERE M_NAME = '일일삼';
```

'TBL_MEMBER' 테이블에서 'M_NAME'이 '일일삼'인 모든 행(row)을 조회합니다.

<br>
<br>

### INSERT 문법 구조

```
INSERT INTO 테이블명 (컬럼명1, 컬럼명2, 컬럼명3, ...)
VALUES (값1, 값2, 값3, ...);
```

<br>

```
Ex.
INSERT INTO TBL_MEMBER (PHONENUMBER, NICKNAME, AGE)
VALUES ('010-1234-5678', '일일삼', 27);
```

'TBL_MEMBER' 테이블에 'PHONENUMBER'가 '010-1234-5678', NICKNAME이 '일일삼', AGE가 27인 새로운 행을 추가합니다.

<br>
<br>

### UPDATE 문법 구조

```
UPDATE 테이블명
SET 컬럼명1 = 값1, 컬럼명2 = 값2, ...
WHERE 조건;
```

<br>

```
Ex.
UPDATE TBL_MEMBER
SET NICKNAME = 'IRON'
WHERE MEMBER_ID = 1;
```

'TBL_MEMBER' 테이블에서 'MEMBER_ID'가 1인 행의 'NICKNAME'을 'IRON'으로 변경합니다.

<br>
<br>

### DELETE 문법 구조

```
DELETE FROM 테이블명
WHERE 조건;
```

<br>

```
Ex.
DELETE FROM TBL_BOARD
WHERE BOARD_ID = 1;
```

'TBL_BOARD' 테이블에서 'BOARD_ID'가 1인 행을 삭제합니다.
