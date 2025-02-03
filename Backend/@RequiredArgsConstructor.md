## @RequiredArgsConstructor

이 어노테이션은 초기화 되지 않은 final 필드나, @NonNull이 붙은 필드에 대해 생성자를 생성해 주는 역할을 한다.

이 어노테이션을 사용하게 되면 새로운 필드를 추가할 때 다시 생성자를 만들어서 관리해야 하는 번거로움을 덜 수 있다.

#### 예시

**@RequiredArgsConstructor 를 사용한 예시**

```java

@RestController
@RequiredArgsConstructor
@RequestMapping("/order")
public class OrderController{

    private final ChickenService;
    private final PizzaService;
}
```

해당 필드로 구성된 생성자를 @RequiredArgsConstructor 가 자동으로 생성자 주입에 대한 코드를 생성해준다.

**@RequiredArgsConstructor 를 사용하지 않고 생성자 주입 코드를 작성한 예시**

```java

@RestController
@RequestMapping("/order")
public class OrderController{

    private final ChickenService;
    private final PizzaService;

    @Autowired
    public OrderController(ChickenService chickenService, PizzaService pizzaService)
    this.chickenRepository = chickenRepository;
    this.pizzaRepository = pizzaRepository
}
```

보통 DI 방식엔 필드 주입, 수정자 주입, 생성자 주입 3가지의 방법이 있는데 생성자 주입을 권장한다.

하지만 생성자 주입을 위한 코드를 만드는데 번거로워서 Lombok에서 @RequiredArgsConstructor 어노테이션을 사용한다. (final변수들, 필드들을 매개변수로 하는 생성자를 자동으로 생성)
