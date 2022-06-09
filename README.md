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
 + 

