## DAO, DTO, VO, Entity

간단한 정리리

#### DAO

- 실제로 DB에 접근하는 객체이다.

- Persistence Layer(DB에 data를 CRUD 하는 계층)이다.

- Service와 DB를 연결하는 고리의 역할음 한다.

- SQL를 사용하여 DB에 접근한 후 적절한 CRUD API를 제공한다.(JPA 대부분의 기본적인 CRUD method를 제공하고 있다.)

- repository == DAO(거의 비슷함) -> 좀 더 깊이있게 차이를 설명하자면, repository는 엔티티 객체를 보관하고 관리하는 저장하는 저장소이고, DAO는 데이터에 접근 하도록 DB접근 관련 로직을 모아둔 객체 이다.

---

#### DTO

- 계층간 데이터 교환을 위한 객체(Java Beans)이다.

    - DB에서 데이터를 얻어 Service나 Controller등으로 보낼 때 사용하는 객체를 말한다.

    - 즉, DB의 데이터가 Presentation Logic Tier로 넘어오게 될 때는 DTO의 모습으로 바뀌어서 오고가는 것이다.

    - DTO는 목적 자체가 로직을 갖고 있지 않고 단순히 데이터를 전달하는 것이기 때문에 순수한 데이터 객체이며, getter/setter 메서드만 갖는다.

---

#### VO

- Read-Only 특징을 가진다.

- 핵심은 equals()와 hashcode()를 오버라이딩 하는 것이다.

- equals, hashcode method를 구현하여 특정 중요한 data를 전달할 때는 VO를 생성하여 이를 동일한 객체 비교까지 필요한 logic내에서 주로 사용한다.

---

#### Entity

- domain package

- 실제 DB의 테이블과 매칭되는 클래스

    - entity는 비즈니스 로직이 있고, 실제 데이터도 변경되기 때문에 Setter를 최대한 사용하지 않는 편이 좋다.

- 최대한 외부에서 Entity클래스의 getter method를 사용하지 않도록 해당 클래스 안에서 필요한 로직 method를 구현한다.
