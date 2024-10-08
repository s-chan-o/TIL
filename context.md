## 영속성 컨텍스트 (Persistence Context)

> 영속성 컨텍스트란??

영속성 컨텍스트란 **엔티티**를 영구 저장하는 환경이라는 뜻인데, 애플리케이션과 데이터베이스 사이에서 객체를 보관하는 가상의 데이터베이스 같은 역할을 한다.

`엔티티 : 엔티티를 그대로 번역하면 실제, 독립체라는 뜻으로 데이터 모델링에서 사용되는 객체라고 생각하면 된다.`

 `데이터베이스 테이블과 매핑되는 객체이다.`

**엔티티 매니저**를 통해 엔티티를 저장하거나 조회하면 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.

- 엔티티 매니저 : 엔티티를 저장하고, 수정하고, 삭제하고 조회하는 등 엔티티와 관련된 모든 일을 처리한다. 

> 엔티티 생명주기

![alt text](image.png)

- **비영속(new/transient) :** 엔티티 객체를 생성했지만 아직 영속성 컨텍스트에 저장하지 않은 상태를 비영속이라고 한다.

이 상태에서는 JPA와 아무런 관련이 없고 데이터베이스와 연관되지 않는다.

`Member member = new Member();`

- **영속(managed) :** 엔티티 매니저를 통해서 엔티티를 영속성 컨텍스트에 저장한 상태를 말하며 영속성 컨텍스트에 의해 관리된다는 뜻이다.

`em.persist();`

- **준영속(detached) :** 영속성 컨텍스트가 관리하던 영속 상태의 엔티티를 더이상 관리하지 않으면 준영속 상태가 된다. 특정 엔티티를 준영속 상태로 만드려면 ***em.datach()*** 를 호출하면 된다.

em.clear()를 호출해 영속성 컨텍스트 전체를 준영속 상태로 만들 수 있다.

#### 준영속 상태의 특징

    - 1차 캐시, 쓰기 지연, 변경 감지, 지연 로딩을 포함한 영속성 컨텍스트가 제공하는 어떠한 기능도 동작하지 않는다.

    - 식별자 값을 가지고 있다.

- **삭제(removed) :** 엔티티를 영속성 컨텍스트와 데이터베이스에서 삭제한다.

`em.remove();` 

> 영속성 컨텍스트의 특징 

- 엔티티 매니저를 생성할 때 하나 만들어진다.

- 엔티티 매니저를 통해서 영속성 컨텍스트에 접근하고 관리할 수 있다.

- 영속성 컨텍스트는 엔티티를 식별자 값으로 구분하기 때문에 영속 상태는 식별자 값이 반드시 있어야 한다.

- JPA 보통 트랜잭션을 커밋하는 순간 영속성 컨텍스트에 새로 저장된 엔티티를 데이터 베이스에 변경하는데 이를 `flush` 라고 한다.

> 영속성 컨텍스트의 장점

- **1차 캐시** : 조회가 가능하며 1차 캐시에 없으면 DB에서 조회하여 **1차 캐시**에 올려 놓는다.

    `1차 캐시 : 영속성 컨텍스트 내부에는 엔티티를 보관하는 저장소를 1차 캐시라고 한다.`

key : @Id로 선언한 필드, 데이터베이스의 기본키와 매핑

value : 엔티티 인스턴스

- 동일성 보장 : 동일성 비교가 가능하다.

- 쓰기 지연 : **트랜잭션**을 지원하는 쓰기 지연이 가능하며 **트랜잭션**을 커밋하기 전까지 SQL을 바로 보내지 않고 모아서 보낼 수 있다.

    `트랜잭션 : 트랜잭션은 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 모두 수행되어야 할 일련의 연산들을 의미한다.`

쓰기 지연은 성능을 최적화하는데 중요한 역할을 하며, 트랜잭션의 일관성을 유지할 수 있다.

- 변경 감지 : 스냅샷을 1차 캐시에 들어온 데이터를 찍는다. 커밋 되는 시점에 엔티티와 스냅샷을 비교하여 update SQL을 생성한다.

- 지연 로딩 : 엔티티에서 해당 엔티티를 불러올 때 그 때 SQL을 날려 해당 데이터를 가져온다.

> 엔티티의 생명주기 관리

- 새로운 엔티티를 생성할 때 엔티티 매니저를 사용하여 영속성 컨택스트에 저장한다.

- 영속 상태의 엔티티는 영속성 컨텍스트에 의해 관리되며, 변경 사항이 있으면 자동으로 감지하여 데이터베이스에 반영된다.

- 엔티티를 삭제하면 영속성 컨텍스트에서 제거된다.

- 의도적으로 영속성 컨텍스트에서 엔티티를 비영속 상태로 만들 수 있다.

> 엔티티와 데이터베이스 간의 작업을 캐시

- 엔티티를 조회할 때, 영속성 컨텍스트에 조회할 내용이 있는지 확인하고, 있다면 데이터베이스를 조회하는 것 대신 캐시 데이터를 사용할 수 있다.


> 지연 로딩

- 엔티티를 조회할 때, 연관된 엔티티를 **즉시 로딩**하는 것 대신, 필요할 때 로딩하는 **지연 로딩**을 지원한다.

    `즉시 로딩 : 즉시로딩이란 데이터를 조회할 때, 연관된 모든 객체의 데이터까지 한 번에 불러오는 것이다.`
    `지연 로딩 : 지연로딩이란, 필요한 시점에 연관된 객체의 데이터를 불러오는 것이다.`

- 같은 트랜잭션 내에서, 같은 영속성 컨텍스트를 사용하여, 일관된 데이터를 유지한다.

> 영속성 컨텍스트의 범위 = 트랜잭션 범위에서 수행됨

- 영속성 컨텍스트의 범위는 트랜잭션 작업 범위에서 적용된다.

- 트랜잭션이 커밋될 때 영속성 컨텍스트에서 변경된 엔티티를 데이터베이스에 flush 하게 된다.

- 같은 트랜잭션 내에서, 같은 영속성 컨텍스트를 사용하여, 일관된 데이터를 유지한다.