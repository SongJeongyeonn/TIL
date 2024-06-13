# DDL
- Data Definition Language는 '데이터를 정의하는 언어'로서, 오브젝트를 정의한다.

|DDL 대상|설명|
|--|--|
|스키마|DBMS 특성과 구현 환경을 감안한 데이터 구조|
||직관적으로 하나의 데이터베이스로 이해 가능|
|도메인|속성의 데이터 타입과 크기, 제약 조건 등을 지정한 정보|
||속성이 가질 수 있는 값의 범위|
|테이블|데이터 저장 공간|
|뷰|하나 이상의 물리 테이블에서 유도되는 가상의 논리 테이블|
|인덱스|검색을 빠르게 하기 위한 데이터 구조|
### DDL 유형
|구분|DDL 명령어|내용|
|-|-|-|
|생성|CREATE|데이터베이스 오브젝트 생성|
|변경|ALTER|데이터베이스 오브젝트 변경|
|삭제|DROP|데이터베이스 오브젝트 삭제|
||TRUNCATE|데이터베이스 오브젝트 내용 삭제, 데이블 구조는 유지|
### DDL의 활용
**1. 테이블 생성**

|구분|문법|
|-|-|
|신규 생성|CREATE TABLE 테이블이름 (|
||열 이름 데이터 타입 [DEFAULT 값] [NOT NULL]|
||[PRIMARY KEY(열 리스트)]|
||{[FOREIGN KEY(열 리스트) REFERENCES 테이블 이름 [(열이름)]|
||[ON DELETE 옵션]|
||[ON UPDATE 옵션]]}|
||[CHECK (조건식) ㅣ UNIQUE(열이름)]);|
|다른 테이블 정보를 이용한 테이블 생성|CREATE TABLE 테이블이름 AS SELECT 문;|
**2. 테이블 변경**

|구분|문법|
|-|-|
|열 추가|ALTER TABLE 테이블이름 ADD 열이름 데이터 타입 [DEFAULT 값]|
|열 데이터 타입 변경|ALTER TABLE 테이블이름 MODIFY 열이름 데이터 타입 [DEFAULT 값]|
|열 삭제|ALTER TABLE 테이블이름 DROP 열이름|
**3. 테이블 삭제 / 내용 삭제, 이름 변경**

|구분|문법|
|-|-|
|테이블 삭제|DROP TABLE 테이블이름|
|테이블 내용 삭제|TRUNCATE TABLE 테이블이름|
|테이블 이름 변경|RENAME TABLE 이전 테이블이름 TO 새로운 테이블이름|
||ALTER TABLE 이전 테이블이름 RENAME 새로운 테이블이름|
**4. 데이터 타입**

|유형|정의|
|-|-|
|CHAR|고정 길이 문자열 데이터타입|
|VARCHAR|가변 길이 문자열 데이터타입|
|INT|숫자에 사용되는 데이터 타입|
|FLOAT|소수형 데이터 타입|
|DATE|날짜에 사용되는 데이터 타입|
### 제약조건 적용
**1. 제약조건 유형**

|제약조건|설명|
|-|-|
|PRIMARY KEY| 테이블의 기본키를 정의하며 기본으로 NOT, NULL, UNIQUE 제약이 포함|
|FOREIGN KEY| 외래키를 정의하고, 참조 대상을 테이블 이름으로 명시해야한다.|
||참조 무결성 위배 상황 시 처리방법으로 옵션 지정 가능 - NO ACTION, SET DEFQULT, SET NULL, CASCADE, RESTRICT|
|UNIQUE|테이블 내에서 열은 유일한 값을 가지며, 중복된 값을 가져서는 안되는 항목에 지정함|
|NOT NULL|테이블 내에서 관련 열의 값은 NULL일수 없고 필수 입력 항목에 대해 제약조건으로 설정함|
|CHECK|개발자가 정의하는 제약조건으로 상항에 따라 다양한 조건을 설정 가능|

**2. 제약조건 변경**

|내용|SQL 명령문|
|-|-|
|제약조건 추가|ALTER TABLE 테이블이름|
||ADD [CONSTRAITNT 제약조건이름] 제약조건(열이름)|
|제약조건 삭제|ALTER TABLE '주문테이블' DROP FOREIGN KEY [제약조건이름];|
|제약조건 활성화|ALTER TABLE 테이블이름|
||ENABLE CONSTRAINT 제약조건이름|
|제약조건 비활성화|ALTER TABLE 테이블이름|
||DISABLE CONSTRAINT 제약조건이름|

### 예제 (SQL - DDL)
**① 테이블 생성 : CREATE**
- 급여라는 테이블을 생성하여 길이에 상관 없는문자열로 ID와 고객명 컬럼을 설정하고, 나이는 숫자, 입사연도는 날짜로 정의하시오.
- 기본키는 ID로 설정하고, ID와 인사연도는 공백을 허용하지 않으며, 입사연도가 입력되지 않을 시 2020으로 입력되도록 기본값을 설정하시오.
```
CREATE TABLE 급여(
    ID VARCHAR(20) NOT NULL
    고객명 VARCHAR(20)
    나이 INT
    입사연도 DATE NOT NULL DEFAULT 2020
    PRIMARY KEY(ID)
)
```
**② 컬럼 이름 및 타입 변경 : ALTER**

- 주문 테이블의 배송지를 배송지역으로 변경하시오.
```
ALTER TABLE '주문' CHANGE '배송지' '배송지역';
```
- 주문 테이블의 상품 데이터 형식을 가변 문자형으로 표현하고 null 값을 허용하지 않도록 하시오.
```
ALTER TABLE '주문' ALTER COLUMN '상품' VARCHAR(20) NOT NULL;
```
**③ 테이블 또는 컬럼 삭제 : DROP**

- 급여 테이블을 삭제하시오.
```
DROP TABLE '급여';
```
- 급여 테이블에서 부서 컬럼만 삭제하시오.
```
ALTER TABLE '급여' DROP COLUMN '부서';
```

**DROP문에서 쓰이는 기타 SQL 명령어들**
- **RESTRICT** : 삭제할 테이블(데이터)이 참조 중이면 삭제하지 않는다.
- **CASCADE** : 삭제할 테이블(데이터)이 참조 중이라도 삭제하게 되면, 삭제할 요소와 참조된 모든 요소를 연쇄적으로 삭제한다.

# DML
Data Manipulation Language 데이터를 조작(데이터 관점에서 생명주기를 제어)하는 명령어를 말한다.

**DML 유형**

|구분|DML 명령어|내용|
|-|-|-|
|데이터 조회|SELECT|테이블의 내용을 조회|
|데이터 삭제|DELETE|테이블의 내용을 삭제|
|데이터 변경|UPDATE|테이블의 내용을 변경|
|데이터 추가|INSERT|테이블의 내용을 추가|
### DML의 활용
**1. 데이터 조회** : 데이터의 내용을 조회할 때 사용하는 명령어이다.
- SELET 명령어의 기본형식
```
SELECT [OPTION] columns FROM table [WHERE 절];
```
- SELECT 문에서 사용되는 요소

|요소|요소값| 내용|
|-|-|-|
|OPTION|ALL|중복을 포함한 조회 결과 출력|
||DISTINCT|중복을 제외한 결과 추력|
|columns|컬럼명 목록|SELECT를 통해 조회할 컬럼명 지정|
||와일드 카드|모두 또는 전체를 의미하는 '*'|
**SELECT문에서 쓰이는 기타 SQL명령어들**
- DISTINCT : 중복된 값을 한 번만 검색되도록 한다.
- BETWEEN : A AND B, 즉 A값과 B값 사이를 만족하는 부분을 검색한다.
- IN : IN(A,B), OR과 동일하게 참조하는 부분 중 하나라도 만족하는 부분을 검색한다.
- ORDER BY : 오름차순 ASC, 내림차순 DESC를 사용하여 정렬한다.
- HAVING : GROUP BY에 의해 그룹으로 분류된 부분에서 WHERE 대신 조건절을 대신한다.

**2. 데이터 삭제**
- 레코드를 삭제할 때 DELETE 명령문 (조건절 없이 DELETE를 사용하는 경우, 테이블 전체가 한 번에 삭제된다.)
```
DELETE FROM table [WHERE 절];
```
**3. 데이터 변경**
- 데이터를 변경, 수정할 때 UPDATE 명령문(보통 WHERE 절을 통해 어떤 조건이 만족할 경우에만 특정 칼럼의 값을 수정하는 용도로 사용된다.)
```
UPDATE table SET column1 = value1, column2 = value2, ...[WHERE 절];
```
**3. 데이터 추가**
- 데이터를 삽입하기위한 명령어로, 두가지 형태를 제공한다.(삽입의 결과로 하나의 레코드가 추가되기에 삽입에 사용되는 정보는 하나의 레코드를 충분히 묘사해야 한다.)
```
INSERT INTO table_name (column1, column2, ...) VALUES(value1, value2, ...);
INSERT INTO tavle_name VALUES (value1, value2, ...);
```
### 예제 (SQL-DML)
**① 데이터 조회 : SELECT**
- 아무 조건 없이 학생 테이블의 모든 컬럼을 조회하시오.
```
SELECT * FROM 학생;
```
- 학생 테이블에서 학년이 2학년인 모든 컬럼을 조회하시오.
```
SELECT * FROM 학생 WHERE 학년 = 2;
```
- 학생 테이블에서 중복을 제외한 동아리명 컬럼을 조회하시오.
```
SELECT DISTINCT 동아리명 FROM 학생;
```
- 학생 테이블에서 학년이 3학년이고, 과목이 영어인 학생의 성명과 연락처를 조회하시오.
```
SELECT 성명, 연락처 FROM 학생 WHERE 학년 = 3 AND 과목 = '영어'
``` 
**② 데이터 삭제 : DELETE(특정 칼럼만)**
- 학생 테이블에서 전체 행을 제거하시오.
```
DELETE FROM '학생';
```
- 학생 테이블에서 학년이 3학년인 데이터를 삭제하시오.
```
DELETE FROM '학생' WHERE 학년 = 3;
```
**③ 데이터 수정 : UPDATE**
- 판매내역 테이블에 재고가 없으면 상태를 '판매불가'라고 수정하시오.
```
UPDATE '판매내역' SET 상태 = '판매불가' WHERE 재고 IS NULL
```
**④ 데이터 추가 : INSERT**
- 회원 테이블에서 회원번호 1112, 성명 '윤지영', 지역'인천', 연락처'486-1112'인 회원을 추가하시오.
```
INSWERT INTO 회원(회원번호, 성명, 지역, 연락처)
VALUES (1112, '윤지영', '인천', '486-1112');
```

# DCL
Data Control Language로 데이터 베이스에서 데이터 이외의 오브젝트에 대해 조작할때 사용하는 명령이다.

**DCL의 조작 대상, 오브젝트 유형**

|오브젝트|목적|내용|
|-|-|-|
|사용자 권한|접근통제|사용자를 등록하고, 사용자에게 특정 데이터베이스를 사용할 수 있는 권리를 부여하는 작업|
|트랜잭션|안전한 거래 보장|동시에 다수의 작업을 독립적으로 안전하게 처리하기 위한 상호작용 단위|

**DCL 유형**
|유형|명령어|용도|
|-|-|-|
|DCL|GRANT|데이터베이스 사용자 권한 부여
||REVOKE|데이터베이스 사용자 권한 회수|
|TCL|COMMIT|트랜잭션 확정|
||ROLLBACK|트랜잭션 취소|
||CHECKPOINT|트랜잭션 설정|
