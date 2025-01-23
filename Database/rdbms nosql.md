## RDBMS와 NoSQL의 차이

먼저 database란 일반적으로 컴퓨터 시스템에 전자 방식으로 저장된 구조화된 정보 또는 데이터의 체계적인 집합을 의미한다.

DBMS(DataBase Management System)란 사용자와 데이터베이스 사이에서 사용자의 요구에 따라 정보를 생성해 주고 데이터베이스를 관리해 주는 소프트웨어이다.

SQL(Strucured Query Language)이란 관계형 데이터베이스 관리 시스템의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어이며 관계형 데이터베이스 관리 시스템에서 자료의 검색과 관리, 데이터베이스 스키마 생성과 수정, 데이터베이스 객체 접근 조정 관리를 위해 고안되었다.

> RDBMS에 대하여

RDBMS는 DBMS앞에 R이 붙어있다. 이 R은 Relational의 약자로 RDBMS는 관계형 데이터베이스 관리 시스템을 의미한다. 이 RDBMS는 RDB를 관리하는 시스템이며 RDB는 관계형 데이터 모델을 기초로 두고 모든 데이터를 2차원 테이블 형태로 표현하는 데이터베이스이다.

관계형데이터베이스(RDBMS)는 아래와 같이 구성된 테이블이 다른 테이블들과 관계를 맺고 모여있는 집합체로 이해할 수 있다.

![alt text](image.png)

관계형 데이터베이스(RDBMS)에서는 이러한 관계를 나타내기 위해 외래키를 사용한다.

이러한 테이블간의 관계에서 외래 키를 이용한 테이블간 Join이 가능하다는 게 RDBMS의 가장 큰 특징이다.

> NoSQL에 대하여

NoSQL이란 (Not Only SQL)의 약자로 말 그대도 위에서 설명한 RDB형태의 관계형 데이터베이스가 아닌 다른 형태의 데이터 저장 기술이다. 또 NoSQL에서는 RDBMS와는 달리 테이블 간 관계를 정의하지 않는다. 데이터 테이블은 그냥 하나의 테이블이며 테이블 간의 관계를 정의하지 않아 일반적으로 테이블 간 Join도 불가능하다.

NoSQL은 점점 빅데이터의 등장으로 인해 데이터와 트래픽이 기하급수적으로 증가함에 따라 RDBMS에 단점인 성능을 향상시키기 위해서는 장비가 좋아야 하는 Scale-Up의 특징이 비용을 기하급수적으로 증가시키기 때문에 데이터 일관성은 포기하되 비용을 고려하여 여러 대의 데이터에 분산하여 저장하는 Scale-Out을 목표로 등장했다.

NoSQL은 다양한 형태의 저장 기술을 지원하고 있다.
이 다양한 형태의 저장기술은 RDBMS 스키마에 맞추어 데이터를 관리해야 된다는 한계를 극복하고 수평적 확장성(Scale-Out)을 쉽게 할 수 있다는 장점이 있다.

1. **Key-Value Database**

- key-Value Database는 데이터가 Key와 Value의 쌍으로 저장된다. Key는 Value에 접근하기 위한 용도로 사용되며, 값은 어떠한 형태의 데이터라도 담을 수 있다. 심지어 이미지나 비디오도 가능하다. 또한 간단한 API를 제공하는 만큼 질의의 속도가 굉장히 빠른 편이다.

- 대표적인 NoSQL Key-Value Model로는 Redis, Riak, Amazon Dynamo DB 등이 있다.

2. **Document Database**

Document Database데이터는 Key와 Document의 형태로 저장된다. Key-Value 모델과 다른 점이라면 Value가 계층적인 형태인 토큐먼트로 저장된다는 점이다. 객체지향에서의 객체와 유사하고 이들은 하나의 단위로 취급되어 저장된다. 다시 말해 하나의 객체를 여러 개의 테이블에 나눠 저장할 필요가 없어진다는 뜻이다.

주요한 특징으로는 객체-관계 매핑이 필요하지 않다. 객체를 Document의 형태로 바로 저장 가능하기 때문이다. 또 검색에 최적화되어 있는데, 이는 Ket-Value 모델의 특징과 동일하다. 단점이라면 사용이 번거롭고 쿼리가 SQL과는 다르다는 점이다. 도큐먼트 모델에서는 질의의 결과가 JSON이나 xml 형태로 출력되기 때문에 그 사용 방법이 RDBMS에서의 질의 결과를 사용하는 방법과 다르다.

대표적인 Document Database Model로는 MongoDB, CouthDB등이 있다.

3. **Wide Column Database**

Column-family Model 기반의 Database이며 이전의 모델들이 Key-Value 값을 이용해 필드를 결정했다면, 특이하게도 이 모델은 키에서 필드를 결정한다. 키는 Row(키 값)와 Column-family, Column-name을 가진다. 연관된 데이터들은 같은 Column-family 안에 속해 있으며, 각자의 Column-name을 가진다. 관계형 모델로 설명하자면 어트리뷰트가 계층적인 구조를 가지고 있는 셈이다. 이렇게 저장된 데이터는 하나의 커다란 테이블로 표현이 가능하며, 질의는 Row, Column-family, Column-name을 통해 수행된다.

대표적인 NoSQL Column-family Model로는 HBase, Hypertable 등이 있다.

4. **Graph Database**

Graph Database Model에서는 데이터를 Node와 Edge, Property와 함께 그래프 구조를 사용하여 데이터를 표현하고 저장하는 Database이다. 개체와 관계를 그래프 형태로 표현한 것이므로 관계형 모델이라고 할 수 있으며, 데이터 간의 관계가 탐색의 키일 경우에 적합하다. SNS에서 내 친구의 친구를 찾는 질의 등에 적합하고, 연관된 데이터를 추천해주는 추천 엔진이나 패턴 인식 등의 데이터베이스로도 적합하다. 

데표적인 NoSQL Graph Model로는 Neo4J가 있다.