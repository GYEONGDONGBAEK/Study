# [SQLD] SELECT

---

# SELECT

데이터베이스에서 행을 검색하고 SQL Server에서 하나 이상의 테이블에서 하나 이상의 행 또는 열을 선택할 수 있도록 한다.

## SELECT 구문

```sql
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]
```

## SELECT 문의 논리적 처리 순서

SELECT 문의 논리적 처리 순서(바인딩 순서)는 아래와 같다.

1. FROM
2. ON
3. JOIN
4. WHERE
5. GROUP BY
6. WITH CUBE or WITH ROLLUP
7. HAVING
8. SELECT
9. DISTINCT or ALL
10. ORDER BY
11. TOP

위 순서는 옵티마이저가 SQL 문장의 SYNTAX, SEMANTIC 에러를 점검하는 순서이기도 하다. 예를 들면 FROM 절에 정의되지 않은 테이블의 칼럼을 WHERE 절, GROUP BY 절, HAVING 절, SELECT 절, ORDER BY 절에서 사용하면 에러가 발생한다.

그러나 ORDER BY 절에는 SELECT 목록에 나타나지 않은 문자형 항목이 포함될 수 있다. 단 SELECT DISTINCT를 지정하거나 SQL 문장에 GROUP BY 절이 있거나, SELECT 문에 UNION 연산자가 있으면 열 정의가 SELECT 목록에 표시되야 한다.

이 부분은 관계형 데이터베이스가 데이터를 메모리에 올릴 때 행 단위로 모든 칼럼을 가져오게 되므로, SELECT 절에서 일부 컬럼만 선택하더라도 ORDER BY 절에서 메모리에 올라와 있는 다른 칼럼의 데이터를 사용할 수 있다.

---

## **SELECT DISTINCT ( 중복제거 )**

DISTINCT는 중복제거 키워드다.

SELECT로 DB에서 컬럼을 조회할 때 중복값을 제거하고 조회할 때 사용한다.

## **SELECT DISTINCT 사용방법**

```sql
SELECT DISTINCT 필드 FROM 테이블
// 테이블에서 필드에 대해 중복제외하여 출력한다.
```

## **DISTINCT 키워드 뒤에 2개 이상의 컬럼 사용 시**

DISTINCT뒤에 2개 이상의 칼럼을 사용한다면, DISTINCT뒤에 오는 모든 컬럼을 하나의 행으로 인식하여, 그 행의 중복을 제거한다.

```sql
SELECT DISTINCT age, name FROM value
// value테이블에서 age, name 컬럼을 합쳐서 중복인 행을 제거한다.
```

---

## **별칭(Alias)**

별칭을 사용하는 방법은 간단하다 컬럼명 뒤에 as를 붙여 별칭을 넣어주기만 하면 된다.

별칭의 경우 현재 사용하고있는 SELECT 구문 문장에 대해서만 유효하고, 최대 30자 까지 가능하나 별칭이므로 최대한 짧게 알기 쉽게 하는것이 좋다.

대소문자, 공백, 한글, 특수문자 등을 표현할 수 있는데, 띄어쓰기를 하거나 특수문자가 맨 앞에 들어갈 경우에는 인용부호(쿼터)로 묶어줘야 한다.

FROM 에는 사용할수 없다.

```sql
SELECT test1 AS "*aliasTest" FROM test
SELECT test1 as "alias Test" FROM test
```

---

## CONCAT

문자열을 병합할 수 있도록 도와주는 함수다.

Oracle 에서는 인수가 2개이기 때문에 만약 3개 이상의 인수를 병합시키려고 하면 || 연산자를 사용하는것이 더 좋다.

SQL server 에서는 || 연산자 대신 + 를 사용한다.

```sql
SELECT CONCAT(문자열, 문자열) FROM 테이블;
SELECT CONCAT(CONCAT(문자열, ' '), 문자열) FROM 테이블;
SELECT 문자열||' '||문자열 FROM 테이블;
```
