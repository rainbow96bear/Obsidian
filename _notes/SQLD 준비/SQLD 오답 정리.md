# **1. 데이터 모델링의 이해**
#### 모델링 특징 
- 추상화
- 단순화
- 정확화

### 모델링 주의 사항
- **중복**   
	여러 장소에 같은 정보를 저장하지 않도록 주의
- **비유연성**   
	작은 변화에 중대한 변화를 일으키지 않도록 주의
- **비일관성**
	데이터와 데이터간의 상호 연관 관계에 대해 명확하게 정의

#### 설계 단계
1. **개념적 설계 단계**
	- 트랜잭션 인터페이스 설계
	- 엔터티와 관계정도만 표현
1. **논리적 설계 단계**
	- ERD 엔터티를 테이블로 구체화
	- 정규화를 거치는 단계
2. **물리적 설계 단계**
	- 목표 DBMS에 맞는 물리적 구조의 데이터로 변환
	- 트랜잭션 실제로 작성

#### 데이터 베이스 스키마 구조
- 외부 스키마 : 사용자 관점
- 개념 스키마 : 설계자 관점
- 내부 스키마 : 개발자 관점

#### **데이터 베이스 설계 시 고려사항**
- 데이터 무결성 유지
- 데이터 일관성 유지
- 데이터 보안성 유지

#### 데이터 모델에 표시할 요소
- **구조(Structure)** : 논리적으로 표현된 개체 타입들 간의 관계로서 데이터 구조 및 정적 성질을 표현
- **연산(Operation)** : 데이터베이스를 조작하는 기본 도구
- **제약(Constraint)** : 실제 데이터의 논리적인 제약 조건

#### 엔터티 특징
- 해당 업무에서 필요하고 관리하고자 하는 정보
- 유일한 식별자에 의하여 식별 가능
- 영속적으로 존재하는 두 개 이상의 인스턴스의 집합
- 업무 프로세스에 의해 이용되어야 한다.
- 반드시 속성이 있어야 한다.
- 다른 엔터티와 한 개 이상의 관계가 있어야 한다.

#### 엔터티 분류
- 발생 시점
	- 기본(키) 엔터티 : 타 엔터티의 부모 역할
	- 중심 엔터티 : 다른 엔터티와의 관계로 행위 엔터티 생성
	- 행위 엔터티 : 2개 이상의 부모 엔터티로부터 발생
- 유형과 무형
	- 유형 엔터티 : 물리적 형태
	- 개념 엔터티 : 개념적 정보
	- 사건 엔터티 : 업무에 따른 결과

#### 엔터티 이름
- 현업 업무에서 사용하는 용어
- 약어 금지
- 단수 명사
- 고유한 이름

#### 속성 분류
1. 특성에 따른 분류
	- 기본 속성 : 일반적인 속성
	- 설계 속성 : 만들어진 속성 (ex - 일련 번호)
	- 파생 속성 : 다른 속성에 영향을 받아 발생하는 속성 (ex - 평균)

#### 도메인
속성에 대한 데이터 타입, 크기, 제약사항 지정

#### 식별자 특징
- **유일성** : 주식별자에 의해 모든 인스턴스들이 유일하게 구분
- **최소성** : 주식별자를 구성하는 속성의 수는 최수의 수
- **불변성** : 지정된 주식별자의 값은 자주 변하지 않아야함
- **존재성** : 주식별자가 지정되면 반드시 값이 필요

#### 식별자 분류
- **대표성 여부**
	- **주식별자** : 타 엔터티와 참조 관계 연결 가능
	- **보조 식별자** : 참조관계 연결 불가
- **스스로 생성 여부**
	- **내부 식별자** : 엔터티 내에 스스로 생성
	- **외부 식별자** : 타 엔터티로부터 받아오는 식별자
- **속성의 수**
	- **단일 식별자** : 하나의 속성으로 구성
	- **복합 식별자** : 2개 이상의 속성으로 구성
- **대체 여부**
	- **본질 식별자** : 업무에 의해 생성
	- **인조 식별자** : 인위적으로 생성

# **2. 데이터 모델과 성능**

#### 성능 데이터모델링 순서
1. 정규화
2. 용량산정
3. 트랜잭션 유형 파악
4. 반정규화
5. 이력모델의 조정, PK/FK 조정, 슈퍼타입/서브타입 조정
6. 데이터 모델 검증

#### 정규화 종류
- **1차 정규화** : 각 열은 원자적인 값만 포함 
- **2차 정규화** : 부분 종속 제거 - 복합키 구성일 때 부분적 함수 종속 관계 분
- **3차 정규화** : 이행적 종속 제거 - 일반 컬럼에 의존하는 컬럼 분리
- **BCNF** : 결정자가 후보 키가 아니면 분리하여 새로운 테이블 생성
- **4차 정규화** : 하나의 속성이 여러 개의 독립적인 다중 값 속성을 갖지 않도록 다치 종속 제거
- **5차 정규화** : 다중 값 속성 간에 조인이 의존되지 않도록 조인 종속 해결
- **6차 정규화** : 레퍼런스 가능한 모든 종속을 처리하여 다른 정규 형태들이 해결하지 못하는 특별한 경우를 다룸

#### 로우체이닝
로우의 길이가 너무 길어서 데이터 블록 하나에 데이터가 모두 저장되지 않고 두 개 이상의 블록에 걸쳐 하나의 로우가 저장되어있는 형식

#### 슈퍼 타입, 서브타입
- **슈퍼타입**
	- 더 일반적이고 범용적인 타입
	- 여러 서브 타입들이 공통으로 가지는 속성이나 특징을 정의
	- 구체적인 인스턴스 가질 수 없음
	- 일반적으로 테이블 하나로 표현되며, 서브타입들의 공통 속성이 담겨있음
- **서브타입**
	- 슈퍼타입에서 파생되는 구체적인 타입
	- 슈퍼타입의 모든 속성을 상속하며, 추가적인 속성이나 특징을 가질 수 있음

# **3. SQL 기본**

#### 데이터베이스 명령어 종류
- **DML** : SELECT, INSERT, UPDATE, DELETE
- **DDL** : CREATE, ALTER, DROP, RENAME
- **DCL** : GRANT, REVOKE
- **TCL** : COMMIT, ROLLBACK

#### 제약 조건
- **PRIMARY KEY** : UNIQUE & NOT NULL
- **UNIQUE KEY** : 중복 불가, NULL 가능
- **NOT NULL** : NULL값 불가
- **CHECK** : 특정 열에 대하여 데이터의 유효성을 검증
	- ex) AGE INT CHECK (AGE>=0)

#### 테이블 생성 시 PRIMARY KEY 지정 방법
<code>
CREATE TABLE PRODUCT ( <br>
    PROD_ID INT PRIMARY KEY, <br>
    NAME VARCHAR(255), <br>
    PRICE DECIMAL(10, 2), <br>
    CATEGORY VARCHAR(50) <br>
); <br>
</code>
<code>
CREATE TABLE PRODUCT ( <br>
    PROD_ID INT, <br>
    NAME VARCHAR(255), <br>
    PRICE DECIMAL(10, 2), <br>
    CATEGORY VARCHAR(50) <br>
    PRIMARY KEY (PROD_ID, NAME) <br>
); <br>
</code>

<code>
CREATE TABLE PRODUCT ( <br>
    PROD_ID INT, <br>
    NAME VARCHAR(255), <br>
    PRICE DECIMAL(10, 2), <br>
    CATEGORY VARCHAR(50), <br>
    CONSTRAINT PRODUCT_PK PRIMARY KEY (PROD_ID, NAME) <br>
); <br>
</code>

* PRIMARY KEY 지정   
<code>
ALTER TABLE PRODUCT
ADD CONSTRAINT PRODUCT_PK PRIMARY KEY (PROD_ID);
</code>

#### AUTO COMMIT
- DDL은 실행 시 AUTO COMMIT
- DML은 COMMIT을 직접 입력

#### 트랜잭션 4가지 특성
- **원자성** : 트랜잭션에 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아있어야한다.
- **일관성** : 트랜잭션이 실행되기 전의 데이터베이스 내용이 잘못 되어 있지 않다면 트랜잭션이 실행된 이후에도 데이터 베이스의 내용에 잘못이 있으면 안된다.
- **고립성** : 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안된다.
- **지속성** : 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터 베이스의 내용은 영구적으로 저장된다.

#### SEARCHED_CASE_EXPRESSION, SIMPLE_CASE_EXPRESSION
- **SEARCHED_CASE_EXPRESSION**   
<code>SELECT
    CASE
        WHEN salary > 50000 THEN 'High Salary'
        WHEN salary > 30000 THEN 'Medium Salary'
        ELSE 'Low Salary'
    END AS salary_category
FROM employees;
</code>

- **SIMPLE_CASE_EXPRESSION**   
<code>SELECT
    CASE department_id
        WHEN 1 THEN 'HR Department'
        WHEN 2 THEN 'IT Department'
        WHEN 3 THEN 'Finance Department'
        ELSE 'Other Department'
    END AS department_name
FROM employees;
</code>

#### WITH TIES (SQL Server)
ORDER BY절과 함께 사용되는 옵션으로 ORDER BY에 사용된 컬럼 기준으로 동점자를 포함하여 출력
##### 예시 코드
<code>
SELECT TOP(2) WITH TIES NAME, GRADE <br>
FROM STUDENT <br>
ORDER BY GRADE DESC;
</code>

# **4. SQL 활용**

#### 집합 연산자
- **UNION** : 합집합 (중복 행 1개)
- **UNION ALL** : 합집합 (중복 행 표시)
- **INTERSECT** : 교집합
- **MINUS** : 차집합 (Oracle에 존재, MySQL EXPECT와 유사)
- **CROSS JOIN** : 곱집합 (cartesian product)

#### 순수 관계 연산자
- SELECT
- PROJECT
- JOIN
- DIVIDE

#### USING
같은 이름을 가진 컬럼들 중에서 원하는 컬럼에 대하여 EQUI JOIN가능   
<code>
SELECT A.ID, A.NAME
FROM TABLE A
LEFT JOIN TABLE B USING (ID)
</code>

#### 앵커 멤버
계층형 데이터에서 일반적으로 최상위 레벨의 노드를 나타내는데 사용

#### 연관 서브쿼리
- 상호작용 있음 : 서브쿼리 내부에서 외부 쿼리의 컬럼이나 테이블에 접근   
<code>
SELECT department_id, employee_name
FROM employees e_outer
WHERE salary = (
    SELECT MAX(salary)
    FROM employees e_inner
    WHERE e_inner.department_id = e_outer.department_id
);
</code>

#### 비연관 서브쿼리
- 상호 작용 없음 : 서브쿼리 내부에서 외부 쿼리의 컬럼이나 테이블에 접근하비 않습니다.   
<code>
SELECT employee_name
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
</code>

#### 인라인 뷰
FROM 절에서 사용되는 서브쿼리

#### 뷰
- 실제 데이터를 가지고 있지 않는 가상 테이블   
- 실행 시점에 SQL 재작성 하여 수행됨
#### 뷰 장점
- **독립성** : 테이블 구조가 변경되어도 뷰를 사용하는 응용 프로그램은 변경하지 않아도 된다.
- **편리성** : 복잡한 질의를 뷰로 생성함으로써 관련 질의를 단순하게 작성할 수 있다.
- **보안성** : 숨기고 싶은 정보가 존재할 때 사용

#### 윈도우 함수
- **RANK, DENSE_RANK**
- **ROW_NUMBER**
- **SUM, AVG, MIN, MAX**
- **LEAD, LAG**
- **FIRST_VALUE, LAST_VALUE**
- **COUNT**

#### 절차적 DML, 비절차적 DML
- **절차적 DML** : 어떻게 데이터를 접근해야하는지 명세
	- ex) MySQL의 DELIMITER 사용
- **비절차적 DML** : 사용자가 무슨 데이터를 원하는지 명세
	- ex) SELECT * FROM TABLE