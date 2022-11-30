# Today I Learned

|date|ver|
|----|----|
|2022-11-30| v1.0|
---
## 오늘 배운 것
### prototype bean 사용 주의점
* 대부분의 spring bean은 singleton
* singleton bean이 prototype bean과 의존관계를 가지면 문제 발생
* singleton bean이 생성되면서 spring container에 prototype bean을 요청하고 spring container가 내려갈 때까지 prototype bean을 계속 가지고 있음
* prototype bean을 사용하는 이유가 호출할 때마다 새로운 인스턴스 사용하기 위함인데 singleton처럼 사용되버림

### ObjectProvider 사용
* provider.getObject() 하면
    * 스프링 컨테이너에서 bean을 찾아서 반환해줌
    * ApplicationContext를 직접 사용하는게 아니라 provider가 찾는 기능만 대신 해줌
* prototype bean 전용으로 사용하는게 아니라, spring container 통해서 bean 찾는걸(dependency lookup) 간단하게 도와주는게 핵심임
* 나 대신 조회해주는 대리자

### Proxymode 사용
* 의존관계 주입 시점에 진짜 bean이 아니라 prototype bean 을 상속받은 프록시 개체가 호출되고, 실제 bean이 사용되야 하는 시점에 BeanFactory에서 실제 객체를 찾아서 로직 수행되도록 함
* BeanFactory에서 찾는 과정에서 Prototype scope 이므로 호출될 때마다 새로운 객체가 생성됨