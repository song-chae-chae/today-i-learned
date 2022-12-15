# Today I Learned

|date|ver|
|----|----|
|2022-12-15| v1.0|
---
## 오늘 배운 것
### validation
* JSR-303 표준 스펙
* 빈 검증기를 이용해 객체의 제약 조건 검증하도록 지시하는 어노테이션
* spring-boot-starter-web에 기본으로 들어있던 적도 있었으나, 2.3 이후는 따로 dependency 추가
* 올바르지 않은 데이터 걸러내고 보안 유지 하기 위해 사용
* Controller단에서 API의 request 객체 앞에 @Validated 붙임
* 검증할 객체의 필드에 Validation annotation 추가해 유효성 검사 적용

|종류| |
|----|----|
|@Null|null만 허용|
|@NotNull| `불가` :  null <br /> `가능` : "", " "|
|@NotEmpty| `불가` : null, "" <br /> `가능` : " " |
|@NotBlank(message =)|`불가` : null, "", " "|
|@Email|이메일 형식 검사 <br/> `가능` : "" |
|@Pattern(regexp =) |정규식 검사|
|@Size(min=, max=)|길이 제한|
|@Max(value = )| value 이하의 값|
|@Min(value = )| value 이상의 값|
|@Positive | 양수만|
|@PositiveOrZero | 양수, 0|
|@Negative| 음수만|
|@NegativeOrZero | 음수, 0|
|@Future |  현재보다 미래|
|@Past |  현재보다 과거|
|@AssertFalse | false 여부 <br/> null 체크 X|
|@AssertTrue | true 여부 <br/> null 체크 X|
