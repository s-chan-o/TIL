## @AllArgsConstructor.

@AllAgsConstructor 어노테이션은 클래스의 모든 필드 값을 파라미터로 받는 생성자를 자동으로 생성한다.

@AllAgsConstructor어노테이션을 사용하면 클래스의 모든 필드를 한 번에 초기화할 수 있다.

```java
public class Ingan{
    private String name;
    private Long age;

    public Ingan(String name, Long age){
            this.name = name;
            this.age = age;
    }
}
```

이 코드를 @AllAgsConstructor 사용하여 바꾸면 아래와 같이 바꿀 수 있다.

```java
@AllAgsConstructor
public class Ingan{
    private String name;
    private Long age;
}
```