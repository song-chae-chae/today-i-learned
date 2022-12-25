# Today I Learned

| date       | ver  |
| ---------- | ---- |
| 2022-12-25 | v1.0 |

---

## 오늘 배운 것

### Origin

- URL에서 프로토콜, 도메인, 포트 번호를 합친 부분을 의미

### 브라우저 보안 정책

- SOP(Same Origin Policy)
  - 다른 Origin으로 요청을 보낼 수 없도록 금지하는 브라우저의 기본 보안 정책
- CORS
  - 서로 다른 Origin끼리 데이터 주고 받기 위해 지켜야 하는 `정책`
  - SOP에 의해 막힐 요청을 풀어주는 정책

### CORS(Cross-Origin Resource Sharing)

- 동작 원리
  - 다른 Origin으로 요청 보낼 때, Origin 헤더에 자신의 Origin 설정
  - 서버로부터 응답 받으면 Access-Control-Allow-Origin 헤더에 설정된 Origin 목록에 요청된 Origin의 헤더 값 포함되는지 검사
  - CORS 요청 위해서는 서버에서 응답의 Access-Control-Allow-Origin 헤더에 허용되는 Origin 목록 or 와일드카드 설정해주면 됨
