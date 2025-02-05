## @NoArgsConstructor

@NoArgsConstructor 어노테이션은 파라미터가 없는 디폴트 생성자를 자동으로 생성한다. 이 어노테이션을 사용하면,  클래스에 명시적으로 선언된 생성자가 없더라도 인스턴스를 생성할 수 있다.

```java
@NoArgsConstructor
public class User{

    private Long id;
    private String name;
    private Long num;
}

User user = new User();//파라미터가 없는 생성자를 자동으로 생성함
```

> 언제 사용?

- @Entity가 붙은 클래스 

- @RequestDto