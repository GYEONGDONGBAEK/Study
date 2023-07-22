# [DB] 사용자 정의 함수 (User-Defined Function)

---

## 사용자 정의함수(User-Defined Function)

- 절차형 SQL을 활용하여 일련의 SQL 처리를 수행하고, 수행 결과를 단일 값으로 반환할 수 있는 절차형 SQL 다.
- DBMS에서 제공되는 공통적 함수 이외에 사용자가 직접 정의하고 작성할 수 있다.

## 사용자 정의함수(User-Defined Function) 구성

- 기본적인 개념 및 사용법, 문법 등은 프로시저와 동일하다.
- 종료 시 단일 값을 반환한다는 것이 프로시저와 가장 큰 차이점이다.
- 사용자 정의함수의 호출을 통해 실행되며, 반환되는 단일 값을 조회 또는 삽입, 수정 작업에 이용하는 것이 일반적이다.

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/2a8939bc-812a-41ae-9fc3-90bde0ba743c">

- 선언부(DECLARE) : 사용자 정의함수의 명칭, 변수와 인수 그리고 그에 대한 데이터 타입을 정의하는 부분
- 시작/종료부(BEGIN/END) : 사용자 정의함수의 시작과 종료를 표현하는데 필수적이며 BEGIN/END가 쌍을 이루어 추가되므로 블록으로 구성다수 실행을 제어하는 기본적 단위가 되며, 논리적 프로세스를 구성
- 제어부(CONTROL) : 기본적으로는 순차적으로 처리비교 조건에 따라 블록 또는 문장을 실행조건에 따라 반복 실행
- SQL : 조회 용도로 SELECT 문을 사용. 데이터를 조작하는 INSERT, UPDATE, DELETE 는 사용할 수 없음
- 예외부(EXCEPTION) : BEGIN~END 절에서 실행되는 SQL문이 실행될 때 예외 발생 시 예외 처리 방법을 정의하는 처리부
- 반환부(RETURN) : 호출문에 대한 함수 값을 반환

## 선언부(DECLARE)

```sql
CREATE FUNCTION 함수명
(
파라미터_명 MODE 데이터_타입
)
IS
RETURN 데이터_타입
변수 선언

CREATE OR REPLACE FUNCTION 함수명
(
파라미터_명 MODE 데이터_타입
)
AS
RETURN 데이터_타입
변수 선언
```

- CREATE : DBMS 내에 객체(트리거, 함수, 프로시저)를 생성. OR REPLACE 는 기존 프로시저 존재 시 현재 컴파일 하는 내용으로 덮어씀(같은 이름의 프로시저가 존재할 경우 OR REPLACE 가 없으면 에러 발생)
- FUNCTION : 사용자 정의함수(FUNCTION) 를 사용한다는 의미
- 함수명 : 해당 사용자 정의함수를 지칭하는 이름
- 파라미터_명 : 사용자 정의함수와 운영체제 간 필요한 값을 전송하기 위한 인자
- MODE : 변수의 입출력을 구분
    1. IN(사용자 정의함수로 값 전달)
    2. OUT(사용자 정의함수에서 처리된 결과)
    3. INOUT(IN과 OUT의 두 가지 기능을 모두 수행)
- 데이터_타입 : 파라미터에 대한 데이터 타입
- IS/AS : PL/SQL 의 블록을 시작. IS 또는 AS 를 작성
- 변수 선언 : 프로시저 내에서 사용할 변수와 변수에 대한 초기값을 설정

### 시작/종료부(BEGIN/END)

사용자 정의함수의 실행 시작과 종료를 알려주는 부분으로 사용자 정의함수에 BEGIN, END 는 반드시 포함되어야 합니다.

### 제어부(CONTROL)

단위 블록별 실행흐름을 제어하는 부분으로 크게 IF문과 CASE문으로 나뉩니다.

### SQL

데이터 관리를 위한 조회, 추가, 수정, 삭제를 수행하는 부분입니다.

INSERT, UPDATE, DELETE 를 통한 데이터 조작은 할 수 없습니다.

**SELECT 를 통한 조회만 가능합니다.**

### 예외부(EXCEPTION)

실행 중 발생 가능한 예외상황을 수행하는 부분이다.

### 반환부(RETURN)

RETURN 명령을 통해 사용자 정의함수 종료 시 사용자 정의함수를 호출한 쿼리에 반환하는 단일값을 정의합니다.

### 사용자 정의함수 호출문

```sql
함수명(파라미터1, 파라미터2, ...)
```