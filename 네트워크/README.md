

# 1. OSI 7 Layer(7계층)

: 네트워크 통신 시 송신자와 수신자가 지켜야할 각 단계의 규칙!!


    Application Layer   (7 Layer) : 응용 계층
    Presentation Layer  (6 Layer) : 표현 계층
    Session Layer       (5 Layer) : 세션 계층
    Transport Layer     (4 Layer) : 전송 계층
    Network Layer       (3 Layer) : 네트워크 계층
    DataLink Layer      (2 Layer) : 데이터 링크 계층
    Physical Layer      (1 Layer) : 물리 계층

-> 아파서 티내다 피나다로 외우면 면접에서 대답 못함!!! 

-> 3,4 Layer는 필수적으로 알고 갈것!!

Application(7Layer)에 가까워질 수록 실제 프로그램에 가까워지고 아래로 내려갈수록 물리적 연결 구간에 가까워 집니다.

아래로 내려갈 수록 Protocol Header가 추가되어 계층 정보를 덧붙인다.


### 계층별 간단 요약
- Application Layer (7 Layer, 응용계층) : 사용자가 UI로 접하는 응용 프로그램과 관련된 계층. 여기에 속한 프로토콜들은 어떠한 방봅으로든 사용자와 직접 접하게 됨. (ex : HTTP, SMTP, DNS 등)
- Transport Layer (4 Layer, 전송계층) : 송신자와 수신자의 논리적 연결(Connection)을 담당하는 부분. 신뢰성 있는 연결을 유지하기 위해서 도와줌. 사용자(Endpoint)간의 연결을 생성하고 데이터를 얼마나 보냈는지, 얼마나 받았는지, 제대로 받았는지 등을 확인. (ex : TCP, UDP 등)
- Network Layer (3 Layer, 네트워크 계층) : IP(Internet Protocol)이 활용되는 부분. Endpoint에서 다른 Endpoint로 갈때, 경로와 목적지를 찾아줌. 이를 Routing으로 부름 (ex : 라우터 등)
- DataLink Layer (2 Layer, 데이터링크 계층) : 같은 네트워크 대역을 사용하는 단말들에 대해 신뢰성 있는 전송을 보장. "MAC address"를 활용하여 같은 구간 내의 Endpoint 혹은 Switching 장비에 전달하며,  1 Layer에 해당하는 물리 계층에 생길 수 있는 오류를 찾아냄.
- Physical Layer (1 Layer, 물리 계층) : 물리적인 계층으로 전기적 신호가 전송되는 구간.


### 계층을 나눈 이유?
-> 장애 발생시 어느 구간이 문제가 생겼는지 명확하게 알기 위함.





# . TCP/IP란?
인터넷에서 컴퓨터들이 서로 정보를 주고 받는데 쓰이는 통신 규약의 모음.
인터넷 프로토콜 중 TCP와 IP를 가장 많이 쓰기 때문에 TCP/IT Protocol 로 불림.

- IP : 인터넷 프로토콜

- TCP : 전송 조절 프로토콜

IP는 패킷 전달 여부를 보증하지 않고, 패킷을 보낸 순서와 받는 순서가 다를 수 있다.
TCP : IP위에서 동작하는 프로토콜로, 데이터 전달을 보증하고 보낸 순서대로 받게 해준다.

=> IP주소 체계를 따르고 IP Routing을 이용해 목적지에 도달. TCP의 특성을 활용해 송신자와 수신자의 논리적 연결을 생성하고 신뢰성을 유지하도록 한다.










[참고]
https://aws-hyoh.tistory.com/entry/TCPIP-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0
