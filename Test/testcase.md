# Today I Learned

### date : 2022-11-21

---
## 오늘 배운 것

### test case 작성
* given - when - then 문법을 활용해라
* 테스트를 클래스 단위로 실행하면 테스트 메서드 간의 순서 보장 안된다.
* 테스트 케이스마다 순서랑 상관없이 메서드별로 따로 동작하도록 테스트 끝나고 나면 데이터 없애줘야 함 (@AfterEach 활용)
* assertThrows로 Exception 테스트 할 수 있다.

### @Transactional
* 테스트케이스에 @Transactional 달면 테스트 실행 후 롤백해줌

### 단위테스트
* 하나의 모듈을 기준으로 독립적으로 수행되는 가장 작은 단위의 테스트
* 스프링 컨테이너까지 올려야되는 통합테스트는 시간이 오래 걸린다.
* 단위테스트 케이스를 잘 짤 수 있도록 훈련해야 한다.
* 테스트 주도 개발에서 말하는 테스트도 단위테스트이다.