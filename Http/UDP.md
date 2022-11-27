 # Today I Learned

|date|ver|
|----|----|
|2022-11-27| v1.0|
---
## 오늘 배운 것
### UDP(User Datagram Protocol)
* 사용자 데이터그램 프로토콜
* 하얀 도화지에 비유 (기능 거의 없음)
    * TCP는 사용자가 최적화하기 힘듦
    * UDP 사용해서 사용자 맘대로 최적화 가능
* 연결지향 - TCP 3 way handshake X
* 데이터 전달 보증 X
* 순서 보장 X
* TCP에 비해 단순하고 빠름
* IP와 거의 같음, port, 체크섬 정도만 추가되어 있음
* 애플리케이션에서 추가 작업 필요함