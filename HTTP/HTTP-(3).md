# Section 3. HTTP 기본



# **모든 것이 HTTP**

### **HTTP(HyperText Transfer Protocol)**

문서 간의 링크를 통해서 하이퍼텍스트 문서를 통해서 연결하는 프로토콜이다. HTTP 프토토콜에 HTML, TEXT, IMAGE, 음성, 영상, 파일, JSON, XML (API) 등 모든 형태의 데이터를 담아서 전송이 가능하다. 심지어 서버간에 데이터를 주고 받을 때도 사용한다.

### **HTTP 역사**

1. HTTP/0.9 (1991년) : GET 메서드만 지원, HTTP 헤더X

2. HTTP/1.0 (1996년) : 메서드, 헤더 추가

3. HTTP/1.1 (1997년) : 가장 많이 사용하고 우리에게 가장 중요한 버전이다.

- RFC2068 (1997년) ➡️ RFC2616 (1999년) ➡️ RFC7230~7235 (2014년)

4. HTTP/2 (2015년) : 성능 개선

5. HTTP/3 (진행중) : TCP 대신에 UDP 사용, 성능 개선

### **HTTP 기반 프로토콜**

HTTP/1.1, HTTP/2 같은 경우에는 TCP 프로토콜 위에서 동작을 한다. HTTP/3은 UDP 프로토콜 기반으로 개발이 되어 있다. TCP는 3 way handshake도 해야 되고 기본적으로 데이터도 많고 매커니즘 자체가 속도가 느린 편이다. 그래서 UDP 프로토콜 위에 애플리케이션 단계에서 성능을 최적화하도록 새로 설계한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/e0c31c17-d48e-42cd-9985-618ad662fdb0">

개발자 도구 → 네트워크 → 프로토콜에서 무슨 프로토콜이 쓰이는지 확인할 수 있다.

### **HTTP 특징**

HTTP 프로토콜은 기본적으로 클라이언트 서버 구조로 동작한다. 무상태 프로토콜(Stateless)이고 비연결성이라는 특징이 있다. HTTP 메시지를 통해서 통신을 하고 단순하고 확장 가능하다.

---

# **클라이언트 서버 구조**

### **Request Response 구조**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/bd2c2d80-66e2-4990-aeb0-9efffbaaf9ef">

HTTP는 클라이언트가 HTTP 메시지를 통해서 서버에 요청을 보내고 클라이언트는 서버에 응답이 올 때 기다린다. 서버가 요청에 대한 결과를 만들어서 응답이 오면 그 응답 결과를 열어서 클라이언트가 동작한다.

### **역할**

원래는 클라이언트와 서버가 하나로 되었다가 개념적으로 분리가 되면서 클라이언트는 UI, 사용성에 집중하고 서버는 비즈니스 로직이랑 데이터에 집중한다. 이슈가 발생해도 서로의 역할이 달라 이슈에 대한 영향을 미치지 않고 독립적으로 이슈를 대응하면서 진화할 수 있다.

---

# **Stateful, Stateless**

### **상태 유지 (Stateful)**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/16d96d4f-0b7e-407d-858d-1b99fb718ab6">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/5047e35a-8f3a-4d02-8ad6-3f96395fa40a">

서버가 클라이언트의 상태를 보존한다. 클라이언트가 상품을 구입할 때 상품 정보와 결제 정보를 매칭된 서버로 계속 유지해야 되서 서버를 늘릴 수가 없다. 중간에 유지해야할 서버가 장애가 발생하면 다른 서버로 바뀌게 되면 클라이언트가 다시 정보를 요청을 해야 된다.

### ****무상태 (Stateless)****

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/237aa870-2437-4283-a194-1b585a72f744">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/a491e034-3db8-428b-a246-814d5f0c3cef">

서버가 클라이언트의 상태를 보존하지 않는다. 클라이언트가 상품을 구입할 때 애초에 필요한 상품 정보와 결제 정보를 담아서 요청을 하면 서버에서는 상태를 보존하지 않고 응답만 한다. 중간에 서버가 장애가 발생해도 클라이언트가 필요한 정보들을 이미 담아 있어서 다른 서버에 요청 할 수 있다.

### 무상태 스케일 아웃

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/7410c205-288d-4feb-8175-0f24390056b0">

이벤트 기간이거나 갑자기 트래픽이 증가할때에 상태를 유지하지 않으면 무한한 확장성을 가지고 있기 때문에 서버를 무한정으로 늘릴 수 있다.

### **상태 유지와 무상태의 한계**

**상태 유지의 한계**

- 로그인 해야 되는 경우는 로그인한 사용자가 로그인했다는 상태를 서버에 유지해야 한다.
- 브라우저에서 쿠키와 서버의 세션을 같이 조합해서 상태를 유지하는 기능을 쓴다. 서버에 세션이 날아가거나 세션 서버가 죽어버리면 전체적으로 로그인이 풀려버리게 된다.
- 상태유지는 최소한으로만 사용한다.

**무상태의 한계**

- 로그인할 필요 없는 단순한 소개 페이지일 때는 상태를 유지할 필요가 없어서 설계하기가 쉽다.
- 클라이언트가 전송할 때 필요한 정보를 담아야 되서 데이터량이 많다.

---

## ****비 연결성(connectionless)****

클라이언트와 서버가 요청(Request)시에만 연결이되며 그 외에는 연결을 유지하지 않고, 않아야 한다.  계속 연결을 유지하는것도 결국 비용이고 연결을 최소한으로 함으로써 비용을 절약한다.

### 단점

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/76648ec3-ab92-42f2-9583-352464513a17">

- 매번 새로 연결해야한다는 부분은 매 연결에 들어가는 비용이 문제가 될 수 있다.
- **TCP/IP**는 매번 연결 시 3-Way Handshake 시간이 추가된다.

### 단점 보완 **- HTTP 지속 연결(Persistent Connections)**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/3a8f8c6c-d2ba-4b07-89d0-3f4baf69e218">

- 클라이언트와 서버가 연결을 한 뒤 필요한 자원을 요청/응답으로 다운받는다.
- 각각의 자원이 별도의 연결/종료가 되는 것이 아니라 한 연결에 필요 정보를 모두 다운받은 뒤 종료된다. 그럼으로써 연결/종료에 걸리는 시간을 단축할 수 있다.

---

# **HTTP 메시지**

## **HTTP 메시지 구조**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/e016eb53-bd92-4150-a19c-cbe2cd55aaea">

HTTP 메시지 구조에서 start-line, header, empty line(CRLF), message body로 4가지 구조로 나눈다.

## ****HTTP 요청 메시지****

### **start-line : request-line**

```jsx
GET /search?q=hello&hl=ko HTTP/1.1
method SP request-target SP HTTP-version CRLF
Host: www.google.com
field-name ":" OWS field-value OWS
```

### **method (메서드)**

HTTP method의 종류가 GET, POST, PUT, DELETE 등이 있고 서버가 수행해야 할 동작을 지정한다.

- GET : 서버에게 리소스 조회
- POST : 서버가 리소스를 요청 내역 처리

### **request-target (요청 대상)**

```jsx
/absolute-pate[?query]
/절대경로[?쿼리]
```

- 보통 절대경로로 ' / '로 시작하고 쿼리를 합친다.
- http://...?x=y 같이 다른 유형의 경로지정 방법도 있다.

### **HTTP-version (HTTP 버전)**

---

## HTTP 응답 메시지

### **start-line : status-line**

```jsx
HTTP/1.1 200 OK
HTTP-version SP status-code SP reason-phrase CRLF
```

**HTTP-version (HTTP 버전)**

**status-code (HTTP 상태 코드)**

클라이언트가 보낸 요청이 성공했는지 실패했는지 나타내는 상태이다.

- 200 : 성공
- 400 : 클라이언트 요청 오류
- 500 : 서버 내부 오류

### **reason-phrase (이유 문구)**

- 사람이 이해할 수 있는 짧은 상태 코드를 읽을 수 있는 글이다.

### header

```jsx
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
field-name ":" OWS field-value OWS
```

HTTP 헤더의 용도는 HTTP 전송에 필요한 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정도 등 모든 부가 정보가 들어가 있다. 표준 헤더가 많다. 필요하면 임의의 헤더도 추가 가능할 수 있다.

### f**ield-name, field-value**

field-name ":" OWS field-value OWS

name 은 대소문자 구별이 없으나, value는 대소문자 구별 해야한다.

OWS 는 띄워쓰기를 나타낸다.

### body

```jsx
<html>
    <body> ... </body>
</html>
```

실제 전송할 데이터가 담아있다. HTML 문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송이 가능하다.