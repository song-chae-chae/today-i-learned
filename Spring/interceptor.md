# Today I Learned

|date|ver|
|----|----|
|2022-12-22| v1.0|

---
## 오늘 배운 것

### interceptor
* 컨트롤러에 들어오는 요청(HttpRequest), 응답(HttpResponse)을 가로채는 역할
* 클라이언트가 서버에 url 통해서 Request 객체를 보내면 DispathcerServlet이 해당 Request 객체를 분석하여 HandlerMapping에 사용자 요청을 처리할 Handler 찾도록 요청 -> HandlerExecutionChain이 동작해 하나 이상의 Handler interceptor를 거쳐서 컨트롤러 실행되도록 구성
* 인증 용도로 사용 가능
* Servlet의 앞, 뒤에서 HttpRequest, HttpResponse를 가로채는 Filter와 유사한 역할

### interceptor VS Filter
|구분|interceptor|Filter|
|---|----|---|
| 호출 시점 | DispatcherServlet 실행 후 | DispatcherServlet 실행 전 |
| 설정 위치 | spring-servlet.xml | web.xml |
| 구현 방식 | 설정 + 메서드 구현 | web.xml |

### HandlerInterceptor 인터페이스 구현
* preHandle(), postHandle(), afterCompletion() 오버라이드
    * preHandle
        * Controller로 가기 전 처리
        * Controller 호출 전 실행
    * postHandle
        * Controller의 Handler 끝난 후 처리
        * Controller 실행된 후 호출
    * afterCompletion
        * view까지 처리된 후 실행됨

### HandlerInterceptorAdaptor 상속
* preHandle, postHandle, afterComplete, afterConcurrentHandlingStarted 메서드 있음
* 필요한거 override 하면 됨