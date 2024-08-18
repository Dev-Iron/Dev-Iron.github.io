---
title: 데이터 제어어 (DCL, Data Control Language) 란?
date: 2024-08-11 20:10:00 +09:00
categories: [DBMS]
tags: [sql, db, dbms, dcl]     # TAG names should always be lowercase
---


## 데이터 제어어 (DCL, Data Control Language) 이란?
**데이터 제어어(DCL, Data Control Language)**은 데이터베이스 내의 권한을 관리하고, 데이터 보안 및 무결성을 유지하는 데 사용되는 SQL 명령어들의 집합입니다. DCL은 데이터베이스 사용자들에게 특정 작업을 수행할 수 있는 권한을 부여하거나 회수하는 기능을 제공합니다. 이를 통해 데이터에 대한 접근을 제어하고, 데이터베이스의 보안을 강화할 수 있습니다.

<br>
<br>


## DCL의 사용 의도
DCL 명령어는 데이터베이스 관리자가 데이터베이스의 보안을 강화하고, 사용자의 접근을 제어하기 위해 사용됩니다. 이 명령어를 통해 데이터베이스 내에서 특정 사용자가 수행할 수 있는 작업을 엄격히 통제할 수 있으며, 민감한 데이터에 대한 접근을 제한하거나 조정할 수 있습니다.

<br>
<br>

### DCL의 종류
DCL의 주요 명령어는 두 가지가 있습니다:

- **GRANT** : 특정 사용자에게 데이터베이스 객체(테이블, 뷰, 스키마 등)에 대한 권한을 부여합니다.
- **REVOKE** : 특정 사용자에게 부여된 권한을 회수합니다.

<br>
<br>


## DCL 문법의 구조


### GRANT 문법 구조

    ```
    GRANT 권한 ON 객체 TO 사용자 [WITH GRANT OPTION];
    ```

    - 권한 : 사용자에게 부여할 권한 (예: SELECT, INSERT, UPDATE, DELETE, ALL 등).
    - 객체 : 권한을 부여할 데이터베이스 객체 (예: 테이블, 뷰, 스키마 등).
    - 사용자 : 권한을 부여받을 사용자 또는 역할.
    - WITH GRANT OPTION : 사용자가 부여받은 권한을 다른 사용자에게 다시 부여할 수 있게 하는 옵션 (선택 사항).

    <br>

    ```
    Ex.
    GRANT SELECT, INSERT ON TBL_MEMBER TO 'user1';
    ```

'TBL_MEMBER' 테이블에 대해 'user1' 사용자에게 'SELECT'(조회) 및 'INSERT'(삽입) 권한을 부여합니다.

<br>
<br>

### REVOKE 문법 구조

    ```
    REVOKE 권한 ON 객체 FROM 사용자;
    ```

    - 권한 : 회수할 권한.
    - 객체 : 권한을 회수할 데이터베이스 객체.
    - 사용자 : 권한을 회수당할 사용자 또는 역할.

    <br>

    ```
    EX.
    REVOKE SELECT ON TBL_MEMBER FROM 'user1';
    ```

'TBL_MEMBER' 테이블에 대해 'user1' 사용자에게 부여된 'SELECT'(조회) 권한을 회수합니다.


