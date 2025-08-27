# MariaDB

- 관계형 DB 관리 : `SQL 문법` 사용
- MySql (유료, MariaDB와 동일 문법), Oracle, PostgreSQL (Supabase) 등
- 비관계형 DB 관리 : `NoSql`
- Firebase, MongoDB, Redis 등

## 1. 설치

- https://mariadb.org/download/?t=mariadb&p=mariadb&r=11.6.2&os=windows&cpu=x86_64&pkg=msi&mirror=blendbyte

## 2. 설치 이후 확인

- `Power Shell` 에서 진행

```bash
mysql --version
```

## 3. Maria DB 서버 접속하기

- `Power Shell` 에서 진행

```bash
  mariadb -u root -p
```

- Enter 키 누르면 비밀번호 입력 창 뜨는데 비밀번호 입력 후 엔터 누르면 접속이 된다

## 4. 다양한 명령어

- `Power Shell` 에서 진행

### 4.1 접속 종료하기

```bash
exit 또는 Ctrl + C 입력
```

```
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

새로운 크로스 플랫폼 PowerShell 사용 https://aka.ms/pscore6

PS C:\Users\user> mysql --version
C:\Program Files\MariaDB 11.4\bin\mysql.exe from 11.4.8-MariaDB, client 15.2 for Win64 (AMD64), source revision c4ed889b74ed95fa8b4eaf96610d4c1480b346a4
PS C:\Users\user> mariadb -u root -p
Enter password: ****
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 11.4.8-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> Ctrl-C -- exit!
Bye
PS C:\Users\user>   mariadb -u root -p
Enter password: ****
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 4
Server version: 11.4.8-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> exit
Bye
PS C:\Users\user>
```

### 4.2 시스템 안에 어떤 데이터베이스가 있는지 파악하기

- SQL 명령어는 대문자

```bash
SHOW DATABASES;
```

```
MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.008 sec)

MariaDB [(none)]>
```

### 4.3 나만의 데이터베이스(Scheme, 스키마) 만들기

```bash
CREATE DATABASE [나만의데이터베이스이름];
CREATE DATABASE board;
```

### 4.4 나만의 데이터 베이스 삭제

```bash
DROP DATABASE board;
```

### 4.5 나만의 데이터베이스 만들고, 사용하기

```bash
CREATE DATABASE board;
SHOW DATABASE board;
USE board;
```

### 4.6 나만의 데이터 베이스 이미 존재하는 TABLE 목록 보기

```bash
SHOW TABLES;
```

### 5. 편리한 도구 workbench 설치하기

- MariaDB는 직접 설치해야함
- [사전설치필요] ( https://12716.tistory.com/entry/MySQL-MySQL-Workbench-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%98%A4%EB%A5%98-%EB%B0%9C%EC%83%9D%EC%8B%9C-%ED%95%B4%EA%B2%B0 )
- https://dev.mysql.com/downloads/workbench/

### 5.1 커넥션을 생성해 준다

### 5.2 Query Editor 가 Power Shell 이라고 생각하자

- 기본은 `SQL 명령어`를 입력하고, `;` 를 입력하고 `ctrl + Enter 키` 로 실행

## 6. 실습

```bash
USE board;
```

### 6.1 author 테이블 만들기

- `작가(authors)` 라는 테이블 만들기
  - id : 자동 증가 및 PK 역할을 함
  - name : 255 字
  - email : 255 字
  - password : 255 字

```sql
use board;
-- 작가 테이블 생성
create table authors(
id int primary key,
name varchar (255),
email varchar (255),
password varchar(255)
);
-- 생성된 테이블의 정보 보기
describe athors;
-- 실행된 테이블 생성 코드 보기
show create table authors;
```


