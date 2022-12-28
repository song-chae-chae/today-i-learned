# Today I Learned

| date       | ver  |
| ---------- | ---- |
| 2022-12-24 | v1.0 |
| 2022-12-28 | v1.1 |

---

## 오늘 배운 것

### JWT(Json Web Token)

- 정보를 JSON 객체로 안전하게 전송하기 위한 간결하고 독립적인 방법을 정의하는 개방형 표준(RFC 7519)
- 사용자를 인증, 식별하기 위한 토큰 기반 인증
- 비밀키 또는 공개/개인키 쌍을 사용해 서명
- 세션과 달리 클라이언트에 저장함으로써 세션 관리를 위한 DB 접근 등을 덜 수 있음
- RESTful과 같이 무상태(stateless) 환경에서 사용자 데이터 주고 받을 수 있음

### JWT 구조

- Header - Payload - Signature 로 구성
- .으로 구분되고, 순서대로 이어져있는 문자열
- Header
  - 토큰 타입, 알고리즘 방식 지정하여 서명 및 토큰 검증에 사용
- Payload
  - 토큰에서 사용할 정보의 조각(claim)이 담겨 있음
  - 토큰 발급자, 제목, 대상자, 만료 시간, 활성 날짜, 발급 시간, 토큰 식별자 등 토큰 정보를 표현하기 위해 정해진 종류의 `등록된 클레임(Register claim)`
  - 공개, 비공개 클레임이 있음
- signature
  - 토큰 인코딩, 유효성 검증할 때 사용하는 고유한 암호화 코드

### access token과 refresh token

- access token 안에 토큰 정보, 전달할 정보, 서명까지 담아서 header에 담아 client단으로 넘겨줌
- session과 달리 토큰 자체가 정보를 가지고 있기 때문에, 탈취 위험 고려가 필요함
  - 민감한 정보는 토큰에 담지 않기
- access token이 탈취될 경우, access token의 유효기간이 끝나기 전까지는 탈취범이 해당 토큰을 자유롭게 악용할 수 있기 때문에, access token의 유효기간은 짧게 하고, refresh token을 추가로 발급
- access token이 만료되면 refresh token을 서버로 보내 검증을 거친 후 access token을 다시 발급해주는 형식
- refresh token은 access token 보다 유효기간이 길고 DB에 저장
