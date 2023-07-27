# Section 8-2. HTTP 헤더2 - 캐시와 조건부 요청-(2)

---

### **검증 헤더와 조건부 요청 2**

**검증 헤더와 조건부 요청이란**

- **검증 헤더**
    - 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
    - Last-Modified, ETag
    - 크게 두 가지가 있다.
- **조건부 요청 헤더**
    - 검증 헤더로 조건에 따른 분기시 사용
    - If-Modified-Since: Last-Modified를 사용
    - If-None-Match: ETag 사용
    - 조건이 만족하면 200 OK
    - 조건이 만족하지 않으면, 304 Not Modified

예를 들어) **If-Modified-Since: 이후에 데이터가 수정되었으면?**

- **데이터 미변경 예시**
    - 캐시: 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 10:00:00
    - 304 Not Modified, 헤더 데이터만 전송한다. (body X)
    - 따라서 전송 용량 0.1MB (헤더 0.1MB)
- **데이터 변경 예시**
    - 캐시: 2020년 11월 10일 10:00:00 vs 서버: 2020년 11월 10일 11:00:00
    - 200 OK, 모든 데이터 전송 (body o)
    - 따라서 전송 용량 1.1MB (헤더 0.1MB, 바디 1MB)

### **Last-Modified, If-Modified-Since의 단점**

- 1초 미만(0.x초) 단위로 캐시 조정이 불가능하다. (최근 갱신 일자의 단위가 초까지임)
- 날짜 기반의 로직을 사용해야 한다
- 데이터를 수정해서 날짜가 달라졌지만, 실질적으로 같은 데이터를 수정해 결과가 똑같은 경우
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
    - 예) 스페이스나 주석처럼 크게 영향이 없는 변경에서 캐시를 유지하고 싶은 경우

이런 경우를 다룰 수 있는 방법이 있다.

### **ETag, If-None-Match**

- ETag (Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아두는 구조
    - 예) ETag: "v1.0", ETag: "a2jiodwjekjl3" => 버전으로 달 수도 있고, Hash 값으로 할 수도 있다.
- **데이터가 변경**되면, 이 **이름을 바꾸는 것**을 포함해 변경한다. (Hash를 다시 생성한다)
    - 예) ETag: "aaaaa" -> ETag: "bbbbb"
- 진짜 단순하게 **ETag만 보내서 같으면 유지**하고, **다르면 다시 받는다!!**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/c2eddc8b-16a5-400f-8a51-629152d9910b">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/27ba02f9-f0d0-462d-8d38-845ced544870">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/f4ded473-4789-4032-aacf-9e97a529f133">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/125567c2-5919-4d5b-bf37-82ab14791b88">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/b0a6175d-5c96-4667-897d-a7d2794ba414">

### **ETag, If-None-Match 정리**

- 진짜 단순하게 ETag만 서버에 보내서 같으면 유지하고, 다르면 다시 받기!
- **캐시 제어 로직을 서버에서 완전하게 관리한다.**
- 클라이언트는 단순히 이 값을 서버에 제공(클라이언트는 캐시 메커니즘을 모름)
- 예시)
    - 서버는 배타 오픈 기간인 3일 동안 파일이 변경되어도, ETag를 동일하게 유지한다.
    - 애플리케이션 배포 주기에 맞춰 ETag를 모두 갱신
- 이렇게 ETag와 If-None-Match를 사용할시, 클라이언트의 입장에서는 캐시 메커니즘이 완전히 블랙박스가 되어버린다.

---

### **캐시와 조건부 요청 헤더**

캐시의 **제어와 관련된 헤더**들이 있다.

- Cache-Control: 캐시 제어
- Pragma: 캐시 제어(하위 호환)
- Expires: 캐시 유효 기간(하위 호환)

하나씩 정리해 보자.

### **Cache-Control - 캐시 지시어(directives)**

- **Cache-Control: max-age**
    - 캐시 유효 시간, 초 단위로 작성한다.
- **Cache-Control: no-cache**
    - 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용한다.(로컬 캐시에 있는 정보가 바뀌었는지 여부를 항상 서버에 검증을 받고 사용해라)
- **Cache-Control: no-store**
    - 데이터에 민감한 정보가 있으므로 저장하면 안된다.(메모리에서 사용하고 최대한 빨리 삭제한다.)

### **Pragma - 캐시 제어(하위 호환)**

- Pragma: no-cache
- HTTP 1.0 하위 호환이라고 한다.
- 지금은 사용 X

### **Expires - 캐시 만료일 지정(하위 호환)**

- expires: Mon, 01 Jan 1990 00:00:00 GMT
- 캐시 만료일을 정확한 날짜로 지정할 수 있다.
- HTTP 1.0부터 사용됨
- 지금은 더 유연한 Cache-Control: max-age를 권장
- 지금 버전에서 Cache-Control: max-age와 **함께** 사용하면 **Expires는 무시**된다.

검증 헤더와 조건부 요청 헤더

- 검증 헤더 (Validator)
    - **ETag**: "v1.0", ETag: "asdfkas;l09"
    - **Last-Modified**: Thu, 04 Jum 2020 07:19:24 GMT
- 조건부 요청 헤더 (특정 헤더의 값을 기반으로 조건에 따른 분기를 원할 때 사용)
    - **If-Match**, **If-None-Match**: ETag 값을 사용한다.
    - **If-Modified-Since**, **If-Unmodified-Since**: Last-Modfied 값을 사용한다.

## 프록시 캐시 (Proxy Cache)

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/48a59c08-5519-46fc-9511-51a8fc50f15d">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/c9455841-1618-4753-88dc-4a7d63481e9f">

proxy cache라는 서버를 도입해서 브라우저(클라이언트의)가 원(origin) 서버가 아닌 proxy cache 서버를 거쳐오도록 만든다.

이 프록시 캐시 서버는 미국에 있는 원서버에 비해 한국에 있을 것이기 때문에, 응답 속도가 훨씬 빠를 것이다. 기존에 0.5초 걸리던 것이 0.1초면 되는 구조다.

유튜브 같은 것들도 사람들이 안 보는 콘텐츠를 틀면 오래 걸리고, 사람들이 많이 보는 컨텐츠가 빨리 뜨는 것은 이러한 프록시 캐시 서버의 영향이다.

현재는 대부분 이러한 cdn 서비스를 이용한다고 한다.

**private cache: 내 로컬 환경이나 브라우저에 저장되는 캐시**

**public cache: 여러 유저가 공용해서 사용하는 캐시**

### **Cache-Control - 캐시 지시어 (기타)**

- **Cache-Control: public**
    - 응답이 public 캐시에 저장되어도 된다.
- **Cache-Control: private**
    - 응답이 해당 사용자만을 위한 것임, private cache에 저장되어야 하는 데이터 (기본값이다.)
- Cache-Control: s-maxage
    - 프록시 캐시에만 적용되는 max-age를 줄 수 있다.
- Age: 60 (HTTP 헤더)
    - 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간 (초 단위)을 받을 수 있다.

---

### **캐시 무효화**

### **Cache-Control - 확실한 캐시 무효화 응답**

캐시를 사용하지 않아도, 브라우저가 알아서 사용자에 맞게 캐싱하는 경우가 있어 캐시로 사용하지 않기 위해서는 아래의 설정들을 모두 해줘야 한다.

- **Cache-Control: no-cache, no-store, must-revalidate**
- **Progma: no-cache**
    - HTTP 1.0 하위호환이지만, 과거 서비스들에도 대비해야

**통장 잔고** 같이 **계속해서 변화하는 내용**들을 확실하게 **caching 하면 안 된다.**

캐시 지시어 - 확실한 캐시 무효화

- **Cache-Control: no-cache**
    - 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!)
- **Cache-Control: no-store**
    - 데이터에 민감한 정보가 있으므로 저장하면 안 됨 (메모리에서 사용하고 최대한 빨리 삭제)
- **Cache-Control: must-revalidate**
    - 캐시 만료 후 **최초 조회 시** **원 서버에 검증해야 함**
    - 원 서버 접근 실패 시 반드시 오류가 발생해야 함 - 504(Gateway Timeout)
    - must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
- **Pragma: no-cache**
    - HTTP 1.0 하위 호환

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/09107aad-1b62-4fdd-a2a0-cc559d8e4f71">

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/4387556c-4abb-47b2-b1ae-3ae519b4d9e2">

no-cache는 cache 서버에 데이터가 있는 경우 가져다 쓰거나, 혹은 원 서버 검증 과정에서 네트워크 단절같은 오류로 원 서버에 접근이 불가능한 경우에 오류를 발생시키기 보다는 오래된 데이터라도 전송하는 식으로 동작한다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/aa4cfbdd-da88-44f9-aa8d-db1d02f984d5">

그에 반해서, must-revalidate는 원 서버에 접근할 수 없는 경우 무조건 504 Gateway Timeout 오류를 발생시킨다.

계좌 잔고 같이 매우 중요한 정보와 관련해서는 잘못된 정보를 제공하는 경우가 더 큰 문제가 될 수 있기 때문에 이러한 경우에 must-revalidate가 사용된다고 한다.