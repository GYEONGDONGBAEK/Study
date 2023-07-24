# Section 7-(1). HTTP 헤더1 - 일반 헤더

---

## ****HTTP 헤더****

HTTP 전송에 필요한 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 등 모든 부가 정보를 헤더에 넣는다. 표준 헤더가 굉장히 많다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/b9497132-6faa-478b-8384-69343b053666">

### ****HTTP 헤더  - RFC2616****

<img src="(https://github.com/GYEONGDONGBAEK/study/assets/122242439/024bc18d-edbb-4900-8c21-022767ce1141">

**헤더 분류**

- General 헤더 : 요청 메시지든 응답 메시시든 구분없이 메시지 전체에 적용되는 정보이다.

```java
Connection: close
```

- Request 헤더 : 요청 정보

```java
User-Agent: Mozilla/5.0 (Macintosh;..)
```

- Reponse 헤더 : 응답 정보

```java
Server: Apache
```

- Entity 헤더 : Entity 바디 정보

```java
Content-Type: text/html, Content-Lenth: 3423
```

### **HTTP BODY - RFC2616**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/7a9f3b16-33dc-4cd8-9425-56c8fcf35bbb">

메시지 본문은 엔티티 본문의 요청이나 응답에서 실제 데이터를 전달 하는데 사용한다. 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 데이터 유형, 데이터 길이, 압축 정보 등을 제공한다.

---

# **2. 표현**

### **HTTP 표준 - RFC723X 변화**

엔티티를 표현으로 바뀌게 된다. 메타 데이터와 표현 데이터를 합쳐서 표현이라고 한다.

### **HTTP BODY - RFC7230**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/d7989372-3495-40c9-ac9b-9b261bd55c85">

메시지 본문을 통해 요청이나 응답에서 전달할 실제 데이터를 표현 데이터 전달 하는데 사용한다. 메시지 본문을 페이로드라고 부른다.

### **Content-Type**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/398589b2-f557-4dbf-9c22-b3a7fb6522a8">

클라이언트랑 서버 간에 실제 주고 받을 때 이해할 수 있는 뭔가를 변환해서 데이터 전달해야 된다. 이때 헤더에다가 Content-Type을 사용한다.

```java
text/html; charset=utf-8
application/json
image/png
```

### **Content-Encoding**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/e0252609-34ff-4660-9456-d0df39f07a29">

표현 데이터를 압축하기 위해 사용한다. 서버에서 클라이언트를 보낼 때 Content-Encoding 부가 정보를 보내줘야 무엇으로 압축되는지 알 수 있다. 데이터 전달하는 곳에서 압축 후 인코딩 추가하고 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축해제한다.

```java
gzip: 압축해서 보낸다
deflate: 압축해서 보낸다
identity: 압축하지 않고 그대로 보낸다
```

### ****Content-Language****

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/4453c000-eb7e-46dd-aba9-a68b29a5f5b8">

표현 데이터의 자연 언어를 표현한다.

```java
ko, en, en-US
```

### Content-Length

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/a10122ef-f976-4c93-8758-ab6dfa64df31">

표현 데이터의 길이다. Transfer-Encoding을 사용하면 Content-Lenght를 사용하면 안된다.

---

# **3. 콘텐츠 협상**

### **협상**

클라이언트가 원하는 표현을 달라고 서버한테 요청을 하면 서버거 클라이언트가 원하는 우선순위에 맞춰서 표현 데이틑 만들어서 보낸다.

- Accept : 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset : 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
- Accept-Language : 클라이언트가 선호하는 자연 언어
- 협상 헤더는 요청시에만 사용한다.

### **Accept-Language 적용 전**


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/192286db-7016-47de-9739-1c1ea7de190a">

한국어 브라우저를 사용하고 다중 언어 지원하는 서버를 사용한다고 가정하에 한국어 브라우저는 외국 사이트를 /event로 들어가면, 다중 언어 지원 서버는 내부적으로 우선순위가 높은 영어를 보낸다. 클라이언트에서 서버로 요청을 보낼 때 서버는 클라이언트의 언어가 한국어인지 영어인지에 대한 아무런 정보가 없다. 그러면 서버는 우선순위가 높은 영어를 응답한다.

### **Accept-Language 적용 후**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/63fdc50a-0fb1-44b0-897d-8ee1b467e7cb">

클라이언트가 선호하는 언어를 한국어 정보를 입력해서 서버에게 전달한다. 서버는 기본언어가 영어지만 한국어도 지원하기 때문에 클라이언트가 원하는 한국어로 넣어서 데이터를 전달한다.

### **Accept-Language 복잡한 예시**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/5125b313-3346-4b1b-a27c-37b452b6ba70">

클라이언트가 선호하는 언어를 한국어 정보를 입력해서 서버에게 전달하는데 서버가 기본이 독일어인데 영어를 지원한다. 다중 언어 지원 서버가 한국어 지원을 하지 않아서 독일어로 보내게 된다.

### **협상과 우선순위 1**

Quality Values(q) 값으로 사용한다. 0~1로 값이 클수록 우선순위가 높고 1은 생략이 가능하다.

```java
GET /event
ko-KR
ko;q=0.9
en-US;q=0.8
en;q=0.7
```

1. **ko-KR**
2. **ko;q=0.9**
3. **en-US;q=0.8**
4. **en;q=0.7**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/012c0ab1-b47b-4668-abd7-8e7be9f0c485">

클라이언트의 브라우저에서 한국어를 선호하지만 다중 언어 지원서버로 기본이 독일어고 영어를 지원한다. 서버에서는 독일어보다는 영어를 선호한다는 거를 알고 영어로 보내게 된다.

### **협상과 우선순위 2**

구체적일 수록 우선순위가 높다.

```java
GET /event
Accept: text/*, text/plain, text/plain;format=flowed, */*
```

1. **text/plain;format=flowed**
2. **text/plain**
3. **text/***
4. **/***

### **협상과 우선순위 3**

구체적인 것을 기준으로 미디어 타입과 매칭하면 된다.

| Media Type | Quality |
| --- | --- |
| text/html;level=1 | 1 |
| text/html | 0.7 |
| text/plain | 0.3 |
| image/jpeg | 0.5 |
| text/html;level=2 | 0.4 |
| text/html;level=3 | 0.7 |

```java
GET /event
Accept: text/*;q=0.3, 
				text/html;q=0.7, 
				text/html;level=1, 
				text/html;level=2;q=0.4, 
				*/*;q=0.5
```

text/* 이 0.3인 이유는 text/html , text/html;level 등 구체적인 값이 먼저 매칭되고 난 후 매칭되기 때문이다. text/* 이 */* 보다 구체적이기 때문에 먼저 text/ 의 값과 매칭이 된다.

# **4. 전송 방식**

### **단순 전송 (Content-Length)**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/e1793c07-f78e-44c7-8ff7-9458a533c602">

Content의 길이를 지정을 해서 한 번에 요청을 하고 응답을 한다.

### **압축 전송 (Content-Encoding)**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/25e56cf4-bb85-4a93-86d4-32c854e2c1f1">

Content를 압축할 때 무엇을 압축되어 있는지 알아야 클라이언트에서 알고 압축을 풀 수 있다.

### **분할 전송 (Transfer-Encoding)**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/0305a3f0-728c-4db7-8822-73edd9f7f9c0">

chunked는 덩어리라는 뜻이다. 덩어리로 쪼개서 전송을 한다. 5byte로 Hello를 서버에서 클라이언트로 보낸다. 또 5byte로 World를 보내고 마지막으로 0byte로 src를 보내면 끝이라는 걸 표현한다. 

이미 chunked 된 메세지에 Content-Length의 값이 들어있고, 서버가 Content-Length의 정확한 값을 모르기 때문에, 분할 전송할 때는 Content-Length를 넣으면 안된다.

### **범위 전송 (Content-Range)**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/bacaab7a-8092-4cf1-924f-609e4cb54744">

이미지를 받다가, 중간에 끊길 경우 못 받은 범위를 지정해서 다시 요청을 한다.

---

# **5. 일반 정보**

### **From**

유저 에이전트의 이메일 정보이다. 일반적으로 잘 사용하지 않는다. 

### **Referer**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/3f28f032-25df-4c12-88d5-495950372db3">

현재 요청된 페이지의 이전 웹 페이지 주소이다. A에서 B로 이동하는 경우 B를 요청할 때 Referer A를 포함해서 요청한다. Referer를 사용해서 데이터 분석 할 때 유입 경로 분석을 가능하다.

### **User-Agent**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/41957f1f-8baf-432a-b1d9-541e25f40158">

클라이언트의 애플리케이션 정보이다. 사용자들이 어떤 종류의 브라우저에서 장애가 발생하는지 파악이 가능하다.

### **Server**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/9cf78e80-111d-4114-9bb1-d467bd8a45ff">

요청을 처리하는 ORIGIN 서버의 소프트웨어 정보이다. ORIGIN 서버는 실제 HTTP 응답을 해주는 서버이다.

### **Date**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/e12ccb85-5fba-4db6-9d4a-a61739e92972">

메시지가 발생한 날짜와 시간이다. 응답에서만 사용한다.

---

# **6. 특별한 정보**

### **Host**

요청에서 사용하고 필수값이다. 하나의 서버가 여러 도메인을 처리해야 할 때, 하나의 IP 주소에 여러 도메인이 적용되어 있을 때 구분해줘야 한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/610704fd-ae9c-40ef-b2ae-8642439194c3">

가상호스트를 통해서 하나의 서버가 지금 IP : 200.200.200.2 가 있고 서버 안에 여러 개의 애플리케이션이 다른 도메인으로 구동되어 있다. 클라이언트가 /hello 로 GET 방식으로 요청을 했는데 서버 입장에서는 /hello 와 관련된 애플리케이션에 어디로 들어갈지 모른다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/648cc51c-4ca7-4f1b-9067-36dd81639e36">

Host 헤더로 입력하면 서버에서 요청에 맞는 도메인주소를 응답한다.

### **Location**

```java
201(Created) : Location 값은 요청에 의해 생성된 리소스 URI이다.
3xx(Redirection) : 응답의 결과에 Location 헤더가 있으면 Location 위치로 자동 리다이렉트로 한다.
```

### **Allow**

허용 가능한 HTTP 메서드이다.

```java
405(Method Not Allowed) : 오류를 내면서 응답에 포함한다.
```

GET, HEAD, PUT만 지원을 한다. 서버에서 많이 구현되지는 않는다.

### **Retry-After**

유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간이다.

```java
503(Service Unavaliable) : 서비스가 언제까지 불능인지 알려준다.
```

---

# **7. 인증**

### **Authorization**

클라이언트 인증 정보를 서버에 전달할 수 있다. 어떤 인증 메커니즘인지 상관없이 인증과 관련된 값을 헤더로 제공한다.

### **WWW-Authenticate**

리소스 접근 시 필요한 인증 방법 정의한다.

```java
401(Unauthorize) : 응답과 함께 사용한다.
WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps"\"", Basic realm="simple"
```