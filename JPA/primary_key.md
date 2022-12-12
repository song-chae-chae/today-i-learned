# Today I Learned

|date|ver|
|----|----|
|2022-12-12| v1.0|
---
## 오늘 배운 것
### 기본키 전략
* Identity 전략
    * auto-increment 사용
    * PK 생성 권한을 DB에 위임
    * 영속성 컨텍스트에 객체 저장할 때 key로 PK를 받는데 문제 발생
    * 예외적으로 persist 하는 순간에 DB에 Insert 쿼리 날림
        * 쓰기 지연 이점 X
* Sequence 전략
    * Insert 쿼리와 상관 없이 DB에서 sequence 만들고, sequence만 호출해서 사용
    * Insert 쿼리 없이 ID 생성 가능
        * 쓰기 지연 이점 O
    * sequence 조회는 필요
    * 만약 1000번의 Insert를 한번에 한다면?
        * sequence 조회 1000번?
        * 너무 비효율적
            * initialValue, allocationSize로 해결
            * allocationSize
                * DB에 sequence를 설정한 개수만큼 올려두고 애플리케이션에서 캐싱해두고 할당된 만큼 사용해서 DB와 건당 통신 없이 PK 생성 가능함
                * 할당된 sequence 다 사용하면 다시 호출함
                * 단일, 다중 서버에서 모두 사용 가능 -> 동시성 이슈 없음
                    * 각각 다른 sequence 할당 받음 (1번 서버에서 1 ~ 51 만큼 받으면 2번 서버는 52 ~ 101 만큼)
                    * 이미 처음에 설정한 개수만큼 올려놓기 때문에 다음에 조회할 때 올려진 sequence를 받으므로 겹칠 일은 없다.
                * sequence call 2번 함
                    * 시작, 끝 value 알기 위해 

