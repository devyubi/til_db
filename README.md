# 데이터베이스의 이해

- 현장에서 대화가 되어야 함
- 특히, BE와 FE가 협업 시 의사소통이 안되면 곤란함

## 1. 데이터베이스 모델링이란?

- 실제 애플리케이션에는 많은 데이터를 관리함
- 데이터를 잘 분류하고, 데이터를 잘 보관해야 함
- 수월하게 데이터를 조회할 수 있어야 함
- 수월하게 데이터를 수정할 수 있어야 함
- 수월하게 데이터를 삭제할 수 있어야 함
- 그래서 어떻게 분류하여, 어떻게 저장하고, 어떻게 관리할 지를 설계하는 행위를 `DB 모델링` 이라 함
- 위의 사항을 줄여서 (회의에서) `데이터베이스모델링`, `DB설계` 라고 칭함

## 2. 데이터베이스 모델링을 배우면 좋은 점

- 협업이 수월해짐
- Entity Relation Diagram (ERD) 을 볼 수 있음
- 효율적으로 데이터를 저장하는 것에 대한 고민을 하게 됨
- BE 개발자는 정말 많은 데이터를 관리함 (BE 개발자는 DB 설계를 필수로 알아야함)
- FE 개발자도 현재는 필수 교양임 (취업 요구 사항)

## 3. 관계형 데이터베이스 관리 시스템

- RDBMS (Relation DataBase Manage Systems)
- 관계형이란 `데이터 표`와 `데이터 표`의 연결을 관리
- 대표적인 도구 : MySQL (유료-Oracle이 매입함), MariaDB (무료-MySQL과 같음-MySQL 개발자중 한명이 회사 나와서 만듬), Oracle, PostgreSQL (SupaBasesms PostgreSQL 기반의 SQL 데이터베이스를 사용), SQLite 등
- SQL 언어는 엑셀의 표와 같음. 즉, `테이블`에 데이터를 관리함
- NoSQL 언어는 son 형태. 즉, `문서`에 데이터를 관리함 (대표적인 도구 : FireBase, MongoDB)

## 4. 테이블에 대한 이해

- 테이블은 엑셀의 `표` 라고 생각하면 쉬움
- 회원 테이블 만들기
- 제품 테이블 만들기

- 예제: https://docs.google.com/spreadsheets/d/1PjX6Sepcg3nVyHcGmYTeMgkz_9uw-6aZZbLbqfhALtU/edit?usp=sharing

## 4.1 기본키(Primary Key)

- 흔히 `PK` 라고 하면 의사소통 됨
- 수 많은 데이터를 구별해 주기 위해서 기본키가 필요함
- 절대 `중복되면 안됨`, `값이 비어서도 안됨`
- `Auto increment` 옵션을 주어서, 1씩 자동 증가 또는 UUID 로 랜덤 값으로 세팅함
- 컬럼명을 `id` 또는 `uid`라고 하는 경우가 많음

### 4.2 외래키(Foreign Key)

- `FK` 라고 통상 칭함
- `게시글 테이블`과 `사용자 테이블` 생성
- 예제:
- 요약: 다른 테이블의 데이터와 관계를 연결 시키는 키를 말함
- 장점: 잘못된 FK(외래키)를 연결하면 오류를 일으켜줌
- 데이터가 오류가 없음을 BE 개발자들은 `참조 무결성` 이라고 칭함

## 5. 데이터베이스의 네이밍 규칙

### 5.1 반드시 테이블명 및 컬럼명은 소문자로 작성한다

- 이유: 운영체제에서는 대, 소문자를 구별하는 경우와 그렇지 않은 경우에 존재함
- 운영체제와 상관없도록 반드시 `소문자`를 규칙으로 하면 좋음

### 5.2 snake_case 를 사용함

- table 명, 컬럼명을 여러 단어로 작성할때 `소문자_소문자` 로 작성

```text
userName   // 안좋은 예시
user_name  // 좋은 예시
```

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

### 5.3 축약어를 사용하지 않는다

- 여러 명이서 DB를 관리함
- 규칙을 지키는 것을 신경써야함
- 직관적일수록 업무 진행이 원할함

```text
u_name    // 안좋은 예시
user_name // 좋은 예시
```

### 5.4 SQL 명령어만 `대문자로` 사용함

- 실제로 sql 명령어는 대,소문자를 구별하지 않음
- 가독성을 위해서 대문자를 활용함
- 아래는 소문자로 구성 된 코드

```sql
select name, age
from users
where age = 20
and name = "홍길동";
```

- 아래는 대,소문자로 구성 된 코드

```sql
SELECT name, age
FROM users
WHERE age = 20
AND name = "홍길동";
```

### 5.5 테이블의 이름을 지을 때는 가능하면 복수형을 선택하자 (권장 사항)

- 데이터가 여러개 임을 의미해 줌
- 회사마다 다름. 하지만 지켜주면 `일관성` 을 유지해 주자 (섞어서 이름 짓지 말자)
- 실습은 `복수형` 으로 진행함

```text
user
users

post
posts
```
