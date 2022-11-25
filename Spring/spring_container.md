# Today I Learned

|date|ver|
|----|----|
|2022-11-23| v1.0|
|2022-11-25| v1.1|
---
## 오늘 배운 것

### spring container
* ApplicationContext
* @Configuration 붙은 클래스를 구성 정보로 사용해서, @Bean 붙은 메서드 전부 호출해 반환된 객체를 컨테이너에 등록
* 이때 등록된 객체가 spring bean
* @Bean 붙은 메서드 이름을 spring bean 이름으로 사용
* applicationContext().getBean()으로 spring bean 찾음

### BeanDefinition
* bean 설정 메타 정보
* 스프링이 다양한 설정 형식(java, xml 등)을 지원할 수 있는 이유
* 역할과 구현을 개념적으로 분리 -> XML 읽어서 BeanDefinition 만들고, 자바 코드 읽어서 BeanDefinition 만듦
* bean 등록 방법 크게 두가지로 나눠보면 직접 등록, factory method(우회 등록) 사용
* 직접 등록한 bean의 메타 정보 보면 class 정보 알 수 있음
* factory method로 등록한 bean의 메타 정보 보면 class 정보는 null이고, factory bean을 이용해서 factory method를 호출해서 bean 등록했다는걸 알 수 있음

### life cycle
* spring bean 등록
* 등록된 bean의 연관 관계 주입(@Autowired 있는 애들)