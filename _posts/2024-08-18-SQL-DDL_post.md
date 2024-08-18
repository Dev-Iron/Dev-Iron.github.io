---
title: 데이터 정의어 (DDL, Data Definition Language) 란?
date: 2024-08-11 20:00:00 +09:00
categories: [DBMS]
tags: [sql, db, dbms, ddl]     # TAG names should always be lowercase
---


## 데이터 정의어 (DDL, Data Definition Language)란?
**데이터 정의어(DDL, Data Definition Language)**는 데이터베이스의 구조를 정의하거나 수정, 삭제하는 데 사용되는 SQL 명령어들의 집합입니다. DDL은 테이블, 인덱스, 뷰, 스키마와 같은 데이터베이스 객체를 생성하거나 변경하고, 삭제하는 작업을 수행합니다. DDL 명령어는 데이터베이스의 기본 구조를 정의하므로, 데이터베이스를 설계하거나 유지 관리할 때 필수적입니다.

<br>
<br>


##  DDL의 사용 의도
DDL은 데이터베이스의 기본 구조를 설정하고 관리하는 데 사용됩니다. 데이터베이스를 처음 설계할 때 테이블이나 인덱스, 뷰 등을 정의해야 하며, 필요에 따라 이 구조를 변경하거나 삭제할 수도 있습니다. DDL 명령어는 이러한 작업을 가능하게 하며, 데이터의 저장, 검색, 관리가 효율적으로 이루어질 수 있도록 데이터베이스의 구조를 적절히 설계하고 유지보수하는 데 필수적입니다.

- **데이터베이스 설계** : DDL은 데이터베이스의 초기 설계 단계에서 테이블, 인덱스, 뷰 등을 정의하는 데 사용됩니다.
- **데이터 구조 수정** : 시스템의 요구 사항이 변경될 때, 기존 데이터 구조를 수정하기 위해 DDL을 사용합니다.
- **불필요한 데이터 제거** : 더 이상 필요 없는 데이터베이스 객체를 삭제하여 시스템을 정리하고 유지보수하는 데 DDL을 사용합니다.

<br>
<br>

## DDL의 종류
DDL은 데이터베이스 구조를 관리하기 위한 다양한 명령어를 제공합니다. 주요 DDL 명령어는 다음과 같습니다:

- **CREATE** : 데이터베이스 객체를 생성합니다. 예를 들어, 새로운 테이블, 인덱스, 뷰를 만들 수 있습니다.
- **ALTER** : 기존 데이터베이스 객체를 수정합니다. 예를 들어, 테이블에 새로운 컬럼을 추가하거나 인덱스를 변경할 수 있습니다.
- **DROP** : 데이터베이스 객체를 삭제합니다. 테이블, 인덱스, 뷰 등을 삭제하여 더 이상 사용하지 않게 할 수 있습니다.
- **TRUNCATE** : 테이블의 모든 데이터를 삭제하지만, 테이블의 구조와 정의는 유지됩니다. 대량의 데이터를 신속하게 삭제할 때 사용됩니다.

<br>
<br>

## DDL 문법의 구조
DDL 명령어는 비교적 간단한 구조를 가지고 있으며, 명령어와 데이터베이스 객체의 이름, 필요한 경우 추가적인 옵션으로 구성됩니다.

### CREATE 문법 구조

    ```
    CREATE TABLE 테이블명 (
        컬럼명 데이터타입 [제약조건]
    );
    ```

    <br>

    ```
    Ex. 
    CREATE TABLE TBL_MEMBER (
        MEMBER_ID INT AUTO_INCREMENT PRIMARY KEY,
        MEMBER_NAME VARCHAR(255) NOT NULL,
        MEMBER_NICKNAME VARCHAR(255) NOT NULL UNIQUE,
        MEMBER_EMAIL VARCHAR(255) NOT NULL UNIQUE,
        MEMBER_PASSWORD VARCHAR(255) NOT NULL,
    );
    ```

MEMBER 테이블을 생성하며, 'MEMEBER_ID', 'MEMBER_NAME', 'MEMBER_NICKNAME', 'MEMBER_EMAIL', 'MEMBER_PASSWORD' 다섯 개의 컬럼을 정의합니다. MEMBER_ID는 기본 키로 설정되어 고유한 값만 가질 수 있습니다.

<br>
<br>

### ALTER 문법 구조

    ```
    컬럼 추가
    ALTER TABLE 테이블명
        ADD 컬럼명 데이터타입 [제약조건];
        
    컬럼명 변경
    ALTER TABLE 테이블명 
        CHANGE 변경할컬럼명 변경할이름 타입;

    컬럼 타입 변경
    ALTER TABLE 테이블명
        MODIFY 변경할컬럼 변경할타입;

    컬럼 삭제
    ALTER TABLE 테이블명
        DROP COLUMN 컬럼명;
    ```

    <br>

    ```
    Ex.
    ALTER TABLE TBL_MEMBER
        ADD PHONENUMBER VARCHAR(100) UNIQUE DEFAULT '000-0000-0000' NOT NULL;

    ALTER TABLE TBL_MEMBER
        CHANGE MEMBER_NAME M_NAME VARCHAR(150);

    ALTER TABLE TBL_MEMBER
        MODIFY MEMBER_NAME VARCHAR(100);

    ALTER TABLE TBL_MEMBER
        DROP COLUMN MEMBER_NICKNAME;
    ```

'TBL_MEMBER' 테이블에 'PHONENUMBER' 새로운 컬럼을 추가합니다.
'TBL_MEMBER' 테이블의 'MEMBER_NAME' 컬럼명을 'M_NAME'으로 변경합니다.
'TBL_MEMBER' 테이블에서 'MEMBER_NAME' 컬럼 타입을 VARCHAR(100)으로 변경합니다.
'TBL_MEMBER' 테이블에서 'MEMBER_NICKNAME'의 컬럼을 삭제합니다.

<br>
<br>


### DROP 문법 구조


    ```
    DROP TABLE 테이블명;

    DROP INDEX 인덱스명;

    DROP VIEW 뷰명;
    ```

    <br>

    ```
    EX.
    DROP TABLE TBL_NOTICE;

    DROP INDEX INDEX_MEMBER;

    DROP VIEW VIEW_BOARD;
    ```

테이블 'TBL_NOTICE'를 삭제합니다.
인덱스 'INDEX_MEMBER'를 삭제합니다.
뷰 'VIEW_BOARD'를 삭제합니다.

<br>
<br>


### TRUNCATE 문법 구조

    ```
    TRUNCATE TABLE 테이블명;
    ```

    <br>


    ```
    EX.
    TRUNCATE TABLE BOARD
    ```

'BOARD' 테이블에 저장된 모든 데이터를 한 번에 삭제합니다.
