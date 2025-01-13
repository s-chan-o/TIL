## Spring MVC
> MVC 패턴이란?

- MVC 패턴은 애플리케이션을 개발할 때 사용하는 디자인 패턴이다.
- 애플리케이션의 개발 영역을 MVC (Model, View, Controller)로 구분하여 각 역할에 맞게 코드를 작성하는 개발 방식이다.
- MVC 패턴을 도입하면서 UI 영역과 도메인(비즈니스 로직) 영역으로 구분되어 서로에게 영향을 주지 않으면서 개발과 유지보수가 가능하다.
- MVC에서 모델은 애플리케이션의 정보(데이터)를 나타내며, 뷰는 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소를 나타내고, 컨트롤러는 데이터와 비즈니스 로직 사이의 상호동작을 관리한다.

> MVC 패턴을 사용하는 이유

사용자가 보는 페이지, 데이터 처리, 그리고 이 2가지를 중간에서 제어하는 컨트롤 이렇게 3가지로 구성되는 하나의 애플리케이션을 만들면 각각 맡은 역할에만 집중을 할 수 있게 된다.

- MVC 패턴의 사용 목적 : 각 컴포넌트가 서로 분리되어 각자의 역할에 집중할 수 있기 때문에 시스템 결합도를 낮출 수 있다. 또한, 유지보수가 쉬우며, 중복코드를 제거할 수 있고, 애플리케이션의 확장성 및 유연성이 증가한다.

> Model, View, Controller

#### Model

- Spring MVC 기반의 웹 애플리케이션이 클라이언트의 요청을 전달받으면 요청 사항을 처리하기 위한 작업을 한다. 
- 처리한 작업의 결과 데이터를 클라이언트에게 응답으로 돌려주어야 하는데, 이 때 클라이언트에게 응답으로 돌려주는 작업의 처리 결과 데이터를 Model이라고 한다.

#### View

- View는 Model을 이용하여 웹 브라우저와 같은 애플리케이션의 화면에 보이는 리소스를 제공하는 역할을 한다.
- Spring MVC에는 다양한 View 기술이 포함되어 있다.
    - HTML 페이지 출력
    - PDF, Excel 등의 문서 형태로 출력
    - XML, JSON 등 특정 형식의 포맷으로 변환

#### Controller

- 컨트롤러는 클라이언트 측의 요청을 직접적으로 전달받는 엔드포인트로써 Model과 View의 중간에서 상호작용을 해주는 역할을 한다.
- 클라이언트 측의 요청을 전달받아 비즈니스 로직을 거친 후, Model 데이터가 만들어지면 이 Model 데이터를 View로 전달하는 역할을 한다.

> MVC1, MVC2

#### MVC1

우리가 흔히 사용하고 있는 MVC 패턴은 사실 MVC1, MVC2 아키텍쳐에서 발전된 패턴이다.

- MVC1 패턴이란, 브라우저(사용자)로부터 요청이 들어오면 DB로부터 필요한 데이터를 받은 Model객체를 JSP 페이지에 담아 응답으로 보내는 패턴이다.
- MVC1 에서는 JSP가 View와 Controller 역할을 모두 담당하기 때문에 JSP 페이지 내에 너무 많은 코드가 들어가게 된다. 따라서, 코드의 가독성이 떨어질 뿐만 아니라 코드가 복잡해질 가능성이 있다. 이러한 점을 보완하여 Controller 역할을 하는 Servlet이 추가된 MVC2 패턴이 등장하게 되었다.

#### MVC2

- MVC2 패턴은 요청을 하나의 컨트롤러가 먼저 받는다.
- 서블릿은 요청에 대한 비즈니스 로직을 처리한 후, 이를 JSP 파일에 반영하는 역할을 수행한다. 
- MVC2는 MVC1 패턴보다 구조가 복잡해질 수 있으나, 이러한 문제점들을 해결하기 위해 각종 프레임워크들이 지금까지 잘 발전되어 왔고, 그 중에서 대표적인 것이 바로 스프링 프레임워크이다.

> Spring MVC 구조

#### DispatcherServlet

- Front Controller의 역할을 수행하며 Request를 각각의 Controller에게 위임한다.
- 가장 앞 단에서 클라이언트의 요청을 처리하는 Controller로써 요청부터 응답까지 전반적인 처리 과정을 통제한다.

         DispatcherServlet을 Front Controller로 설정하는 방법 : 
        1. web.xml에 명시한다.
        2. org.springframework.web.WebApplicationInitializer 인터페이스를 구현한다.

#### Handler Mapping

- 요청을 직접 처리할 컨트롤러를 탐색한다.
- 구체적인 Mapping은 xml파일이나 java config 관력 어노테이션 등을 통해 처리할 수 있다.

#### HandlerAdapter

- 매핑된 컨트롤러의 실행을 요청한다

#### Controller

- DispatcherServlet이 전달해준 HTTP 요청을 처리하고 결과를 Model에 저장한다.
    - 직접 요청을 처리하고 처리 결과를 반환한다.
    - 결과가 반환되면 HandlerAdapter가 ModelAndView 객체로 변환되며, 여기에는 View Name과 같이 응답을 통해 보여줄 View에 대한 정보와 관련된 데이터가 포함되어 있다.

#### ModelAndView

- Controller에 의해 반환된 Model과 View가 Wrapping된 객체이다.

#### View Resolver

- View Name을 확인한 후, 실제 컨트롤러로부터 받은로직 처리 결과를 반영할 View 파일 (jsp)을 탐색한다.

#### View

- 로직 처리 결과를 반영한 최종 화면을 생성한다.

> Spring MVC 동작 구조

- 사용자의 모든 요청을 받아 처리한다.
- 프론트 컨트롤러에 해당하는 역할을 수행하며 Request를 각각의 Controller에게 위임한다.
- DispatcherServlet을 프론트 컨트롤러로 가능하도록 설정하기 위해서는 이를 web.xml에 명시하거나 org.springframework.web.WebApplicationnlnitializer 인터페이스를 구현하는 두 가지 방식을 사용할 수 있다.

> 주요 어노테이션

- @Repository : 데이터 액세스 계층에 사용, 예외 변환 기능 포함.

- @Service : 서비스 계층에 사용, 비즈니스 로직 담당.

- @Autowired : 의존성 주입을 자동으로 수행.

- @Controller : 프레젠테이션 계층에 사용, 웹 요청 처리.

- @RequestMapping : 특정 URL 패턴과 HTTP 메서드를 컨트롤러 메서드에 매핑.

- @GetMapping : HTTP GET 요청을 처리.

- @PostMapping : HTTP POST 요청을 처리.