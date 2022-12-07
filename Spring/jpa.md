# Today I Learned

|date|ver|
|----|----|
|2022-12-06| v1.0|
|2022-12-07| v1.1|

---
## 오늘 배운 것

### jpa test
* @Test 와 @Transactional 이 같이 붙어있으면
    * 테스트 끝난 후 롤백해버린다. -> insert의 경우 DB에 insert문을 날리지 않음
    * 롤백하기 싫으면 @Rollback(false)

### 영속성 컨텍스트
* 같은 transaction 안에서 저장하고 조회하는 경우 영속성 컨텍스트가 같음
    * 영속성 컨텍스트 안에서는 id 값 같으면 같은 엔티티로 인식
    * 이미 있으니까 조회 새로 하지 않고 1차 캐시에서 가져옴

### 연관관계
* 모든 연관관계는 지연로딩으로 설정해라 (ManyToOne, OneToOne 은 FetchType.EAGER 가 디폴트 이므로 LAZY로 변경해주기)
* 즉시로딩은 예측 어렵고, JPQL 실행 시 n + 1 문제가 자주 발생

### Cascade
* CascadeType.ALL
 * 모든 엔티티는 save 할 때, 각각 persist 해줘야 하지만 연관된 애한테 옵션 주면 같이 persist 해줌

### 양방향 연관관계(다대일, 일대다 예시)
* 테이블은 FK 하나로 양방향 연관관계 맺음
* 객체는 단방향 연관관계(참조) 2개로 양방향 연관관계를 맺음
* 객체와 테이블의 간극을 메우기 위해 객체의 연관관계 2개 중 하나만 FK를 관리하는 연관관계의 주인이 됨
* 실제 테이블에서 FK를 소유하고 있는 쪽의 엔티티가 FK를 관리하는 것이 더 비용 절감되니까, FK 소유한 `다` 쪽이 연관관계의 주인이 됨
* 연관관계 주인 쪽에서는 @JoinColumn 으로 외래키 명시해주고
* 다른 연관관계는 mappedBy 속성을 통해 주인이 아님을 명시

### 연관관계 편의 메서드
* 양방향 연관관계가 있을 때, 순수한 객체 관점에서 양쪽 방향(연관관계)에 다 필드 채워져야 함
    * ex) JPA 사용하지 않는 테스트
* 이 때, 각각 채워주면 실수할 확률이 높으니, 둘 중 한 곳에서 한번에 연관관계 있는 엔티티들 다 채워주면 좋음(setter 활용)

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
* 영속성 컨텍스트에 있는 내용을 DB에 동기화
* commit과는 다름
* flush 면 rollback 가능하지만 commit하면 rollback 불가능