# Section 4. HTTP 메서드

---

## ****요구사항 및 API URI 설계****

```jsx
회원 정보 관리 API 설계
1. 회원 목록 조회 :  /read-member-list
2. 회원 조회 :  /read-member-by-id
3. 회원 등록 : /create-member
4. 회원 수정 : /update-member
5. 회원 삭제 : /delete-member
```

요구사항 기반으로 API를 만들게 되는게 위와 같이 현업에서 잘못된 API URI 설계를 한다.

### ****API URI  설계 분리****

```jsx
리소스 : 회원
행위 : 조회, 등록, 수정, 삭제
```

API URI 설계를 할 때 리소스와 해당 리소스를 대상으로 하는 행위를 분리해야 한다. 회원이라는 리소스만 식별하고 회원 리소스를 URI에 매핑을 하면 된다.

### 리소스

동작을 제외한 자원 그 자체를 리소스라한다. 회원 등록 시스템을 예로 들면, 회원을 등록하거나 수정 혹은 삭제하는 행위는 리소스가 아니다.오직 회원이라는 개념만이 리소스라 할 수 있다.

### ****API URI 재설계****

```jsx
회원 정보 관리 API 재설계
1. 회원 목록 조회 :  /members
2. 회원 조회 :  /members/{id} 
3. 회원 등록 : /members/{id}
4. 회원 수정 : /members/{id}
5. 회원 삭제 : /members/{id}

계층 구조상 상위를 컬렉션으로 보고 복수 단어 사용 권장(member  ➡️  members)
```

API URI 재설계를 했지만 행위는 구분이 되지 않는다. 구분하는 방법은 URI 리소스만 식별해 놓으면 HTTP 메서드인 GET, POST, PUT, DELETE 이런 것들이 조회, 등록, 수정, 삭제 역할을 대신해준다.

---

# **HTTP 메서드 - GET, POST**

### **HTTP 메서드 종류**

- GET : 리소스를 조회
- POST : 요청 데이터를 담아서 처리
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성
- PATCH : 리소스 부분 변경
- DELETE : 리소스 삭제
- HEAD : GET과 동일하지만 메시지 부분을 제외하고 상태 줄과 헤더만 반환
- OPTIONS : 대상 리소스에 대한 통신 가능 옵션(메서드)를 설명 (주로 CORS에서 사용)
- TRACE : 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

### GET

리소스를 조회한다. 서버에 전달하고 싶은 데이터는 쿼리 파라미터 또는 쿼리 스트링을 통해서 전달한다. GET은 메시지 바디를 전달할 수 있지만 실무에서는 바디에 보통 데이터를 넣지 않는다. 지원하지 않는 서버들이 많아서 권장하지 않는다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/59101da7-bc7d-4f05-9baf-4bf0dad32789">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/cae430e3-d15b-4077-9627-caea2ed48c6c">

클라이언트가 /members/100 GET하고 요청하면 서버에서 GET 메시지가 도착한다. 서버에서는 /members/100 에서 데이터베이스를 조회해서 응답 메시지를 만들어서 클라이언트에게 보낸다.

### POST

클라이언트에서 메시지 바디를 통해서 서버로 요청해서 서버가 데이터를 처리하는 모든 기능을 수행한다. 주로 전달된 데이터로 신규 리소스 등록하거나 변경된 프로세스를 바꿀 때 많이 이용한다.


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/28936bb9-a348-4501-aa3b-735e55eef922">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/9f6bad9c-eaaf-4748-a0e7-7b733f6e21dd">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/a5f71ae0-2781-47a8-ae4a-e903ea27829c">
리소스를 /members POST로 전달하면 서버 입장에서는 그 데이터를 내부적으로 어떻게 쓸꺼야라고 미리 서로 약속을 해놓은다. 클라이언트는 필요한 데이터를 전달한다. 그러면 서버에서는 신규로 등록한다고 /members에서 100 신규 리소스 식별자를 생성한다. 신규로 자원이 생산 된 경로를 응답메시지로 보낸다.

### ****POST 정리****

- 메세지 바디를 통해 서버로 요청 데이터를 전달하면 해당 데이터를 처리한다.
- 주로 등록 혹은 프로세스 처리등에 사용된다.
1. 리소스 등록: 서버가 아직 식별하지 않은 새 리소스 생성(회원 등록)
2. 요청 데이터 처리: 단순한 데이터 생성을 넘어 프로세스를 처리해야 하는 경우로, 꼭 새로운 리소스가 생성되지 않을수도 있다.
 ⇒ POST /order/{orderId}/start-delivery (컨트롤 URI)
이처럼 경우에 따라 리소스단위가 아닌 행위가 포함된 URI 설계를 할 수도 있는데 이런 경우를       Control URI라 한다.
- 다른 메서드로 해결하기 어려운경우 POST를 사용하고는 한다.

---

## ****HTTP 메서드 - PUT, PATCH, DELETE****

### PUT- 리소스가 존재하는 경우


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/7ec18aa6-a2cf-49e9-96ef-9202407845da">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/11824137-61ff-4bf5-a474-a139c2b86a15">
클라이언트가 /members/100 리소스 지정해서 데이터를 서버에게 보냈는데, 만약 서버에 존재한다면, 클라이언트가 보낸 값으로 대체된다.

### PUT- 리소스가 존재하지 않을 경우


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/83460147-2700-4056-ba50-4ecbcb12c895">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/30a1d9b4-e121-4216-ac4f-2b64fd4f9dd3">
클라이언트가 members/100 리소스 지정해서 데이터를 서버에게 보냈는데 서버에서 해당 리소스가 없다면 신규 리소스로 생성이 된다.

### PUT 주의 사항 - 필드의 갯수가 다를때


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/25f56d1d-bf3e-480a-a3d7-cc8b5e4d8eca">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/1b4abc48-165b-45e2-888c-ae23f8449135">
클라이언트가 /members/100 데이터에 username이 없고 age로 지정해서 보내면 서버에서는 클라이언트로 부터 들어온 값으로 대체하기 때문에 username의 필드가 사라지게된다.

### PATCH

PATCH는 클라이언트가 원하는 값만 바꿀수 있다.


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/7c057462-638f-49ab-a799-3a20bc5c66fa">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/3815cf21-2e9c-4fdf-9797-dbfab07b8a8a">
### DELETE


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/f787b035-00b3-4260-bd92-7f27aad8f213">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/4b4eccd9-614a-41ae-a112-095f9a712e53">
리소스를 삭제한다. 클라이언트가 /members/100 를 삭제해달라고 요청하면 서버에서 리소스를 삭제한다.

---

## ****HTTP 메서드의 속성****


<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/5d94d3d1-99eb-4f78-a69f-2f9b3a724393">
### **안전(Safe Methods)**

호출해도 리소스가 변경하지 않는다.

- GET은 단순히 조회만 하기 때문에 안전하다. 한번 호출해도 여러번 호출해도 변경이 일어나지 않아서 안전하다.
- POST, PUT, PATCH, DELETE는 안전하지 않다.
- 만약에 그래도 계속 호출해서 서버에서 로그가 계속 쌓게되서 서버 장애가 일어날 때는 안전은 그런 부분까지 고려하지 않는다. 안전은 해당 리소스만 고려하기 때문이다.

### **멱등(Idempotent Methods)**

한 번 호출해도 두 번 호출해도 100번 호출해도 결과는 동일하다.

- GET은 한 번 조회하든 두 번 조회하든 같은 결과로 조회된다.
- PUT은 결과를 대체하기 때문에 같은 요청을 여러 번 해도 최종 결과는 동일하다.
- DELETE는 결과를 삭제하기 때문에 같은 요청을 여러 번 해도 삭제된 결과는 동일하다.
- PUT은 멱등이 아니다. 두 번 호출하면 같은 결제가 중복해서 발생해서 새로운 리소스로 구별이 된다.

```jsx
사용자 1 : GET ➡️ username: A, age: 20
사용자 2 : PUT ➡️ username: A, age: 30
사용자 3 : GET ➡️ username: A, age: 30
```

멱등은 외부 요인으로 중간에 리소스가 변경되는 것까지 고려하지 않는다. 클라이언트가 동일한 요청을 똑같은 클라이언트가 동일한 요청했을 때만 멱등한다. 즉 멱등은 동시성 문제까지 고려하지 않는다.

### **멱등의 활용**

자동 복구 매커니즘로 활용할 수 있다. 클라이언트가 자동 DELETE를 호출했는데 서버에서 잘 되고 있는지 안 되고 있는지 응답이 없다. 클라이언트가 다시 자동 DELETE를 재시도 해도 멱등한다. 실무에서 이런 전반적으로 자동 복구 매커니즘을 많이 사용한다.

### **캐시가능(Cacheable Methods)**

웹 브라우저에 용량이 큰 이미지를 한번 요청을 하면 그 다음에 똑같이 용량이 큰 이미지를 요청할 필요없다. 똑같은 이미지를 서버에서 다운로드 받으면 오래 걸린다. 그래서 로컬 PC에 웹 브라우저 저장을 하고 있을 때 캐시라고 한다. 캐시는 GET, HEAD, POST, PATCH 가능 하지만 실제로는 GET, HEAD 정도만 캐시로 사용한다. POST, PATCH는 캐시를 하려면 본문 내용으로 리소스랑 캐시 키가 맞아아야 되는데 복잡해서 구현이 쉽지 않다. GET, HEAD는 URI만 캐시 키로 캐시해서 간단하다.