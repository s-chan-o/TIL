# 디비 기초

## 관계형 DB(RDBMS)와 비관계형 DB(NoSQL)의 차이

### 관계형 DB(RDBMS)

관계형 DB는 **데이터를 테이블 형태로 저장하는 데이터베이스**이다.

```text
User Table
id | name | age
1  | Kim  | 18
2  | Lee  | 19
```

데이터는 행(row)과 열(column)로 구성되며, 테이블 간 관계를 설정할 수 있다.

**특징**

- 정해진 스키마가 있다.
- SQL을 사용한다.
- 테이블 간 관계를 가진다.
- 데이터 정합성과 트랜잭션에 강하다.
- 복잡한 조회와 조인에 유리하다.

**예시**

- MySQL
- PostgreSQL
- Oracle
- MariaDB

### 비관계형 DB(NoSQL)

NoSQL은 **테이블 구조에 고정되지 않고 다양한 형태로 데이터를 저장하는 데이터베이스**이다.

대표적으로 문서(Document), Key-Value, 그래프, 컬럼 기반 구조가 있다.

```json
{
  "id": 1,
  "name": "Kim",
  "age": 18
}
```

**특징**

- 스키마가 유연하다.
- 대량의 데이터 처리와 확장에 유리하다.
- 테이블 조인보다 데이터 중복 저장을 통해 빠르게 조회하는 경우가 많다.
- 구조가 자주 바뀌는 데이터에 적합하다.

**예시**

- MongoDB
- Redis
- Cassandra
- DynamoDB

### 비교

| 구분 | RDBMS | NoSQL |
|---|---|---|
| 저장 구조 | 테이블 | 문서, Key-Value, 그래프 등 |
| 스키마 | 고정적 | 유연함 |
| 조회 방식 | SQL | DB마다 다름 |
| 관계 표현 | 조인 사용 | 중첩 구조 또는 중복 저장 |
| 장점 | 정합성, 트랜잭션, 복잡한 조회 | 확장성, 유연한 구조, 대량 데이터 처리 |
| 단점 | 스키마 변경이 부담될 수 있음 | 복잡한 관계 조회에 불리할 수 있음 |
| 예시 | MySQL, PostgreSQL | MongoDB, Redis |

### 선택 기준

- 데이터 구조가 명확하고 정합성이 중요하다 → `RDBMS`
- 복잡한 조인과 트랜잭션이 중요하다 → `RDBMS`
- 데이터 구조가 자주 바뀐다 → `NoSQL`
- 대량 데이터와 수평 확장이 중요하다 → `NoSQL`
- 캐시나 단순 key-value 저장이 필요하다 → `NoSQL`

### 정리

- RDBMS는 테이블 기반이고, 정합성과 관계 표현에 강하다.
- NoSQL은 다양한 구조를 지원하고, 유연성과 확장성에 강하다.
- 정해진 스키마와 트랜잭션이 중요하면 RDBMS가 적합하다.
- 빠른 확장과 유연한 데이터 구조가 중요하면 NoSQL이 적합하다.

## 기본키와 외래키

### 기본키(Primary Key)

기본키는 **테이블에서 각 행(row)을 유일하게 구분하는 값**이다.

```text
User Table
id | name
1  | Kim
2  | Lee
```

위 테이블에서 `id`는 각 사용자를 구분할 수 있으므로 기본키로 사용할 수 있다.

**특징**

- 중복될 수 없다.
- null이 될 수 없다.
- 한 테이블에서 각 행을 식별하는 기준이다.

### 외래키(Foreign Key)

외래키는 **다른 테이블의 기본키를 참조하는 값**이다.

```text
User Table
id | name
1  | Kim
2  | Lee

Order Table
id | user_id | product
1  | 1       | Book
2  | 2       | Pen
```

`Order Table`의 `user_id`는 `User Table`의 `id`를 참조한다.  
즉, 주문이 어떤 사용자에게 속하는지 나타낸다.

**특징**

- 테이블 간 관계를 연결한다.
- 참조하는 값은 보통 다른 테이블의 기본키이다.
- 잘못된 데이터가 들어가는 것을 막아 데이터 정합성을 지킨다.

### 기본키와 외래키 비교

| 구분 | 기본키 | 외래키 |
|---|---|---|
| 역할 | 행을 유일하게 식별 | 다른 테이블과 연결 |
| 중복 | 불가능 | 가능 |
| null | 불가능 | 설정에 따라 가능 |
| 위치 | 자기 테이블 | 참조하는 쪽 테이블 |

### 정리

- 기본키는 한 테이블에서 각 행을 구분하는 값이다.
- 외래키는 다른 테이블의 기본키를 참조하는 값이다.
- 기본키는 중복과 null이 불가능하다.
- 외래키는 테이블 간 관계를 만들고 데이터 정합성을 유지하는 데 사용된다.

## DDL, DML, DCL, TCL의 차이

SQL 명령어는 역할에 따라 DDL, DML, DCL, TCL로 나눌 수 있다.

### DDL(Data Definition Language)

DDL은 **데이터베이스 구조를 정의하거나 변경하는 명령어**이다.

테이블, 스키마, 인덱스 같은 데이터베이스 객체를 만들거나 수정할 때 사용한다.

**대표 명령어**

- `CREATE`: 객체 생성
- `ALTER`: 객체 수정
- `DROP`: 객체 삭제
- `TRUNCATE`: 테이블 데이터 전체 삭제

```sql
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);
```

### DML(Data Manipulation Language)

DML은 **테이블에 저장된 데이터를 조회, 추가, 수정, 삭제하는 명령어**이다.

실제 데이터를 다룰 때 사용한다.

**대표 명령어**

- `SELECT`: 데이터 조회
- `INSERT`: 데이터 추가
- `UPDATE`: 데이터 수정
- `DELETE`: 데이터 삭제

```sql
INSERT INTO users (id, name)
VALUES (1, 'Kim');
```

### DCL(Data Control Language)

DCL은 **데이터베이스 권한을 제어하는 명령어**이다.

사용자에게 권한을 주거나 회수할 때 사용한다.

**대표 명령어**

- `GRANT`: 권한 부여
- `REVOKE`: 권한 회수

```sql
GRANT SELECT ON users TO user1;
```

### TCL(Transaction Control Language)

TCL은 **트랜잭션을 제어하는 명령어**이다.

데이터 변경 작업을 확정하거나 되돌릴 때 사용한다.

**대표 명령어**

- `COMMIT`: 트랜잭션 확정
- `ROLLBACK`: 트랜잭션 취소
- `SAVEPOINT`: 중간 저장점 설정

```sql
COMMIT;
```

### 비교

| 구분 | 의미 | 역할 | 대표 명령어 |
|---|---|---|---|
| DDL | Data Definition Language | 구조 정의 | CREATE, ALTER, DROP, TRUNCATE |
| DML | Data Manipulation Language | 데이터 조작 | SELECT, INSERT, UPDATE, DELETE |
| DCL | Data Control Language | 권한 제어 | GRANT, REVOKE |
| TCL | Transaction Control Language | 트랜잭션 제어 | COMMIT, ROLLBACK, SAVEPOINT |

### 정리

- DDL은 테이블 같은 데이터베이스 구조를 다룬다.
- DML은 테이블 안의 실제 데이터를 다룬다.
- DCL은 사용자 권한을 다룬다.
- TCL은 트랜잭션의 확정과 취소를 다룬다.

## NULL이란 무엇이고 다룰 때 주의할 점

`NULL`은 **값이 없거나 아직 알 수 없는 상태**를 의미한다.

`0`, 빈 문자열(`''`), 공백과는 다르다.

```text
0       -> 숫자 값 0
''      -> 비어 있는 문자열
NULL    -> 값이 없음 또는 알 수 없음
```

### NULL 비교

`NULL`은 일반 비교 연산자로 비교하면 안 된다.

```sql
WHERE name = NULL; -- 잘못된 방식
```

`NULL` 여부를 확인할 때는 `IS NULL` 또는 `IS NOT NULL`을 사용해야 한다.

```sql
WHERE name IS NULL;
WHERE name IS NOT NULL;
```

### NULL 연산

`NULL`이 포함된 연산 결과는 대부분 `NULL`이 된다.

```sql
10 + NULL -- NULL
```

즉, 알 수 없는 값과 계산하면 결과도 알 수 없다고 본다.

### 집계 함수에서의 NULL

집계 함수는 `NULL`을 제외하고 계산하는 경우가 많다.

```sql
COUNT(column) -- NULL 제외
COUNT(*)      -- 전체 행 개수
```

예를 들어 특정 컬럼의 값이 `NULL`이면 `COUNT(column)`에는 포함되지 않는다.

### 주의할 점

- `NULL`은 `0`이나 빈 문자열이 아니다.
- `NULL` 비교는 `=`이 아니라 `IS NULL`을 사용한다.
- `NULL`이 포함된 연산 결과는 `NULL`이 될 수 있다.
- 집계 함수에서 `NULL`이 제외될 수 있다.
- 필수 값이라면 `NOT NULL` 제약조건을 걸어야 한다.

### 정리

- `NULL`은 값이 없거나 알 수 없는 상태를 의미한다.
- `NULL`은 일반 값처럼 비교하면 안 된다.
- `NULL` 확인에는 `IS NULL`, `IS NOT NULL`을 사용한다.
- 데이터 정합성이 중요하면 `NOT NULL` 제약조건을 적절히 사용해야 한다.
