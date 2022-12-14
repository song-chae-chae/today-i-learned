# Today I Learned

|date|ver|
|----|----|
|2022-11-28| v1.0|
---
## 오늘 배운 것
### spring bean 여러 개 조회될 때
* @Qualifier
* @Primary 

### spring bean 생명주기 콜백
* 객체의 초기화, 종료 작업 필요한 경우
    * 데이터베이스 커넥션 풀, 네트워크 소켓 등
* 객체 생성, 의존관계 주입 완료되어야 필요한 데이터 사용할 수 있는 준비 완료됨
* 초기화 작업은 의존관계 주입 모두 완료된 뒤 호출해야 하는데, 완료 시점을 알기 위해 스프링에서 의존관계 주입 완료되면 스프링 빈에 콜백 메서드를 통해서 초기화 시점을 알려주는 다양한 기능 제공
* 스프링 컨테이너 종료되기 직전에 소멸 콜백도 줌(싱글톤 빈일경우)
* 생명주기 짧은 빈들도 있음
    * 컨테이너와 무관하게 빈 종료되기 직전에 소멸 전 콜백 발생함

### spring bean 이벤트 라이프 사이클
* 스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존관계 주입 -> 초기화 콜백 -> 사용 -> 소멸 전 콜백 -> 스프링 종료

### 객체 생성과 초기화는 분리하라.
* 생성자의 역할은 필수 정보 받고, 메모리 할당해서 객체 생성하는 것까지만 하기
* 초기화는 생성된 값 활용해서 외부 커넥션 연결하는 등 `무거운 동작` 수행

