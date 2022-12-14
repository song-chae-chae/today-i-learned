# Today I Learned

|date|ver|
|----|----|
|2022-11-27| v1.0|
---
## 오늘 배운 것
### TCP(Transmission Control Protocol)
* 전송 제어 프로토콜
* 두 개의 호스트를 연결하고 데이터 스트림을 교환하게 해주는 네트워크 프로토콜
* 패킷 소실 방지
* 데이터 순서 보장
* 프로그램에서 http 메시지 작성하면 소켓 라이브러리 통해서 OS 계층에 메시지 전달하고 OS에서  메시지 데이터를 포함한 TCP 정보 생성한다.
* 생성된 TCP 정보에 IP 정보까지 씌워서 패킷을 생성함

### TCP/IP 패킷 정보
* TCP
    * 출발지 port, 목적지 port, 전송 제어, 순서, 검증 정보 등
* IP
    * 출발지 IP, 목적지 IP 등

### TCP 특징
* 연결 지향 - TCP 3 way handshake
    * SYN -> SYN + ACK -> ACK -> 데이터 전송
        * SYN : 접속 요청
        * ACK : 요청 수락
    * 가상 연결
        * 실제로는 중간 노드들 있으니 물리적으로 연결됐다는 의미 X
        * 다만 연결되었지 여부는 확인할 수 있으니 가상연결되었다고 표현
* 데이터 전달 보증
    * 데이터 전송 후 잘 받았다는 응답 보냄
* 순서 보장
    * 패킷 순서대로 오지 않으면 잘못된 패킷부터 다시 보내라는 요청 보냄
* 신뢰 가능한 프로토콜