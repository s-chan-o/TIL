# rest api
> REST API란??

REST API(RESTful API 또는 RESTful 웹 API라고도 함)는 REST(Representational State Transfer) 아키텍처 스타일의 설계 원칙을 준수하는 API(애플리케이션프로그래밍 인터페이스)이다. REST API는 애플리케이션을 통합하고 마이크로서비스 아키텍처의 구성 요소를 연결하는 유연하고 가벼운 방법을 제공한다.

> API란??

웹 API는 클라이언트와 웹 리소스 사이의 네트워크 통신을 위한 게이트웨이라고 생각할 수 있다. API(애플리케이션프로그래밍 인터페이스)는 다른 소프트웨어 시스템과 통신하기 위해 따라야 하는 규칙을 정의한다.

> REST란??

REST(Representational State Transfer)의 약자

자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미한다.

'HTTP URI(Uniform Resource Identifier)'를 통해 자원(Resource)을 명시하고,
'HTTP Method(POST, GET, PUT, DELETE, PATCH 등)'를 통해 해당 자원(URI)에 대한 **'CRUD Operation'** 을 적용한다.

CRUD Operation : 
- Create : 데이터 생성(POST)
- Read : 데이터 조회(GET)
- Update : 데이터 수정(PUT, PATCH)
- Delete : 데이터 삭제(DELETE)

1. 자원을 이름으로 구분? = 자원의 표현

- 자원 = 문서, 사진, 그림, 데이터 등 소프트웨어가 관리하는 모든 것을 HTTP URI(Uniform Resource Identifier)를 통해 명시하는 것이다.

2. 자원의 상태를 주고 받음(요청 -> 응답)

- 클라이언드는 데이터가 요청되어지는 시점에서 자원의 상태를 전달한다.
- 클라이언트가 자원의 상태에 대한 조작을 요청하면 서버는 이에 적절한 응답을 보낸다.
- 전달 방식으로는 JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
