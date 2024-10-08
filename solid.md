## SOLID

SOLID란 **객체 지향 프로그래밍**을 하면서 지켜야하는 5대 원칙으로 각각 SRP(단일 책임 원칙), OCP(개방-폐쇄 원칙), LSP(리스코프 치환 원칙), DIP(의존 역전 원칙), ISP(인터페이스 분리 원칙)의 앞글자를 따서 만들어졌다. 

- 객체 지향 프로그래밍 : 객체 지향 프로그래밍 (Object-Oriented Programming, OOP)은 프로그래밍에서 필요한 데이터를 추상화 시켜 상태와 행위를 가진 객체로 만들고, 객체들간의 상호작용을 통해 로직을 구성하는 프로그래밍 방법이다.

SOLID 객체 지향 원칙을 적용하면 코드를 확장하고 유지 보수 관리하기가 더 쉬워지고 불필요한 복잡성을 제거해 리펙토링에 소요되는 시간을 줄임으로써 프로젝트 개발의 생산성을 높일 수 있다.

--- 

#### 단일 책임의 원칙 (SRP, Single Responsibility Principle)

- 클래스는 단 한 개의 책임을 가져야 한다.

- 클래스를 변경하는 이유는 단 하나여야 한다.

> 왜 하나의 클래스의 책임이 많으면 안될까??

    하나의 클래스에 책임져야할 부분이 많을 경우, 섣불리 내부를 변경하기 어렵고, 해당 클래스와 연계된 클래스 모두가 영향을 받기 때문이다.

즉, 하나의 클래스에 저렇게 모아놓으면, 수정이 일어났을 때, 수정해야 할 코드가 많아진다. 이런 부분은 유지보수와도 이어지기 때문에, 반드시 책임을 분리해줘야 한다.

SRP를 제대로 준수한다면, 변경이 필요할 때 수정할 대상이 명확해진다. 이런 장점은 시스템이 커질수록 극대화 된다. 시스템이 커지면서 서로 많은 의존성을 갖게 되는 상황이고, 변경요청이 들어오면 특정 클래스 하나만 수정하면 되기 때문이다.

> 간단한 코드 예시

    class Car {
                                        // SRP 위반: Car 클래스가 두 가지 책임(start와 stop)을 가지고 있음
                                        // 각각의 메서드가 개별적으로 관리되어야 할 책임을 담고 있음

    public void start() {
        // 자동차를 시작하는 로직
    }

    public void stop() {
        // 자동차를 정지하는 로직
    }
}


---

#### 개방 폐쇄 원칙 (OCP, Open-Closed Principle)

- 요구사항이 변경될 때 새로운 동작을 추가하여 애플리케이션의 기능을 확장할 수 있다. (클래스는 확장에 열려있어야 하며)

- 기존의 코드를 수정하지 않고 애플리케이션의 동작을 추가하거나 변경할 수 있다. (수정에는 닫혀 있어야 한다)

즉, 기능 추가 요청이 오면 클래스를 확장을 통해 쉽게 구현하면서, 확장에 따른 클래스 수정은 최소화 하는 것이다. 만약 새로운 변경사항이 있을 때, 객체를 직접적으로 수정해야 한다면, 유지 보수의 비용 증가로 이어지고, 이는 안 좋은 설계방식이다.

    OCP를 위반하지 않는 설계를 할 때 중요한 것은 무엇이 변하는 것인지, 무엇이 변하지 않는 것인지 구분해야 한다.

이것은 추상화와 연관이 있다.

OCP는 추상화를 통해 구현이 가능하다. 자주 변화하는 기능들을 추상화 함으로써, 기존의 클래스가 영향을 받지 않게 클라이언트가 개별적인 클래스에 접근하는 것이 아닌 추상화한 인터페이스로 접근을 하게 한다.

요구사항의 변경이나 추가사항이 발생하더라도, 기존 코드를 크게 수정할 필요 없이, 유연하게 기능을 확장할 수 있다.

> 간단한 코드 예시

        interface Shape {
        double getArea();                       // OCP 적용: Shape 인터페이스는 확장에 열려 있음 (새로운 도형을 추가할 수 있음)
    }

    class Rectangle implements Shape {
        private double width;
        private double height;

                                                // OCP 적용: Rectangle 클래스는 Shape 인터페이스를 구현하며, 변경 없이 확장이 가능
        public double getArea() {
            return width * height;              // 직사각형의 면적 계산
        }
    }

    class Circle implements Shape {
        private double radius;

                                                // OCP 적용: Circle 클래스도 Shape 인터페이스를 구현하며, 변경 없이 확장이 가능
        public double getArea() {
            return Math.PI * radius * radius;   // 원의 면적 계산
        }
    }

---

#### 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)

    리코스프 치환 원칙이란 부모 객체와 자식 객체가 있을 때 부모 객체를 호출하는 동작에서 자식 객체가 부모 객체를 완전히 대채할 수 있다는 원칙이다.

즉 자식타입의 객체는 언제든 부모타입의 객체로 교체할 수 있어야 한다. 

객체지향에서 상속이 일어나면, 자식 객체는 부모 객체의 특성을 가지며, 그 특성을 토대로 확장할 수 있습니다.

리스코프 치환 원칙은 무분별한 상속이 아닌, 올바른 상속을 위해 자식 객체의 확장이 부모 객체의 방향을 온전히 따르도록 권고하는 원칙이다.

- 올바른 상속이란, 부모 클래스의 인스턴스 대신, 자식 클래스의 인스턴스를 별 다른 변경 없이 사용해야 한다.

> 간단한 코드 예시

        interface Bird {
        void fly();                                     // 모든 새가 구현해야 하는 비행 메서드 (LSP 위반 가능성 있음)
    }

    class Duck implements Bird {
        public void fly() {
            // 오리는 날 수 있으므로 비행 로직 구현
        }
    }

    class Ostrich implements Bird {
        public void fly() {
            throw new UnsupportedOperationException();  // 타조는 날 수 없으므로 예외를 던짐 (LSP 위반)
        }
    }



#### 인터페이스 분리 원칙 (ISP, Interface segregation principle)

    SRP가 클래스의 단일 책임을 명시했다면, ISP는 인터페이스의 단일 책임을 명시해 준다. ISP 원칙은 인터페이스를 사용하는 클라이언트를 기준으로 분리해서, 클라이언트의 목적과 용도에 적합한 인터페이스 만을 제공해 주는 것이 목표다.

- 만약 사용하지 않는 메서드에서 변경이 일어날 시, 문제가 발생할 수 있다.

- 인터페이스를 분리함으로써, 클라이언트가 사용하지 않는 인터페이스에 변경이 발생하더라도 영향을 받지 않도록 만들어 줘야 한다.

> 간단한 코드 예시

                                            // Car 인터페이스: 자동차 관련 메서드
    interface Car {
        void drive();                       // 자동차 주행
    }

                                            // Airplane 인터페이스: 비행기 관련 메서드
    interface Airplane {
        void fly();                         // 비행기 비행
    }

                                            // FltyingCar 클래스: Car와 Airplane 인터페이스를 모두 구현
                                            // 하나의 클래스가 두 가지 기능(Car와 Airplane)을 구현하고 있음

    class FltyingCar implements Car, Airplane {
    
        @Override
        public void drive() {
            // 자동차 주행 구현
        }

        @Override
        public void fly() {
            // 비행기 비행 구현
        }
    }


---

#### 의존성 역전 원칙 (DIP, Dependency Inversion Principle)

    의존 역전 원칙이란 고수준 모듈은 저수준 모듈의 구현에 의존해서는 안되며, 저수준 모듈이 고수준 모듈에 의존해야 한다는 것이다.

- 고수준 모듈 
    - 어떤 의미 있는 단일 기능을 제공하는 모듈
    - 변하지 않는 것

- 저수준 모듈
    - 고수준 모듈의 기능을 구현하기 위해 필요한 하위 기능의 실제 구현(메인 클래스, 객체)
    - 빈번하게 변하는 것

저수준 모듈은 빈번하게 변경되고, 새로운 것이 추가될 때마다 고수준 모듈이 영향을 받기 쉬우므로, 의존관계를 역전시켜야 한다. 따라서 한 마디로 상위의 인터페이스 타입의 객체로 통신하라는 원칙입니다.

> 의존관계란??

한 클래스가 어떤 기능을 수행하려고 할 때, 다른 클래스의 서비스가 필요한 경우를 말하는데, 대표적으로 A 클래스의 메서드에서 메개변수를 다른 B 클래스의 타입으로 받아 B 객체의 메서드를 사용할 때, A 클래스는 B 클래스와 의존한다고 한다.

> 간단한 코드 예시

                                            // Database 인터페이스: 데이터 저장 메서드 정의
    interface Database {
        void save(String data);             // 데이터 저장
    }

                                            // MySQL 클래스: Database를 구현하여 MySQL에 데이터 저장
    class MySQL implements Database {
        @Override
        public void save(String data) {
            // MySQL에 데이터 저장
        }
    }

                                            // User 클래스: Database에 의존하고, 데이터 저장 기능을 제공
    class User {
        private Database database;          // Database 의존성

        // 생성자에서 Database를 주입받음
        public User(Database database) {
            this.database = database;
        }

        // 데이터를 저장하는 메서드
        public void saveData(String data) {
            database.save(data);            // Database를 통해 데이터 저장
        }
    }
