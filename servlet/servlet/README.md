# 스프링 MVC 1편 - 백엔드 웹 개발 헥심 기술

## 1. Hello 서블릿
 + 요청 메세지를 간편하게 확인하려면 retources의 application.properties에 하단 부분을 추가해주면 된다. (단, 운영서버에 이렇게 작업을 하면 성능저하가 발생할 수 있으므로 개발 단계에서만 적용하여야 한다.) 
 > logging.level.org.apache.coyote.http11=debug

## 2. HTTP 요청 데이터 - 개요
HTTP 요청 메세지를 통해 클라이언트에서 서버로 데이터를 전달하는 방법
 1. GET - 쿼리 파라미터
 2. POST - HTML Form
 3. HTTP message body
 
## 3. HTTP 요청 데이터 - GET 쿼리 파라미터
 + 받는 방식에는 전체 파라미터, 단일 파라미터, 복수 파라미터가 있다.
 + 복수 파라미터가 생겼을 경우 values를 붙이면 된다.
 > 단일 : request.getParameter("username");\
 > 복수 : request.getParameterValues("username");

## 4. HTTP 요청 데이터 - POST HTML Form
 + 파라미터 형식이 GET 형태와 동일한 쿼리 파라미터 방식이다. 그러므로 getParameter로 값을 가져올 수 있다.

## 5. HTTP 요청 데이터 - API 메시지 바디
 + 스프링 부트로 Spring MVC를 선택하면 기본으로 Jackson 라이브러리('ObjectMapper')를 제공한다.
 > 형태 : {"username": "hello", "age": 20}

## 6. HttpServletResponse - 기본 사용법
 + 편의 기능으로 Content-Type, 쿠키, Redirect가 있다.

## 7. HTTP 응답 데이터 - API JSON
 + application/json 은 스펙상 utf-8 형식을 사용하도록 되어있다. 그래서 스펙에 utf-8을 작업하지 않아도 된다.

## 8. 프론트 컨트롤러
 + 프론트 컨트롤러 서블릿 하나로 클라이언트의 요청을 받고 해당 요청에 맞는 컨트롤러를 찾아서 호출
 + 입구 하나로 공통처리가 가능하게 해준다.
 + 프론트 컨트롤러를 제외한 나머지 컨트롤러는 서블릿을 사용하지 않아도 된다.
 + View 이동 부분이 분리가 가능하다.
 + Model도 분리할 수 있다.
 + 분리 작업과 함께 뷰의 논리 이름을 반환하게 구현하여 물리 뷰를 찾을 수 있게 컨트롤러를 작업할 수 있다.
 + ModelView를 작업하지 않아도 되다보니 편리한것이다.
 + 여러 작업 방식에 따라 구분할 수 있도록 어댑터를 사용하면 좋다.
 + 어댑터를 사용하게 된다면 프레임워크를 유연하고 확장성 있게 설계할 수 있다.

> 서블릿에 종속되지 않는 형태를 구현하기 위해서 작업을 하는 것

## 9. 핸들러 패밍과 핸들러 어댑터
 + 이전에 직접 Spring 만들었던 것에 대한 내용을 자동 제공된다며 설명해주는 시간이였다.

## 10. 스프링 MVC - 시작하기
 + @Controller 어노테이션이 있으면 자동으로 스프링 빈에 등록한다.
 + 컴포넌트 스캔의 대상이 되는것이다.
 + 스프링 MVC에서 어노테이션 기반 컨트롤러로 인식한다. RequestMappingHandlerMapping에서 핸들러 정보라고 인식할 수 있다는 뜻이다.
 + @RequestMapping 으로도 인식시킬 수 있다.(그대신 @Component를 넣어야 한다.)
 + 클래스 레벨에 붙어있어야 한다.
 + @Component을 안적고 @RequestMapping만 적었다면 ServletApplication에서 Bean 등록을 해줘야 한다.

## 11. 스프링 MVC - 컨트롤러 통합
 + 하나의 컨트롤러에 역할을 분담했던 업무를 하나로 합칠수도 있다.
 + 만약 경로가 중복이 있다면 @RequestMapping을 통해서 중복 부분을 제거할 수 있다.
 + @RequestMapping에 명시한 경로에 바로 파일이 있다면 @RequestMapping만 적어두고 경로를 적지 않으면 된다.

## 12. 스프링 MVC - 실용적인 방식
 + ModelAndView를 사용하지 않고 String으로 변환 후 return값도 문자로 넘기면 자동으로 뷰로 판단에서 자동으로 진행된다.
 + 데이터를 받아야 할 경우 받아야되는곳에 HttpServlet(Request/Response)를 사용하지 않고도 @RequestParam으로 직접 명시하여 사용할 수 있다.
 + 그리고 그 값을 Model에 담아서는 사용하면 된다.
 + 그런데 이렇게 코딩할 경우 Request 방식에 대한 제약이 없어서 POST, GET 둘다 가능하다.
 + 그렇다보니 @RequestParam에서 method를 지정하여 제어를 해줘야 한다.
 + 해당 구문보다 더 간결하게는 @GetMapping과 @PostMapping이 있다.


