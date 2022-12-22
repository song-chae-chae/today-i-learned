# Today I Learned

|date|ver|
|----|----|
|2022-12-22| v1.0|

---
## 오늘 배운 것

### resolver
* HandlerMethodArgumentResolver 인터페이스를 구현
* parameter로 받는 값이 여러 개 존재, 처리하는 코드 중복 발생 시
* Controller에 공통으로 입력되는 parameter들 추가하거나 수정하는 등 여러 공통적인 작업 한번에 처리하고 싶을 때 사용
* 인증 처리 코드 한번에 처리할 수 있음
* 인증에 사용되는 객체가 parameter로 들어온다면, 핸들러에서 해당 parameter 타입인지 판단해서 맞으면 어떤 작업 공통적으로 수행할 지 로직 정의해두면 됨
* 구현한 HandlerMethodArgumentResolver를 @Configuration 붙어있는 WebMvcConfigurer 구현한 클래스에서 addArgumentResolvers 메서드를 통해 등록해야 함