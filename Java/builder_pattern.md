# Today I Learned

|date|ver|
|----|----|
|2022-12-15| v1.0|
---
## 오늘 배운 것
### builder pattern
* 복합 객체의 생성 과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴 
* 2 단어 요약: 생성자 오버로딩 [위키백과]
* 장점
    * 가독성
        * 필드 많아질수록 생성자, static 메서드 가독성 매우 안좋아짐
        * 같은 타입의 필드끼리 순서 바뀌어도 알 길이 없음
    * 유연성
        * 필드 추가, 삭제에 기존 코드가 영향 받지 않음
    * 변경 가능성 최소화
        * setter 사용하지 않고 수정할때는 빌더로 새로 만들어주면 변경점 찾기 훨씬 수월
        * final까지 붙일 수 있다면 불변성 확보 ↑
    * 필요한 데이터만 채우기 가능
        * 생성자 or static 메서드 무한으로 생성하지 않아도 됨