# 참고하면 좋은 URI 설계 개념

---

# 명사 네이밍

- RESTful URI 는 리소스를 다루는 작업, 행동이 아니라 리소스의 이름, 명사를 참조하도록 한다. 왜냐하면 명사는 동사는 가지지 못하는 속성, 영역이 있기 때문이다. 예를 들어 시스템의 유저, 유저의 정보 등과 같이 계층을 가지고 다른 리소스를 포함할 수 있다.
- 이러한 리소스의 타입을 더 명확하게 하기 위해서, document, collection, store 그리고 controller 의 4가지 타입으로 구분할 수 있다.

## document

```jsx
 http://api.example.com/device-management/managed-devices/{device-id}
 http://api.example.com/user-management/users/{id}
 http://api.example.com/user-management/users/admin
```

- document 리소스는 객체 인스턴스나 데이터베이스 데이터와 같은 유일 개념이다.
- REST 방식에서 리소스의 컬렉션 내부의 하나의 리소스로 생각하면 된다. document 의 상태 표현은 일반적으로 값과 다른 연관된 리소스로의 링크를 모두 포함하고 있다.
- document 리소스를 표현하기 위해서는 단수 표현으로 이름을 정한다.

## collection

```jsx
http://api.example.com/device-management/managed-devices
http://api.example.com/user-management/users
http://api.example.com/user-management/users/{id}/accounts
```

- collection 리소스는 리소스들의 server-managed directory 이다.
- 클라이언트가 리소스들을 컬렉션에 추가하기를 요청할 수 있다. 이때 새로운 리소스를 생성할지 아닌지는 collection 리소스에게 달려있다.
- collection 리소스는 포함할 리소스를 선택하고 포함된 리소스들의 URI 를 결정한다.
- collection 리소스를 표현하기 위해서는 복수 표현으로 이름을 정한다.

## store

```jsx
http://api.example.com/song-management/users/{id}/playlists
```

- store 리소스는 client-managed 리소스 저장소이다. store 리소스는 API 를 사용하는 client 가 리소스를 입력, 출력, 삭제 등을 수행할 수 있도록 한다.
- store 는 절대로 새로운 URI들을 생성하지 않는다. 대신 각각의 저장된 리소스는 개별의 URI 를 가진다. 이들은 초기에 store 에 입력될때 client 에서 결정되어 들어온다.
- store 리소스를 표현하기 위해서 URI 에서는 복수형 이름을 사용한다.

## controller

```jsx
http://api.example.com/cart-management/users/{id}/cart/checkout
http://api.example.com/song-management/users/{id}/playlist/play
```

- controller 리소스 절차, 프로세스의 개념을 규격화한다. controller 리소스는 실행 가능한 함수와 같이 매개변수와 반환 값, 입력값과 출력값을 가지고 있다.
- controller 리소스를 표현하기 위해서는 동사를 사용한다.