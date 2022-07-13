## 1. 로깅 간단히 알아보기

System.out.println() 대신 사용하는 로깅 시스템이다.  
스프링 부트 라이브러리를 사용하면 스프링 부트 로깅 라이브러리가 함께 포함된다.  

SLF4J와 Logback 이 두가지이다.  

SLF4J 라이브러리에는 다양한 로그 라이브러리가 들어있다.  

SLF4J는 인터페이스고, 구현체가 Logback 같은 로그 라이브러리라고 생각하면 된다.

> @RestController를 배우게 되는데, @Controller와 차이점이라면  
@Controller는 return시 반환되는것이 view 이름이 반환되는것이다.  
> 
> 그런데 @RestController를 입력하게 되면 return시 String이 바로 반환되게 된다.  
(해당 내용은 차후에 설명해주신다 하였다.)

log를 통해서 출력을 하게 되면 스레드의 정보, 컨트롤러의 이름, 메세지 까지 출력이 되다보니 많은 정보를 통해서 위치를 바로 찾을 수 있는 장점이 있다.

그리고 가장 중요한 기능으로는 trace, debug, info, warn, error의 로그를 출력할 수 있다.  

그 설정들을 application.properties 파일에서도 로그 레벨별로 제어가 가능하다.  

> `#hello.springmvc 패키지와 그 하위 로그 레벨 설정`
> `logging.level.hello.springmvc=trace`

상단처럼 입력하게 되면 "trace부터 모두 보여주겠다.(trace->debug->info->warn->error)" 라는 형태이다.  
LEVEL : `TRACE > DEBUG > INFO > WARN > ERRO`  
주로 운영서버에는 info부터 남긴다. 로컬에는 trace, debug를 사용하기도 한다.

명시를 안할 경우 info 부터 출력된다. 기본 설정이기 때문이다.  

출력할 때 `log.trace("trace log={}", name);` 형태로 출력하지않고  
`log.trace("trace log=" + name);` 형태로 출력하게 된다면 문자와 함께 해당 정보가 더해져서 보여지다보니 쓸모없는 리소스가 발생하는 것이다.  

설정을 통해서 파일로 로그을 남기거나 네트워크로 전송도 가능하다.

## 2. 요청 매핑

@RestController에 대한 내용을 한번 더 설명해준다. 뒤에서 더 자세히 설명을 해준다고 한다.  
RequestMapping에 대해 설명해주는데 Url 호출이 오면 이 메서드가 실행되도록 매핑한다.  
배열 설정도 가능하다.`{"/hello-basic", "/hello-go"}` OR 조건으로 된다.

method를 지정해주는걸 다시 테스트 한다. GET 방식으로 테스트를 진행하였다.  

그러고서 @GetMapping을 다시 설명해주었다.  

마지막으로는 PathVariable 스타일이라는걸 알려주었다.  
리소스 경로에 식별자를 넣어서 호출하는 형태를 선호한다.  
`@GetMapping("/mapping/{userId}")`

?는 쿼리 파라미터 방식이다. 해당 테스트는 PathVariable 방식인것이다.  
@PathVariable의 이름과 파라미터 이름이 같으면 생략할 수 있다.
다중으로도 사용이 가능하다.  

파라미터로 추가 매핑을 할 경우 특정 파라미터가 있을 때 호출이 가능하도록 설정도 가능하다.  
특정 헤더로도 가능하다.  

미디어 타입 조건으로도 매핑이 가능하다.  
Accept 헤더로도 매핑이 가능하다.  

## 3. 요청 매핑 - API 예시

Postman을 통해서 MappingClassController 테스트를 해봤다.

매핑 방법을 여러가지 예제를 보았다.

## 4. HTTP 요청 - 기본, 헤더 조회

![img.png](img.png)

MultiValueMap은 하나의 키에 여러 값을 받을 때 사용된다.  

## 5. HTTP 요청 파라미터 - 쿼리 파라미터, HTML Form

클라이언트에서 서버로 요청 데이터를 전달할 때 주로 사용되는 방법을 설명해준다.

GET, POST HTTP message body(주로 JSON을 사용)

GET, POST의 전송방식은 구분없이 조회가 가능하다.  

이것을 간단히 요청 파라미터(request parameter) 조회라 한다.

## 5. HTTP 요청 파라미터 - @RequestParam

@Controller를 사용하게 되면 view를 리턴해줘야 한다.  
그럴경우 @ResponseBody을 사용하면 HTTP 응답에 String을 바로 보낼 수 있다.  
이건 후에 추가로 설명을 준다고 하였다.  

@RequestParam을 압축할 수 있는 방법에 대해서 설명을 해준다.  

단순 타입이면 @RequestParam을 생략할 수 있다.  

required를 통해서 필수값 여부를 지정할 수 있다.  

만약 false 형태로 하였을 경우 객채형이 아니라면 에러가 날 수 있다.  

`int a = null` -> Error  
`Integer a = null` -> next  

defaultValue에 대해서도 설명해주었다.  
defaultValue는 값이 없을 경우 기본 값을 지정해주는 속성이다.  
빈 문자의 경우에도 처리가 가능하다.

파라미터를 Map으로도 조회가 가능하다.  

파라미터의 값이 1개가 확실하다면 Map 을 사용해도 되지만, 그렇지 않다면 MultiValueMap 을 사용하면 된다.  

## 6. HTTP 요청 파라미터 - @ModelAttribute

롬복 @Data 를 사용하게 되면,  
@Getter , @Setter , @ToString , @EqualsAndHashCode , @RequiredArgsConstructor 를 자동으로 적용해준다.  

@ModelAttribute 속성을 사용하게 되면 모델 객체가 생성되고, 요청 파라미터의 값도 모두 들어가있다.  

순서로는 예제로 설명하자면  
> HelloData 객체 생성 -> 해당 이름의 객체로 프로퍼티를 찾은 후 프로퍼티의 setter를 호출해서 파라미터의 값을 입력(바인딩)`

이렇게 된다.

@ModelAttribute를 생략할 수 있다. @RequestParam과 혼란이 발생 할 수 있을거라 생각이 들지만 생략시 적용되는 규칙이 있다.  

String, int, Integer 같은 단순 타입의 경우 @RequestParam을 사용하고, 나머지의 경우 @ModelAttribute를 사용한다.  
단, argument resolver 로 지정해둔 타입은 되지 않는다.  
argument resolver는 뒤에서 추가로 설명을 해준다고 한다.

@ModelAttribute 안에 name도 설정해줄 수 있다고 한다.

## 7. HTTP 요청 파라미터 - 단순 텍스트

HttpEntity를 배우게 된다. 메세지 바디 정보를 직접 조회하는 기능으로 요청 파라미터를 조회하는 기능과는 관계가 없다.

요청 파라미터 방식이란 쿼리스트링이나 POST 방식으로 HTML Form 데이터를 전송하는 방식을 말한다.  
`(@RequestParam, @ModelAttribute)`  

RequestEntity와 ResponseEntity를 배우게 되는데 뒤에서 자세히 설명해주신다 하였다.  

요청 파라미터를 조회할 때 : `@RequestParam`, `@ModelAttribute`  
HTTP 메세지 바디를 직접 조회할 때 : `@RequestBody`

## 8. HTTP 요청 파라미터 - JSON

@RequestBody에 직접 만든 객체를 지정할 수 있다.  

생략하게 된다면 값이 들어가지 않게된다.  

그리고 자동으로 @ModelAttribute를 적용하게 된다. 그래서 요청 파라미터를 처리하게 된다.  

## 9. 응답 - 정적 리소스, 뷰 템플릿

@RequestMapping에 대한 사용을 주로 알려준다.  

HTML에 데이터를 보내주는걸 return 해줄 때 사용하는 형태이다.  

void를 반환하는 경우 컨트롤러의 경로 이름과 뷰의 논리적 이름이 같으면 논리적 뷰의 이름으로 진행이 가능하다.  

단, @Controller를 사용하여야 하고, HttpServletResponse , OutputStream(Writer) 같은 HTTP 메시지
바디를 처리하는 파라미터가 없어야 가능하다.  

## 10. HTTP 응답 - HTTP API, 메세지 바디에 직접 입력

HTML이나 뷰 템플릿을 사용해도 HTTP 응답 메시지 바디에 HTML 데이터가 담겨서 전달된다.  

정적 리소스나 뷰 템플릿을 거치지 않고, 직접 HTTP 응답 메세지를 전달하는 경우를 설명한다.  

> IOException을 사용하지 않는 이유..? 궁금하다..
> 답 : 값을 받아오는게 없어서 필요가 없는것이다.

@RestController는 @Controller와 @ResponseBody가 포함된 어노테이션이다.  

## 11. HTTP 메세지 컨버터

메세지 컨버터는 인터페이스로 되어있다.

스프링 부트는 다양한 메시지 컨버터를 제공하는데, 대상 클래스 타입과 미디어 타입 둘을 체크해서
사용여부를 결정한다.

만약 만족하지 않으면 다음 메세지 컨버터로 우선순위가 넘어가게 된다.

그 중 주요한 메세지 컨버터를 알아보자.

* `ByteArrayHttpMessageConverter` : `byte[]` 데이터를 처리한다.
  + 클래스 타입: `byte[]` , 미디어타입: `*/*` ,
  + 요청 예) `@RequestBody byte[] data`
  + 응답 예) `@ResponseBody return byte[]` 쓰기 미디어타입 `application/octet-stream`
* `StringHttpMessageConverter` : `String` 문자로 데이터를 처리한다.
  + 클래스 타입: `String` , 미디어타입: `*/*`
  + 요청 예) `@RequestBody String data`
  + 응답 예) `@ResponseBody return "ok"` 쓰기 미디어타입 `text/plain`
* `MappingJackson2HttpMessageConverter` : application/json
  + 클래스 타입: 객체 또는 `HashMap` , 미디어타입 `application/json` 관련
  + 요청 예) `@RequestBody HelloData data`
  + 응답 예) `@ResponseBody return helloData` 쓰기 미디어타입 `application/json` 관련

## 12. 요청 매핑 헨들러 어뎁터 구조

argument resolver가 파라미터 작업 처리를 도와주고, @RequestBody, @ResponseBody, HttpEntity에 한하여 HTTP 메세지 컨버터를 통해 파라미터 작업 처리를 요청한다.

그렇다보니 핸들러 어댑터는 정말 데이터 호출만 해주는 형태이다.  
