# Today I Learned

| date       | ver  |
| ---------- | ---- |
| 2022-12-24 | v1.0 |
| 2022-12-27 | v1.1 |

---

## 오늘 배운 것

### spring security

- 별도의 설정이나 구현 없이 기본적인 웹 보안 기능 연동
  - 모든 요청은 인증 필요
  - 인증 방식
    - 폼 로그인 방식
    - httpBasic 로그인 방식
  - 기본 로그인 페이지 제공
  - 기본 계정 제공(user/랜덤 문자열)

### CORS

- spring security에서 별도로 CORS 관련 설정해줘야 함
