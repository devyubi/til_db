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

### 6.2 posts 테이블 만들기 ( CRUD )

- `게시글 (posts)` 이라는 테이블 만들기
  - id : 자동증가 (AI), PK
  - title : 255 字
  - content : 3000 字
  - `authors_id : FK`

```sql
-- 게시글 ( posts ) table 만들기
create table posts(
	id int,
    title varchar(255),
    content varchar(3000),
    authors_id int not null,
    primary key (id),
    foreign key (authors_id) references authors(id)
); /* references : 참조하다, ctrl + Enter */

describe posts; /* ctrl + Enter */
```

### 6.3 테이블명 변경하기

- 하단 바꾸고 싶은 테이블명 변경 예시

```sql
-- ALTER TABLE 테이블명 RENAME 테이블명;

USE 데이터베이스명; /* ctrl + Enter */
ALTER TABLE posts RENAME post; /* ctrl + Enter */
show tables; /* ctrl + Enter */
```

### 6.4 테이블에 컬럼 추가/삭제하기

- 컬럼 추가하기

```sql
-- USE 데이터베이스명; /* ctrl + Enter */
-- 반드시 테이블 확인하고 실행해야함
-- DESCRIBE 테이블명;
-- ALTER TABLE 테이블명 ADD 컬럼명 데이터타입;

alter table authors add age int; /* ctrl + Enter */

describe authors; /* ctrl + Enter */
```

- 컬럼 삭제하기

```sql
-- USE 데이터베이스명; /* ctrl + Enter */
-- 반드시 테이블 확인하고 실행해야함
-- DESCRIBE 테이블명;
-- ALTER TABLE 테이블명 DROP 컬럼명;

alter table authors drop age; /* ctrl + Enter */

describe authors; /* ctrl + Enter */
```

### 6.5 테이블에 컬럼 변경하기

```sql
-- USE 스키마(데이터베이스)명; /* ctrl + Enter */
-- 컬럼 변경하기
-- ALTER TABLE 테이블명 CHANGE COLUMN 컬럼명 새컬럼명 데이터타입

alter table posts change column content contents varchar(3000); /* ctrl + Enter */
describe posts; /* ctrl + Enter */
```

### 6.6 특정 컬럼의 속성 변경하기

```sql
-- USE 스키마(데이터베이스)명; /* ctrl + Enter */
-- DESCRIBE 스키마(데이터베이스)명;
-- ALTER TABLE 테이블명 MODIFY COLUMN 컬럼명 데이터타입;
-- DESCRIBE 테이블명;

describe authors;
-- 컬럼 변경 시 반드시 데이터 타입이 있어야 함

alter table authors modify column email varchar(30) not null;

describe authors;
```

### 6.7 데이터 추가하기 ( insert )

- DML : 추가( insert ), 수정( update ), 삭제( delete )

```sql
-- USE 데이터베이스명;
-- DESCRIBE 테이블명;
-- 데이터 추가
-- INSERT INTO 테이블명 (칼럼1, 칼럼2, 칼럼3) VALUES (값1, 값2, 값3); // 값이 여러개면 value`s`
-- 데이터 입력 결과 확인하기 (전체 확인)

use board;
describe authors;
insert into authors (id, name, email) values (1, "홍길동", "hong@a.com");
select * from authors;
```

### 6.8 `authors 테이블의 id 가 1 인 데이터` 를 `posts 테이블에 추가`하기

- FK 가 있는 경우

```sql
-- FK 가 있는 경우
describe posts;

insert into posts (id, title, contents, authors_id) values (1, "제목", "내용1", 1);
select * from posts;
describe posts;
```

- FK 가 없을 경우

```sql
-- INSERT INTO 테이블명 (컬럼명, 컬럼명, ...) VALUES (값, 값, ...);
-- FK 에 없는 사용자 id 를 넣는다면 ?

insert into posts (id, title, contents, authors_id) values (2, "제목2", "내용2", 1);
-- insert into posts (id, title, contents, authors_id) values (2, "제목2", "내용2", 2); // 해당 코드는 오류.
insert into posts (id, title, contents, authors_id) values (3, "제목3", "내용3", 1);

select * from posts;
```

### 6.9 데이터 수정 ( update )

- 반드시 조건절이 있어야함 ( `조건절이 없으면 전체 모든 데이터가 수정됨` )
- `WHERE 조건` 을 누락하게 되는 경우, 모든 데이터가 수정됨.
- 필수 주의 사항 : 기존 프로그래머들
  - `==` 을 사용하지 않음. 즉, sql 에서는 같다는 표현이 아님.
  - `=` 을 사용하여 같다, 즉 비교함.

```sql
-- UPDATE 테이블명 SET 칼럼명 = 값, 칼럼명 = 값 WHERE 조건
-- UPDATE 테이블명 SET 칼럼명 = 값, 칼럼명 = 값 WHERE 필드이름=값;

update authors set email = "hong@gmail.com" where id=1;

select * from authors;
```

### 6.10 데이터 삭제 (delete)

- 퇴사당함
- `WHERE 를 반드시 사용함`

```sql
-- DELETE FROM 테이블명 WHERE 조건;
-- DELETE FROM 테이블명 WHERE 필드이름=값;

-- 사용자 한명을 추가 후 삭제
describe authors; /* ctrl + Enter */

insert into authors (id,name,email,password) values (2,"유비","b@b.com",1234); /* ctrl + Enter */
insert into authors (id,name,email,password) values (3,"소정","c@c.com",1234); /* ctrl + Enter */
insert into authors (id,name,email,password) values (4,"깜찍","d@d.com",1234); /* ctrl + Enter */
insert into authors (id,name,email,password) values (5,"둘리","e@e.com",1234); /* ctrl + Enter */

select * from authors; /* ctrl + Enter */

delete from authors where id=2; /* ctrl + Enter */
-- 아이디 2번 유저를 삭제함
select * from authors; /* ctrl + Enter */
```

### 6.11 테이블의 모든 데이터 삭제하기

- `DELETE FROM 테이블명`

  - 데이터를 지우고 테이블은 남겨둠 ( TRUNCATE, DROP 은 x. 테이블 전체를 날리는 것 )
  - `복구 가능`
  - storage 에 자료는 파일 형태로 남아있음

- `TRUNCATE TABLE 테이블명`

  - 데이터도 지우고 테이블도 지움
  - 테이블 구조(스키마)는 남기고, 데이터만 전부 삭제
  - DELETE보다 훨씬 빠름 (로그를 최소한만 남기기 때문)
  - 자동 증가값 (AUTO_INCREMENT) 초기화

  - `복구 불가능` / ROLLBACK 불가 (복구 힘듦)

- `DROP TABLE 테이블명`
  - 데이터 삭제, 테이블 구조도 삭제함, `복구 불가`

### 6.12 데이터 조회 ( Select ) ※ 매우 중요 ※

- 개발자가 가장 많이 사용함
- 특정한 데이터에서 원하는 결과를 도출해 내는 작업
- `알고리즘 시험에 늘 나옴`

- 모든 데이터 조회 하기

```sql
-- SELECT * FROM 테이블명;
SELECT * FROM authors;
```

### 6.13 WHERE 절을 이용해 원하는 데이터 출력하기

- PK 를 이용해 데이터 추출하기 ( 유일한 값 )

```sql
select * from authors where id=1;
```

- 문자열 비교는 반드시 `작은 따옴표` 를 사용

```sql
select * from authors where name = '유비';
```

- 숫자는 비교시 =, >, <, >=, <= 가능

```sql
select * from authors where id >= '1';
```

- WHERE 조건이 2개 이상이면 `AND` 를 사용

```sql
select *
from authors
where id > '1' and password = '1234';

select *
from authors
where id > '1' and email = 'd@d.com';
```

- 특정 항목만 조회하기

```sql
select name
from authors;

select name, email
from authors;

select name
from authors
where name = '유비';
```

- 오름차순 정렬로 조회하기 ( PK 를 기준으로 함 )

```sql
-- 아이디를 기준으로 정렬
select * from authors
order by id;

-- 오름차순
select * from authors
order by id asc;

-- 내림차순 ( 예를 들면 최근 글일 시 해당 코드 이용함 )
select * from authors
order by id desc;

-- 오름차순 : 이름 ( 가나다 순서 )
select * from authors
order by name;

-- 내림차순 : 이름 ( ㅎ 부터 출력 )
select * from authors
order by name desc;
```

- 여러 칼럼을 정렬함 ( 앞쪽 출력 후 뒤쪽 출력 )

```sql
select * from authors order by name desc;

select * from authors order by name desc, email desc;
```

- 조회 갯수를 제한하기 ( limit )

```sql
select * from authors limit 2;

select *
from authors
where password = '1234'
order by id desc
limit 7;
```

- null 을 조회 조건으로 활용

```sql
select *
from authors
where password is null;

select *
from authors
where password is not null;
```

- 코딩테스트 : https://school.programmers.co.kr/learn/challenges?order=recent&page=1&languages=mysql

## 7. 데이터 종류

### 7.1 tinyint

- 컬럼 추가하기
- `-128 ~ -127`

```sql
alter table authors add column age tinyint;
```

### 7.2 int ( 가장 흔히 많이 쓰임 )

- `-20억 ~ 20억`

### 7.3 bigint

- 글로벌 서비스

### 7.4 unsigend

- 양수, 음수를 제외하고 2배로
- `int unsigend` : 40억
- `tintint unsigend` : 0 ~ 255

### 7.5 실수

- `decimal ( m, d )`
- `float`
- `double`

### 7.6 문자 char ( 길이 )

- 길이에는 최대 길이를 작성함
- 설정 길이만큼 공간 차지함
- 검색 속도가 훨씬 빨라서 자주 씀
- 성별, 주민번호, 전화번호 등
- 길이가 정해진 데이터를 정의할 때 자주 쓰임

### 7.7 문자 varchar ( 길이 )

- 웬만하면 varchar 사용
- 길이에는 문자열의 최대 길이를 말함
- 가변 길이로써 딱 글자만큼만 저장함
- 이름, 상품명, 주소 등

### 7.8 문자 text

- 길이 지정 못함
- 가변 적으로 길이 정해짐
- 최대 65536 글자 가능
- 느림

### 7.9 blob

- 바이너리 데이터
- png 등의 이미지를 굳이 보관할 때
- 잘 쓰지 않음

### 7.10 enum

- 미리 들어갈 수 있는 특정 데이터의 목록 값을 지정함

```sql
ALTER TABLE author ADD COLUMN role ENUM('admin', 'user') not null default 'user';
```

### 7.11 날짜 date

- 날짜만 저장 가능 ( YYYY-MM-DD )
- 생년월일

### 7.12 날짜 datetime ( 가장 많이 사용함 )

- 날짜, 시간을 저장함
- 옵션을 주면 m 지정 시 소수정 microseconds 단위까지 저장함 ( YYYY-MM-DD HH:MM:SS )
- 주문시간, 글 작성 시간 등
- `칼럼명 datetime default current_timestamp()` : 현재 시간을 기본으로

### 7.13 날짜/시간 now() 함수

- 현재 날짜와 시간을 반환함 

```sql
create table user_Info (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT unique not null,
  pw TEXT,
  nickname TEXT,
  birth DATE,
  gender TEXT,
  profile_img TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```
