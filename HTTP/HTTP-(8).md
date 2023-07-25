# Section 7-(2). HTTP 헤더 - 쿠키

---

# **8. 쿠키**

### **Set-Cookie**

서버에서 클라이언트로 쿠키를 전달(응답)한다.

### **Cookie**

클라이언트가 서버에서 받은 쿠키를 저장하고 HTTP 요청시 서버로 전달한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/0af9439e-5baf-49f1-a220-a9f8ddc4421f">

웹 브라우저에서 로그인 하지않은 사용자가 /welcome 으로 웹 페이지로 접근하면 서버에서는 손님으로 들어오게 된다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/efb073fb-447d-4092-a7cf-4982ace11e11">

/login으로 유저 정보, 패스워드 등을 POST방식으로 보내서 로그인을 하면 서버에서는 홍길동으로 로그인했다고 응답을 준다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/f1b31727-c3b7-453e-b974-a3e68b81cb50">

이 상태에서 다시 /welcome으로 접근하면 서버입장에서 로그인한 사용자인지 아닌지 구분할 방법이 없다. 이러한 이유는 HTTP가 무상태 프로토콜이기 때문이다.  기본적으로 클라이언트와 서버가 요청과 응답을 주고 받으면, 연결이 끊어진다. 클라이언트가 서버에 다시 요청한다 하더라도, 클라이언트와 서버는 서로 상태를 유지하지 않기 때문에, 서버는 이전 요청을 기억하지 못한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/74272bf5-22bc-4eb8-ba95-dc3c0c05a81f">

대안으로는 모든 요청에 사용자 정보를 포함해서 보내면 된다. 사용자 정보를 계속 서버에 주면 서버는 홍길동으로 응답해준다. 문제점은 모든 요청과 링크의 사용자 정보를 다 포함하면 보안의 문제, 개발하기 힘들다는 문제가 있다.  ⇒ 쿠키로 보완

### **Cookie**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/458ba622-1ed9-49aa-8c2c-81b169c73c57">

웹 브라우저가 POST로 로그인을 하면 서버에서는 Set-Cookie로 홍길동 정보를 만들어서 응답을 한다. 웹 브라우저 내부에는 쿠키 저장소가 있는데 서버가 응답에서 만든 Set-Cookie로 key는 user, value는 홍길동이라고 쿠키 저장소에 저장을 한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/ec2b4e30-48d1-4d0e-9f5b-2c16d74cf0e7">

로그인 이후에 웹 브라우저가 /welcome에 들어오면 자동으로 웹 브라우저는 서버에 요청을 보낼 때 마다 쿠키 저장소에서 조회를 해서 홍길동이라는 HTTP 헤더를 만들어서 서버에 보낸다. 서버는 쿠키를 인식해 홍길동이라는 걸 인지하기 때문에, URL이나 파라미터를 넣어서 요청 필요가 없다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/1c321414-39e1-4081-9fd9-2f05426f3145">

지정한 서버에 쿠키는 모든 요청 정보에 쿠키 정보를 자동으로 포함을 한다.

### **쿠키**

```java
set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
```

- 사용처

   ⇒사용자 로그인 세션 관리

   ⇒광고 정보 트래킹

- 쿠키 정보는 항상 서버에 전송

   ⇒ 네트워크 트래픽 추가 유발하기 때문 최소한의 정보만 사용 : 세션 Id, 인증 토큰

- 주의사항 : 보안에 민감한 데이터는 쿠키에 저장하면 안된다.

### 쿠키 - 생명주기

Set-Cookie:**expires , max-age**

- **expires** : 쿠키를 무제한으로 보관할 수 없다. GMT기준으로 만료일이 되면 쿠키를 자동으로 삭제한다.
- **max-age** : 초 단위로 구성되어 있고 0이나 음수를 지정하면 쿠키가 삭제한다.
- 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

### 쿠키- 도메인

명시: 명시한 문서 기준 도메인 + 서브 도메인 포함

- domain=example.org를 지정해서 쿠키 생성
• example.org는 물론이고
• dev.example.org도 쿠키 접근

생략: 현재 문서 기준 도메인만 적용
      • example.org 에서 쿠키를 생성하고 domain 지정을 생략
      • example.org 에서만 쿠키 접근
      • dev.example.org는 쿠키 미접근

### **쿠키 - 경로**

경로를 포함한 하위 경로 페이지만 쿠키를 접근 할 수 있다. 일반적으로 path=/ 루트로 지정한다.

**path=/home 지정**

/home  ➡️ **가능**

/home/level1  ➡️ **가능**

/home/level1/level2  ➡️ **가능**

/hello  ➡️ **불가능**

### ****쿠키 - 보안****

**Secure** : 쿠키는 원래 http, https를 구분하지 않고 전송을 한다. Secure를 넣으면 https인 경우에만 클라이언트에서 서버로 key를 전송한다.

**HttpOnly** : XXS 공격을 방지할 수 있다. 자바스크립트에서 접근할 수 없다. 대신에 http 전송에서만 사용할 수 있다.

**SameSite** : XSRF 공격을 방지할 수 있다. 요청하는 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키를 전송할 수 있다.