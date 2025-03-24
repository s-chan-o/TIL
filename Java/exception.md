## 예외처리

프로그램 실행 시 발생할 수 있는 오류에 대비하기 위해 프로그램의 비정상 종료를 막고 실행 상태를 유지하는 것

#### 오류의 종류

1. 에러(Error)

- 시스템, 운영체제, JVM의 잘못으로 발생되는 것

- 개발자가 해결할 수 있는 문제가 아님

- 예외처리의 대상이 아님

2. 예외(Exception)

- 개발자의 코딩실수나 사용자의 잘못된 프로그램 사용으로 발생하는 오류

- 예외처리를 통해서 비정상적인 종료 예방 가능

- UncheckedException / CheckedException으로 구분

**UncheckedException**

- RuntimeException 클래스와 그 자식 클래스들

- 주로 개발자의 코딩 실수로 발생되는 오류

- 컴파일러가 예외처리 여부를 체크하지 않음


**CheckedException**

- Exception 클래스와 Exception 클래스의 하위 클래스 중에서 RuntimeException 클래스의 하위 클래스가 아닌 예외클래스

- 사용자의 잘못된 사용으로 인해 발생하는 오류

- 컴파일러가 예외처리 구현 여부를 반드시 체크함