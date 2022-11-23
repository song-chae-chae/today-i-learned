# Today I Learned

|date|ver|
|----|----|
|2022-11-21| v1.0|
|2022-11-23| v1.1|

---
## 오늘 배운 것

### dependency injection
* 의존관계 주입
* A -> B 클래스 간의 의존관계가 있을 때 외부에서 객체를 생성해서 넣어주는 것
* B가 바뀔 때 A도 같이 바꿔야 하는 문제를 방지할 수 있음 (DIP, OCP 규칙)
* 생성자 주입 시 생성자 한개만 있으면 @Autowired 생략 가능
* 의존관계 주입을 위해 Configuration 클래스(@Configuration) 만들어서 구현 객체 생성, 연결을 실행 부분과 분리


### spring bean 등록
* compoment scan으로 등록되게 할 수 있고(@Service, @Repository 등)
* 직접 @Configuration 이용해서 bean 등록 가능
* 최근엔 잘 사용하지 않지만, xml 형식으로도 bean 등록 가능(GenericXmlApplicationContext)

