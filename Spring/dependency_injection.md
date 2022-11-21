# Today I Learned

### date : 2022-11-21

---
## 오늘 배운 것

### dependency injection
* 의존성 주입
* A - B 클래스 간의 의존관계가 있을 때 외부에서 객체를 생성해서 넣어주는 것
* 생성자 주입 시 생성자 한개만 있으면 @Autowired 생략 가능하다.

### spring bean 등록
* compoment scan으로 등록되게 할 수 있고(@Service, @Repository 등)
* 직접 @Configuration 이용해서 bean 등록 가능