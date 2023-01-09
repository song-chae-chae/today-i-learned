# Today I Learned

| date       | ver  |
| ---------- | ---- |
| 2023-01-02 | v1.0 |
| 2023-01-09 | v1.1 |

---

## 오늘 배운 것

### Optional

- orElse VS orElseGet

  - `orElse`는 Optional 값의 유무와 상관없이 무조건 수행됨
  - 새로운 객체를 생성하거나 새로운 연산 하는 경우는 사용 X
  - `orElseGet`은 값이 없을 때만 사용됨

- `Optional<List<T>>`
  - 이렇게 쓸 필요가 없다.
  - Optional을 사용하는 이유
    - NPE를 방지하고 다른 방식으로 null을 처리하기 위함
    - List에 아무 값이 들어오지 않는다면 null이 아니라 빈 List로 리턴될 것 -> NPE가 절대 발생하지 않음
