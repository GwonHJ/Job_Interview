# Spring

1. Framework란?
    1. 특정 형태의 소프트웨어 문제를 해결하기 위해서 클래스 프레임과 인터페이스 프레임의 집합
    2. 특정한 틀을 만들어 놓고 거기에 살을 붙이면서 프로그램을 만들어서 작업시간을 줄여주는 것
    3. 프레임워크는 특정 개념들의 추상화를 제공하는 여러 클래스나 컴포넌트로 구성
    
    프레임워크를 사용하는 이유
    
    - 프로그램 개발에 투입되는 개발자가 늘어나면서 전체 시스템의 통합성, 일관성이 떨어짐 → 개발자의 자유를 제한
    
    프레임워크의 장/단점
    
    - 장점 : 개발 시간을 줄일 수 있고 오류로부터 자유로울 수 있다
    - 단점 : 처음에 익힐 시간이 필요하다?
    
2. Spring Framework(스프링 프레임워크)
    1. 자바(JAVA) 플랫폼을 위한 오픈소스 애플리케이션 프레임워크(Framework)이다.
    2. 자바 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크이다.
    3. 자바 개발을 위한 프레임워크로 종속 객체를 생성해주고, 조립해주는 도구
    4. 자바로 된 프레임워크로 자바 SE로 된 자바 객체(POJO)를 자바EE에 의존적이지 않게 연결해주는 역할
        1. 자바 SE : 데스크톱, 서버, 임베디드시스템을 위한 표준 자바 플랫폼
            1. 자바 EE : 자바를 이용한 서버측 개발을 위한 플랫폼
        2. POJO : 특정한 자바 모델이나 기능, 프레임워크르 따르지 않는 순수한 자바 객체
3. Spring의 특징
    - 경량 컨테이너로서 자바 객체를 직접 관리 : 각각의 객체 생성, 소멸과 같은 라이프 사이클을 관리하며 스프링으로부터 필요한 객체를 얻어올 수 있다.
    - 제어의 역행(IoC)
        - 객체의 생성, 사용, 소멸에 해당하는 생명주기의 관리를 애플리케이션 코드 대신 독립된 컨테이너가 담당한다.
        - 객체간의 연결관계를 런타임에 결정한다.
        - 객체간의 연결관계가 느슨해짐
    - DI : 의존성 주입
        - Spring IoC 컨테이너의 구체적인 구현 방식
        - 각 클래스 간의 의존관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것
        - 개발자들은 빈설정 파일에서 의존관계가 필요하다는 정보를 추가하면 된다.
        - 코드가 단순해진다
    - AOP(관점 지향 프로그래밍)
        - 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화 하는것
        - 간단한 설정만으로도 공통 기능을 여러 클래스에 적용할 수 있음
        - ex) 웹 애플리케이션의 보안, 로깅, 트랜잭션 등의 공통 관심 사항
    - 스프링은 영속성과 관련된 다양한 서비스를 지원 (ex. MyBatis, Hibernate등 이미 완성도가 높은 데이터 베이스 처리 라이브러리와 연결할 수 있는 인터페이스 제공)
    - 스프링은 확장성이 높음
4. Spring MVC구조의 처리과정
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b11ca52c-06dd-4769-a101-cdfce09feecb/Spring_MVC_.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b11ca52c-06dd-4769-a101-cdfce09feecb/Spring_MVC_.png)
    
    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d03d966-d672-4a93-9e0d-2f5528ee082e/Spring_MVC___.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d03d966-d672-4a93-9e0d-2f5528ee082e/Spring_MVC___.png)
    
    - DispatcherServlet : 애플리케이션으로 들어오는 모든 Request를 받는 관문
        
        클라이언트의 요청을 전달받아 요청에 맞는 컨트롤러가 리턴한 결과값을 View에 전달하여 알맞은 응답을 생성
        
    - HandlerMapping : 클라이언트의 요청 URL을 어떤  컨트롤러가 처리할지 결정
    - Controller : 클라이언트의 요청을 처리한 뒤, 결과를 DispatcherServlet에게 리턴
    - ModelAndView : 컨트롤러가 처리한 결과 정보 및 뷰 선택에 필요한 정보를 담음
    - ViewResolver : 컨트롤러의 처리 결과를 생성할 뷰를 결정
    - View : 컨트롤러의 처리 결과 화면을 생성
    - 동작과정
        1. 클라이언트가 서버에 요청을 하면, front controller인 DispatcherServlet 클래스가 요청을 받는다.
        2. DispatcherServlet는 프로젝트 파일 내의 servlet-context.xml 파일의 @Controller 인자를 통해 등록한 요청 위임 컨트롤러를 찾아 매핑(mapping)된 컨트롤러가 존재하면 @RequestMapping을 통해 요청을 처리할 메소드로 이동한다.
        3. 컨트롤러는 해당 요청을 처리할 Service(서비스)를 받아 비즈니스로직을 서비스에게 위임한다.
        4. Service(서비스)는 요청에 필요한 작업을 수행하고, 요청에 대해 DB에 접근해야한다면 DAO에 요청하여 처리를 위임한다.
        5. DAO는 DB정보를 DTO를 통해 받아 서비스에게 전달한다.
        6. 서비스는 전달받은 데이터를 컨트롤러에게 전달한다.
        7. 컨트롤러는 Model(모델) 객체에게 요청에 맞는 View(뷰) 정보를 담아 DispatcherServlet에게 전송한다.
        8. DispatcherServlet는 ViewResolver에게 전달받은 View정보를 전달한다.
        9. ViewResolver는 응답할 View에 대한 JSP를 찾아 DispatcherServlet에게 전달한다.
        10. DispatcherServlet는 응답할 뷰의 Render를 지시하고 뷰는 로직을 처리한다.
        11. DispatcherServlet는 클라이언트에게 Rendering된 뷰를 응답하며 요청을 마친다.
    - DispatcherServlet의 장점 :  dispatcher-servlet이 해당 애플리케이션으로 들어오는 모든 요청을 핸들링해주면서 web.xml의 역할을 상당히 축소시켜주었다.
    - xml파일은 모두 객체(Bean)를 정의한다.
        - web.xml : Web Application의 설정(?)을 해주는 파일로서 XML 형식의 파일. ServletContext의 초기 파라미터, Session유효시간, Servlet/JSP에 대한 정의 및 매핑, Welcom File list 등이 작성됨
        - root-context.xml : 이 context에 등록되는 Bean들은 모든 context에서 사용되어 진다.(공유가 가능하다) 스프링 프로젝트 생성 시 root-context.xml에는 특별한 설정이 없다. 공통적으로 사용하려는 Bean을 그때그때 사용
        - servlet-context.xml : web.xml에서 DispatcherServlet 등록 시 설정한 파일. 이 context에 등록되는 Bean들은 servlet-container에만 사용되어진다.

5. REST API

- 웹(HTTP)의 장점을 최대한 활용할 수 있도록 만들어진 아키텍쳐
- REST API 구성
    - 자원(Resource) - URI
    - 행위(Verb) - HTTP METHOD
    - 표현(Representations)
        - URI란? 인터넷 자원을 나타내는 고유 식별자
- HTTP METHOD
    
    [제목 없음](https://www.notion.so/3c16b5b97f2846719ad17477fcd1affb)
    
- REST API 디자인 가이드
    - URI는 정보의 자원을 표현해야한다
    - 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.
- REST의 특징
    - 유니폼 인터페이스 : URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일
    - 무상태성 : 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다. 세선 정보나 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API서버는 들어오는 요청만을 단순하게 처리하면 됨
    - 캐시 가능 : REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. HTTP가 가진 캐싱 기능이 적용 가능하다.
    - 자체 표현 구조 : REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것입니다.
    - Client - Server 구조 : REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됩니다.
    - 계층형 구조 : REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

6.  Spring Annotation

- 컴파일러를 위한 정보를 제공하기 위한 용도.
- @를 이용해서 특별한 의미를 부여한다.
- 종류
    - Bean VS Component
        - 둘 다 목적이 명확하지 않을 때 사용
        - 각자 선언할 수 있는 타입이 정해져 있어 해당 용도 외에는 컴파일 에러가 발생
        - Bean : (개발자가 컨트롤 불가능한) 외부라이브러리들을 Bean으로 등록하고 싶을때
        - Componente : 개발자가 직접 컨트롤이 가능한 클래스일때
    - Controller VS WebServlet
        - 서블릿을 선언할 때 사용
        - Servlet Container에 의해 처리
        - WebServlet과 Spring MVC Controller는 같은 일을 하는 데 사용된다
        - Spring MVC의 Controller를 실행하기 위해서는 애플리케이션에 필요한 jar를 패키징해야 한다.
    - Service : 서비스영역
    - Repository : DAO
    

7. get/post방식의 차이

- get,post 모두 클라이언트가 서버로 요청을 보내는 방법입니다.
- get의 경우 URL에 변수(데이터)를 포함시켜서 요청
- URL에 데이터가 노출되어도 문제가 없을경우에 사용합니다.
- 간단한 데이터를 빠르게 전송이 가능합니다.
- 데이터 양에 제한이 있습니다.
- POST방식은 URL과 별도로 HTTP header뒤에 body에 입력스트림 데이터로 전달됩니다.
- 데이터의 제한이 없고 get보다 최소한의 보안 유지 효과가 있습니다.
- get방식보다는 느리다는 단점이 있습니다.
