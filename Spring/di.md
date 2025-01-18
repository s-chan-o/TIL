## DI (Dependency Injection)

DI란 무엇: Dependcy Injection의 줄임말로 의존성 주입이라고 한다.

**하나의 객체에 다른 객체의 의존성을 제공하는 기술** 이라고 표현한다.

> 코드로 이해하는 DI

```
public class Chicken{

    private Bbq bbq;

}
```

이 코드에서 Chicken클래스는 Bbq 클래스를 의존한다.

하지만 이 상태에선 클래스끼리 강하게 결합되어 있다는 것이 문제가 되고 객체가 아닌 클래스 끼리의 관계이기 때문에 개발자들이 추구하는 객체지향과는 거리가 있다.

**쉽게 생각했을때 치킨을 비비큐의것만 먹고 살 수는 없다**

이것은 인터페이스, 다형성이라는 개념으로 해결한다.

```
public class Chicken{

    private Brand brand;

    public Chicken(Brand brand){
        this.brand = brand;
    }

}
```

Brand라는 인터페이스를 만들어서 Chicken 객체를 생성할 때 외부에서 Brand객체를 매개변수로 받는다. bbq는 bhc든 받아서 넣어줄 수 있게 되었다.

여기에서 DI 컨테이너가 필요하다. 

Chiken에서 Brand 객체를 주입하기 위해선, 어플리케이션 실행 시점에, 필요한 객체를 생성해야한다.

**의존성이 있는 두 객체를 연결하기 위해 한 객체를 다른 객체로 주입 시켜야 하기 때문이다!**