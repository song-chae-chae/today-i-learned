# Today I Learned

|date|ver|
|----|----|
|2022-12-13| v1.0|
---
## 오늘 배운 것
### JPA의 데이터 타입
* 엔티티 타입
    * @Entity로 정의하는 객체
* 값 타입
    * 단순히 값으로 사용하는 자바 기본 타입이나 객체

### 값 타입
* int, Integer, String 처럼 단순히 값으로 사용하는 자바 기본 타입이나 객체
* 식별자 없이 값만 있음
    * 변경 시 추적 불가
* 종류
    * 기본값 타입
        * 자바 기본 타입 (primitive type)
        * 래퍼 클래스
        * String
    * 임베디드 타입(복합 값 타입)
    * 컬렉션 값 타입
* 특징
    * 생명주기를 값 타입 소유한 엔티티에 의존
    * 공유하면 안됨
    * 자바의 기본 타입은 공유되지 않음 (항상 값 복사)
    * 래퍼 클래스나 String 클래스는 공유가능하나, 불변 객체임
    * 문제는 임베디드 값 타입 
### 임베디드 타입
* 새로운 값 타입을 직접 정의
* 정의하는 쪽에 @Embeddable
* 사용하는 쪽에 @Embedded
* 주로 기본 값 타입 모아서 만들어서 복합 값 타입이라고 함
* 기본 생성자 필수
* 엔티티의 값일 뿐, 사용한다고 매핑 테이블 달라지지 않음
* 엔티티에서 같은 값 타입 여러개 사용할 수 있도록 override 가능
* 장점
    * 재사용 ↑
    * 높은 응집도
    * 의미 있는 메서드 만들어서 사용하기 좋음
* 사용 시 주의점
    * 값 타입 여러 엔티티에서 공유하면 위험
    * 객체 타입의 경우 하나 바꾸다가 다 같이 바뀌는 수가 있음
    * 실제 인스턴스 이용해서 바꾸지 말고 값을 복사해서 사용하는게 안전
    * 근데 실수하기 쉬움
    * 아예 한번 생성되면 바꾸지 못하도록 제약을 주는 편이 안전(불변객체로 만들기)
    * 수정자를 없애고, 생성 시에만 값 할당 가능하도록 하는 등
* 타입 비교
    * == 비교 하면 다른 인스턴스이기 때문에 무조건 false 나옴
    * 값이 같다면 같은 객체로 보기 위해 equals, hashcode 재정의 해서 사용하기(동일성 말고 동등성 비교)

### 값 타입 컬렉션
* 값 타입을 하나 이상 저장할 때 사용
* @ElementCollection, @CollectionTable 사용
* 컬렉션 저장 위한 별도의 DB 테이블 필요
    * DB는 컬렉션을 같은 테이블에 저장하지 못하기 때문
* 제약사항
    * 식별자 개념 없기 때문에 값 변경하면 추적 어려움
    * 컬렉션에 변경 사항 발생 시, 주인 엔티티와 연관된 모든 값 타입 데이터 삭제하고, 현재 값 타입 컬렉션에 있는 값을 다시 저장
    * OrderColumn 옵션 쓰면 어느정도 해결은 되긴 하지만..
    * 걍 안쓰는게 좋음 완전 원하는대로 동작하지 않음
    * 굉장히 비효율적
    * 값 타입 컬렉션을 매핑하는 테이블은 모든 컬럼을 묶어서 기본키 구성해야 함
* 대안
    * 식별자가 필요하고, 변경이 추적이 필요한 순간부터 값 타입이 아니라 엔티티로 만들어야 함
    * 값 타입 컬렉션 대신 일대다 관계를 고려
    * 일대다 관계를 위한 엔티티 만들어서 그 안에서 필드로 값 타입을 들고 있도록
    * 엔티티로 값타입 객체를 한번 Wrapping 하는거
    * 단방향 혹은 양방향으로 사용 가능
* 결론
    * 값타입은 정말 단순한 경우에나 사용하셈
    * 식별자 필요하고, 값 추적, 변경 필요하면 그건 엔티티로 만드는게 맞는거!
* 엔티티 VS 값 타입
    * 엔티티
        * 식별자 있음
        * 스스로 생명주기 관리
        * 공유 가능
    * 값타입
        * 식별자 없음
        * 생명주기 엔티티에 의존(자아 없음)
        * 공유하면 안됨 -> 불변객체로 사용