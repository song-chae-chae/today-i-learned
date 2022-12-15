# Today I Learned

|date|ver|
|----|----|
|2022-12-15| v1.0|
---
## 오늘 배운 것
### @ExceptionHandler
* Controller 계층에서 발생하는 에러를 메서드에서 처리하도록 하는 어노테이션
* service, repository 발생 에러는 제외
* 어떤 Exception 처리할지 속성에 지정 가능
* 구체적인 Exception 지정하는 것이 좋음
* ResponseEntity로 데이터 파싱하지 않는 경우
    * @ResponseStatus에 응답 상태를 직접 지정해줘야 함(기본적으로 200으로 응답되기 때문에)
    * @ResponseBody를 붙여줘야 함

### @ControllerAdvice
* @ControllerAdvice 붙은 클래스 내의 @ExceptionHandler 붙은 메서드에서 해당 예외 처리 가능
* @Controller, handler에서 발생하는 에러 잡아줌
* 속성으로 컨트롤러 범위 설정 가능

### @RestControllerAdvice
* @ControllerAdvice, @ResponseBody 어노테이션 가지고 있어, Response body로 값을 리턴하고 싶을 때 사용

### 가장 깔끔한 조합
* @RestControllerAdvice + ResponseEntity\<T>
