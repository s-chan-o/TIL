# 해시 관련

## 해시 테이블(Hash Table)의 동작 원리

해시 테이블은 **key를 해시 함수로 변환해 나온 index에 value를 저장하는 자료구조**이다.  
key를 배열의 index처럼 바꿔 접근하기 때문에 평균적으로 조회가 빠르다.

```text
key -> hash function -> index -> value
```

### 저장과 조회

데이터를 저장할 때는 key를 해시 함수에 넣어 index를 구하고, 해당 위치에 value를 저장한다.

```text
key: name
value: Kim

name -> hash function -> index
index 위치에 Kim 저장
```

조회할 때도 같은 key를 해시 함수에 넣는다.  
같은 key는 같은 index로 변환되기 때문에 저장된 value를 빠르게 찾을 수 있다.

### 해시 충돌(Hash Collision)

해시 충돌은 **서로 다른 key가 같은 index로 변환되는 상황**이다.

```text
apple  -> index 4
banana -> index 4
```

충돌이 발생하면 같은 위치에 여러 값을 저장해야 하므로 충돌 처리 방식이 필요하다.

대표적인 해결 방법은 다음과 같다.

- **체이닝(Chaining)**: 같은 index에 여러 데이터를 연결해서 저장한다.
- **개방 주소법(Open Addressing)**: 충돌이 나면 다른 빈 index를 찾아 저장한다.

### 시간복잡도

| 작업 | 평균 | 최악 |
|---|---:|---:|
| 삽입 | O(1) | O(n) |
| 조회 | O(1) | O(n) |
| 삭제 | O(1) | O(n) |

평균적으로는 `O(1)`이지만, 해시 충돌이 많이 발생하면 최악의 경우 `O(n)`까지 느려질 수 있다.

### 정리

- 해시 테이블은 key를 index로 바꿔 value를 저장한다.
- 평균적으로 삽입, 조회, 삭제가 `O(1)`이다.
- 서로 다른 key가 같은 index를 가리키면 해시 충돌이 발생한다.
- 해시 충돌은 체이닝이나 개방 주소법으로 해결한다.

## Map과 Set의 차이

`Map`과 `Set`은 둘 다 해시 기반 자료구조로 구현될 수 있지만, 저장하는 데이터의 형태가 다르다.

### Map

`Map`은 **key-value 쌍으로 데이터를 저장하는 자료구조**이다.

```text
key -> value
name -> Kim
age  -> 18
```

- key는 중복될 수 없다.
- value는 중복될 수 있다.
- key를 이용해 value를 빠르게 찾을 때 사용한다.

### Set

`Set`은 **중복을 허용하지 않는 값의 집합**이다.

```text
A, B, C
```

- 같은 값은 한 번만 저장된다.
- 값의 존재 여부를 빠르게 확인할 때 사용한다.
- 중복 제거에 자주 사용된다.

### Map과 Set 비교

| 구분 | Map | Set |
|---|---|---|
| 저장 형태 | key-value | value |
| 중복 허용 | key 중복 불가, value 중복 가능 | value 중복 불가 |
| 주요 목적 | key로 value 찾기 | 값의 존재 여부 확인, 중복 제거 |

## HashMap

`HashMap`은 해시 테이블을 기반으로 `Map`을 구현한 자료구조이다.

즉, key-value를 저장하되, key를 해시 함수로 변환해 저장 위치를 찾는다.

```text
key -> hash function -> index -> value
```

예를 들어 `name = Kim`을 저장하면, `name`이라는 key를 해시 함수에 넣어 index를 구하고, 그 위치에 `Kim`을 저장한다.

```text
name -> hash function -> index -> Kim
```

### HashMap의 특징

- key-value 형태로 데이터를 저장한다.
- key는 중복될 수 없다.
- 같은 key로 다시 저장하면 기존 value가 덮어써진다.
- 평균적으로 삽입, 조회, 삭제가 `O(1)`이다.
- 해시 충돌이 많이 발생하면 최악의 경우 `O(n)`까지 느려질 수 있다.

### 정리

- `Map`은 key-value를 저장하는 자료구조이다.
- `Set`은 중복 없는 value만 저장하는 자료구조이다.
- `HashMap`은 해시 테이블 기반의 Map 구현체이다.
- 빠른 조회가 필요하면 HashMap을 많이 사용한다.
