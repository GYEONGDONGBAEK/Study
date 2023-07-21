# Section 1. 인터넷 네트워크

---

## 인터넷 통신

### **인터넷망에서 컴퓨터들은 어떻게 통신할까?**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/632d9749-a1f7-43a4-af0c-f8870da9e100">

만약 우리가 통신해야하는 컴퓨터가 주변에 있다면, 간단히 케이블을 연결하여 바로 통신 할 수 있게

만들면 된다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/78552daf-ee71-4f6c-92dd-a612260d1512">

하지만 만약 클라이언트와 서버 사이의 거리가 너무 멀다면, 인터넷이라는 복잡한 망 속에서 Hello,world! 라는 메세지를 전달해야 한다. 하지만 어떤 규칙으로, 어떻게 전달하는지, 어떻게 안전하게 도착할 수 있는지를 이해하려면 IP 프로토콜에 대한 이해가 필요하다.

---

# IP(인터넷 프로토콜,Internet Protocol)

### IP 주소 부여

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/ece7190d-830f-4492-88a3-607377815f83">

### IP 의 역할

- 지정한 IP 주소 (IP Address)에 데이터 전달
- 패킷 (Packet) 이라는 통신 단위로 데이터 전달

### IP 패킷 정보

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/a756e943-0b47-4412-a02e-1136bf5fe64a">

- 노드끼리는 IP주소를 이용해 데이터를 전달하는데 데이터 전달 단위를 패킷(Packet)이라 한다.
- 패킷은 다음과 같이 구성된다.

     ⇒Payload : 전송하고자 하는 데이터의 한 블록.

     ⇒주소지 정보: 발신지, 목적지 주소

     ⇒관리 정보: Header, IPv6과 같이 망이 패킷을 목적으로 전달하는데 필요한 정보

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/84adb3b8-daf2-4266-863d-62d7319102df">

인터넷에 전송된 패킷은 여러 노드를 거쳐 목적지(서버)에 도달하게 되며 서버는 메세지를 잘 수신했다는 정보를 담아 다시 클라이언트로 보낸다.

---

# IP의 한계

**1. 비연결성**

목적지의 상태를 알 수 없으므로, 패킷이 전송되는 대상이 없거나 대상 서비스가 불능상태이더라도 패킷이 전송된다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/5cea4ee7-dacd-4793-8695-cae2e432a223">

**2. 비신뢰성 (전달보증 및 순서일치 보장 X)**

- 패킷이 손실될 수 있으며, 손실여부를 알 수 없다.
- 패킷이 전달되는 순서가 도착순서와 일치함을 보장하지 못한다. 이더넷 상에서 패킷의 최대크기(MTU)는 1500바이트인데 MTU를 초과하는 데이터의 경우 패킷을 분할해 전달해야 한다. 이때 각 패킷이 최종 목적지로 도달하는데 거치는 노드는 패킷마다 다를 수 있으며 이로 인해 목적지에 도착하는 패킷의 순서가 달라질 수 있다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/062a2b65-9f53-45cb-9576-4be311570361">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/9b4d3194-87f7-41c0-9829-9ecf726fc13e">

**3. 프로그램 구분**

PORT 번호가 없기 때문에 같은 IP로 여러 애플리케이션을 이용할 경우 구분할 수 없다.

이러한 문제점 때문에 신뢰성 있는 통신을 보장하지 못한다.

---

# TCP,UDP

## TCP (전송 제어 프로토콜, Transmission Control Protocol)

IP 패킷 정보가 가지고 있는 한계점(비신뢰성, 비연결성)을 TCP 정보를 통해 해결한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/241b922b-b6c5-4854-92e7-41698880584a">

**TCP의 특징**

**1. 연결 지향 (3-way handshake)**

목적 호스트와 연결이 되어야 메세지를 전송한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/90b18eec-cdaa-4cab-9518-67d9c76ec443">

**2. 데이터 전달 보증**

목적 호스트가 데이터를 받았다면, 송신한 호스트에게 확인 메세지를 보냄으로써 패킷이도착했는지 알 수 있다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/20b7f046-9b7f-4f04-aaa5-5aab7f224430">

**3. 패킷 순서 보장**

목적호스트에 도착한 패킷 순서가 잘못되었을 때 재전송을 요구함으로써 패킷 순서를 보장한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/2ffc4040-a3e2-4e96-aa57-83888c6bf962">

**4. 신뢰할 수 있는 프로토콜**

내가 전송한 데이터가 목적지까지 오류없이 전송됨을 보장한다.

## UDP (사용자 데이터그램 프로토콜, User Datagram Protocol)

TCP와 비교하여 연결지향도 아니고, 데이터 전달, 패킷 순서도 보장되지 않는다.

- 기능이 거의 없기 때문에 **속도가 빠르다**.

- IP와 비슷해 보이지만, PORT정보는 포함되어있고, 체크섬 정도는 추가되어 있다.

- 애플리케이션에서 추가적인 작업이 필요하다.

---

# **PORT**

IP가 인터넷 세계에서 논리적인 내 컴퓨터의 주소라면, PORT는 내 컴퓨터내의 수많은 애플리케이션의 식별자가 되는 경로이다.

(예시: 아파트가 IP 주소라면 각각의 집이 PORT번호가 된다)

**포트범위 및 포트목록**

- 0 ~ 65535
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
- 1024 ~ 49151 : 등록된 포트
- FTP (20, 21)
- SSH (22)
- TELNET (23)
- DNS (53)
- HTTP (80)
- HTTPS (443)

---

# DNS (도메인 네임 시스템, Domain Name System)

IP주소는 외우기도 힘들뿐더러 변경가능성도 있다.

그래서 이런 IP 주소들을 KEY/Value로 우리가 읽기에 가독성도 좋고 외우기도 좋은 도메인을 알아서 IP주소로 매칭하여 찾아주는 DNS 서버가 만들어졌다.

### DNS 서비스 로직

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/f3ca53be-1d39-4a1f-a86c-814986112348">

1. 클라이언트에서는 우리가 알고 있는 [google.com](http://google.com/), [naver.com](http://naver.com/) 과 같은 도메인 이름으로 요청을 보낸다.
2. DNS 서버에서는 해당 도메인에 해당하는 IP를 매칭해 응답한다.
3. 해당 IP로 접속한다.