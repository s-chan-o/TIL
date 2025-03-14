## JDBC

JDBC는 Java기반 애플리케이션의 데이터를 데이터베이스에 저장 및 업데이트 하거나, 데이터베이스에 저장된 데이터를 
Java에서 사용할수 있도록 하는 자바 API이다.

JDBC는 Java애플리케이션에서 데이터베이스에 접근하기 위해 JDBC API를 사용하여 데이터베이스에 연동할 수 있으며, 데이터베이스에서 자료를 쿼리(Query)하거나 업데이트하는 방법을 제공한다.

> JDBC 표준 인터페이스

JDBC는 3가지 기능을 표준 인터페이스로 정의하여 제공한다.

- java.sql.Connection - 연결

- java.sql.Statement - SQL을 담은 내용

- java.sql.ResultSet - SQL요청 응답

Spring Data JDBC, Spring Data JPA 와 같은 기술이 등장하면서 JDBC API를 직접적으로 사용하는 일은 줄어들었다.

하지만, Spring Data JDBC, Spring Data JPA와 같은 기술도 데이터베이스와 연동하기 위해 내부적으로 JDBC를 이용하기 때문에 JDBC의 동작 흐름에 대해 알 필요가 있다.

> JDBC의 동작 흐름

 JDBC는 Java애플리케이션 내에서 JDBC API를 사용하여 데이터베이스에 접근하는 단순한 구조이다.

 JDBC API를 사용하기 위해서는 JDBC드라이버를 먼저 로딩한 후 데이터베이스와 연결하게 된다.

 JDBC 드라이버
 - 데이터베이스와의 통신을 담당하는 인터페이스
 - Oracle, MySQL 등과 같은 데이터베이스에 알맞은 JDBC 드라이버를 구현하여 제공
 - JDBC드라이버의 구현체를 이용해서 특정 벤더의 데이터베이스에 접근할 수 있음

 > JDBC API 사용 흐름

 ```
 JDBC 드라이버 로딩 -> 
 Connection 객체 생성 ->
  Statement 객체 생성 -> 
  Query 실행 -> 
  ResultSet객체로부터 데이터 조회 -> 
  ResultSet 객체 Close -> 
  Statement 객체 Close -> 
  Connection 객체 Close
 ```

 - JDBC 드라이버 로딩: 사용하고자 하는 JDBC 드라이버를 로딩한다. (DriverManager 클래스를 통해 로딩)

 - Connection 객체 생성: JDBC드라이버가 정삭적으로 로딩되면 DriverManager를 통해 데이터베이스와 연결되는 세션인 Connection 객체를 생성함

 - Statement 객체 생성: Statement 객체는 작성된 SQL 쿼리문을 실행하기 위한 객체로 정적 SQL쿼리 문자열을 입력으로 가진다.

 - Query 실행: 생성된 Statement 객체를 이용하여 입력한 SQL 쿼리를 실행한다.

 - ResultSet 객체로부터 데이터 조회: 실행된 SQL쿼리문에 대한 결과 데이터 셋이다.

 - ResultSet, Statement, Connection객체들의 Close: JDBC API를 통해 사용된 객체들은 생성된 객체들을 사용한 순서의 역순으로 Close한다.

 #### 커넥션 풀(Connection Pool)

 JDBC API를 사용하여 데이터베이스와 연결하기 위해 Connection객체를 생성하는 작업은 비용이 많이 드는 작업 중 하나이다.

 **커넥션 객체를 생성하는 과정**

 - 애플리케이션에서 DB 드라이버를 통해 커넥션을 조회한다.

 - DB 드라이버는 DB와 TCP/IP 커넥션을 연결한다.

 - DB 드라이버는 TCP/IP 커넥션이 연결되면 아이디와 패스워드, 기타 부가 정보를 DB에 전달한다.

 - DB는 아이디, 패스워드를 통해 내부 인증을 거친 후 내부에 DB를 생성한다.

 - DB는 커넥션 생성이 완료되었다는 응답을 보낸다.

 - DB 드라이버는 커넥션 객체를 생성해서 클라이언트에 반환한다.

 이처럼 커넥션을 새로 만드는 것은 비용이 많이 들며, 비효율적이다.

 이러한 문제를 해결하기 위해 애플리케이션 로딩 시점에 Connection 객체를 미리 생성하고