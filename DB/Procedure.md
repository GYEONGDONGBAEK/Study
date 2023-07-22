# [DB] 프로시저(Procedure)

---

## 프로시저(Procedure)의 개념

- 프로시저는 절차형 SQL 을 활용하여 특정 기능을 수행할 수 있는 트랜잭션 언어다.
- 프로시저는 호출을 통해 실행된다.
- 일련의 SQL 작업을 포함하는 데이터 조작어(DML, Data Manipulate Language)를 수행한다.
- DML(Data Manipulate Language) 데이터베이스에 저장된 자료들을 입력, 수정, 삭제, 조회를 하는 언어로 SELECT, INSERT, UPDATE, DELETE 명령이 존재한다.

---

## **프로시저 구성**

<img src="https://github.com/GYEONGDONGBAEK/study/assets/122242439/35ac5cba-769f-412a-93a9-af9f8ffe9d78">

- 선언부(DECLARE) : 프로시저의 명칭, 변수와 인수 그리고 그에 대한 데이터 타입을 정의하는 부분
- 시작/종료부(BEGIN/END) : 프로시저의 시작과 종료를 표현하며, BEGIN/END가 쌍을 이룬다. 다수 실행을 제어하는 기본적 단위가 되며 논리적 프로세스를 구성
- 제어부(CONTROL) : 기본적으로는 순차적으로 처리조건문과 반복문을 이용하여 문장을 처리
- SQL : DML을 주로 사용한다. 자주 사용되지 않지만 DDL 중 TRUNCATE 사용
- 예외부(EXCEPTION) : BEGIN~END절에서 실행되는 SQL문이 실행될 때 예외 발생 시 예외 처리 방법을 정의하는 처리부
- 실행부(TRANSACTION) : 트리거에서 수행된 DML 수행 내역의 DBMS의 적용 또는 취소 여부를 결정하는 처리부

### **선언부(DECLARE)**

```sql
CREATE PROCEDURE 프로시저_명
(
파라미터_명 MODE 데이터_타입
)
IS
변수 선언

CREATE OR REPLACE PROCEDURE 프로시저_명
(
파라미터_명 MODE 데이터_타입
)
AS
변수 선언
```

- CREATE : DBMS 내에 객체(트리거, 함수, 프로시저)를 생성. OR REPLACE 는 기존 프로시저 존재 시 현재 컴파일 하는 내용으로 덮어씀(같은 이름의 프로시저가 존재할 경우 OR REPLACE 가 없으면 에러 발생)
- PROCEDURE : 프로시저(PROCEDURE)를 사용한다는 의미
- 프로시저_명 : 해당 프로시저를 지칭하는 이름
- 파라미터_명 : 프로시저와 운영체제 간 필요한 값을 전송하기 위한 인자
- MODE : 변수의 입출력을 구분
    1. IN(프로시저로 값 전달)
    2. OUT(프로시저에서 처리된 결과)
    3. INOUT(IN과 OUT의 두 가지 기능을 모두 수행)
- 데이터_타입 : 파라미터에 대한 데이터 타입
- IS/AS : PL/SQL 의 블록을 시작IS 또는 AS 를 작성
- 변수 선언 : 프로시저 내에서 사용할 변수와 변수에 대한 초기값을 설정

### 시작/종료부(BEGIN/END)

프로시저의 실행 시작과 종료를 알려주는 부분으로 BEGIN, END는 프로시저에 반드시 포함되어야 합니다.

### 제어부(CONTROL)

실행흐름을 제어하는 부분으로 조건문과 반복문으로 나뉩니다.

- **조건문**

```sql
-- IF
IF 조건 THEN
  문장;
ELSIF 조건 THEN
  문장;
ELSE
  문장;
END IF;

-- CASE 변수
CASE 변수
  WHEN 값1 THEN
    SET 명령어;
  WHEN 값2 THEN
    SET 명령어;
  ELSE
    SET 명령어;
END CASE;

-- CASE
CASE
  WHEN 조건1 THEN
    SET 명령어;
  WHEN 조건2 THEN
    SET 명령어;
  ELSE
    SET 명령어;
END CASE;
```

- **반복문**

```sql
-- LOOP
LOOP
  문장;
  EXIT WHEN 탈출조건;
END LOOP;

-- WHILE
WHILE 반복 조건 LOOP
  문장;
  EXIT WHEN 탈출조건;
END LOOP;

-- FOR LOOP
FOR 인덱스 IN 시작 값 .. 종료 값
  LOOP
  문장;
END LOOP;
```

### 프로시저 SQL

SELECT, INSERT, UPDATE, DELETE 문을 작성한다.

### 예외부(EXCEPTION)

실행 중 발생 가능한 예외상황을 수행하는 부분입니다.

```sql
EXCEPTION
  WHEN 조건 THEN
    SET 명령어;
```

### 실행부(TRANCSTION)

해당 프로시저에서 수행한 DML을 DBMS에 반영할지 복구할지를 결정하는 부분입니다

- COMMIT : 하나의 트랜잭션이 성공적으로 끝나고, 데이터베이스가 일관성이 있는 상태에 있을 때 하나의 트랜잭션이 끝났을 때 사용
- ROLLBACK : 하나의 트랜잭션이 비정상적으로 종료되어 트랜잭션 원자성이 깨질 경우 처음부터 다시 시작하거나, 부분적으로 연산을 취소할 때 사용

### **프로시저 호출문**

```sql
EXECUTE 프로시저_명(파라미터_명1, 파라미터_명2, ...);
```