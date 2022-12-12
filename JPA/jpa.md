# Today I Learned

|date|ver|
|----|----|
|2022-12-06| v1.0|
|2022-12-07| v1.1|
|2022-12-11| v1.2|
|2022-12-12| v1.3|
---
## 오늘 배운 것
### JPA 
* Java Persistence API
* 자바 진영의 ORM 기술 표준
    * ORM
        * Object-Relational mapping(객체 관계 매핑)
        * 객체는 객체대로, 관계형 DB는 관계형 DB대로
        * ORM 프레임워크가 중간에서 매핑 해줌
* Java 애플리케이션과 JDBC 사이에서 동작
* 인터페이스의 모음
* 구현체로 Hibernate 등 사용

### jpa test
* @Test 와 @Transactional 이 같이 붙어있으면
    * 테스트 끝난 후 롤백해버린다. -> insert의 경우 DB에 insert문을 날리지 않음
    * 롤백하기 싫으면 @Rollback(false)

### 영속성 컨텍스트
* 같은 transaction 안에서 저장하고 조회하는 경우 영속성 컨텍스트가 같음
    * 영속성 컨텍스트 안에서는 id 값 같으면 같은 엔티티로 인식
    * 이미 있으니까 조회 새로 하지 않고 1차 캐시에서 가져옴


### Cascade
* CascadeType.ALL
 * 모든 엔티티는 save 할 때, 각각 persist 해줘야 하지만 연관된 애한테 옵션 주면 같이 persist 해줌
 * 범위에 대한 문제
    * 어디까지 CascadeType.ALL 적용할지?
    * private owner 일 때 사용하면 좋음 - 다른 객체랑은 관계 없고, 현재 관계만 있을 때

### persist
* entityManager.persist(obj)
    * 객체를 영속성 컨텍스트에 넣고 트랜잭션이 커밋되는 시점에 DB에 반영됨(insert 쿼리 날라가는거)
    * 영속성 컨텍스트에 key, value 있음
    * 이때 key는 DB PK랑 매핑한 애임 -> 엔티티의 @Id 붙은 애
    * DB에 값 넣기 전이어도 객체에 PK 채워져 있는거 보장됨
* jpql 사용
    * sql 쿼리랑 문법 거의 비슷한데 from 의 대상이 sql은 테이블이고, jpql은 엔티티인거

### EntityManager
* repository에서 사용할 때, @PersistenceContext 붙여서 entity manager 주입 해줘야 하는데 
* Spring Data JPA에서는 생성자 주입 가능함(@Autowired 로 바꿔줘서)

### flush
* 영속성 컨텍스트의 변경 내용을 DB에 동기화
* 영속성 컨텍스트를 비우지 않음
* commit 직전에 동기화
* commit과는 다름
* flush 면 rollback 가능하지만 commit하면 rollback 불가능

### N + 1 문제
* 연관관계가 있는 객체 조회 시, 객체 한 개당 연관된 객체까지 같이 조회하면서 쿼리가 추가로 발생하는 문제
    * ex) 객체가 3건 조회되었다면, 연관된 객체를 추가로 3번 더 조회함
* 즉시, 지연 로딩이든 상관없이 발생
* N번의 추가 쿼리 발생 시점의 차이만 있음

### N + 1 해결 방법
* fetch join
    * JPQL에서 제공
    * 지연 로딩이 걸려있는 연관관계에 대해서 한번에 같이 즉시로딩해줌
    * 연관된 객체의 모든 정보를 하나의 객체로 한번에 불러옴
    * 일반 조인은 조회하는 주체 entity만 영속화하기 때문에 연관 entity가 필요하면 추가 쿼리 발생함
    * fetch join은 조회 주체 entity 외에 연관 entity 모두 select 하면서 전부 영속화
    * 지연 로딩이어도 이미 전부 가져왔기 때문에 영속성 컨텍스트에 연관된 엔티티도 다 들어있고 추가 쿼리 발생하지 않음
* fetch join 단점
    * 일반 조인과 달리 엔티티의 특정 속성만 가져오기 불가능 (성능 이슈 가능성)
    * 둘 이상의 컬렉션은 불가능
    * 페이지네이션 불가능
        * JPQL에서 만드는 쿼리에 페이징 처리에 사용하는 limit이 적용되지 않음
        * 모든 값을 select해서 불러와서 인메모리에 저장하고 application 단에서 필요한 수만큼 반환 -> 페이징 효과 없음
        * 이렇게 하는 이유는 -> 중복된 데이터가 있을 수 있으니 limit, offset을 무시하고 일단 다 가져옴
* pagination 해결책
    * ToOne 관계에서 페이징하기
        * fetch로 가져오는게 1개 -> 메모리 부담 X
    * batch size
        * SQL where ~ in 절 사용
        * 지연로딩으로 쿼리 실행될 때, batch size 옵션에 지정한 만큼의 크기를 미리 가져옴
        *  1건씩 n번 조회할걸 단축할 수 있음
        * n > batch size 인 경우 batch size만큼 나눠서 여러번 쿼리 날림
        * N + 1 문제 부분 해결 (1 + N + N -> 1 + 1 + 1로)


