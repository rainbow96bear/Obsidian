#### 모델링 특징 
- 추상화
- 단순화
- 정확화

#### 모델링 주의 사항
- **중복**   
	여러 장소에 같은 정보를 저장하지 않도록 주의
- **비유성**   
	작은 변화에 중대한 변화를 일으키지 않도록 주의
- **비일관성**
	데이터와 데이터간의 상호 연관 관계에 대해 명확하게 정의

#### 데이터 베이스 스키마 구조
- 외부 스키마
- 개념 스키마 : 통합적 관점
- 내부 스키마

#### 개념 스키마 모델링
- ERD 기술

#### 엔터티 특징
- 해당 업무에서 필요하고 관리하고자 하는 정보
- 유일한 식별자에 의하여 식별 가능
- 영속적으로 존재하는 두 개 이상의 인스턴스의 집합
- 업무 프로세스에 의해 이용되어야 한다.
- 반드시 속성이 있어야 한다.
- 다른 엔터티와 한 개 이상의 관계가 있어야 한다.

#### 엔터티 분류
- 발생 시점
	- 기본(키) 엔터티
	- 중심 엔터티
	- 행위 엔터티
- 유형과 무형
	- 유형 엔터티
	- 개념 엔터티
	- 사건 엔터티

#### 설계 단계
1. **개념적 설계 단계**
	- 트랜잭션 모델링
2. **논리적 설계 단계**
	- 종속적인 논리 스키마 설계
	- 트랜잭션 인터페이스 설계

#### **데이터 베이스 설계 시 고려사항**
- 데이터 무결성 유지
- 데이터 일관성 유지
- 데이터 보안성 유지
#### 데이터 모델에 표시할 요소
- 구조
- 연산
- 제약
<br>
#### 속성 분류
1. 특성에 따른 분류
	- 기본 속성
	- 설계 속성
	- 파생 속성
2. 개체 구성 방식
	- 기본키 속성
	- 외래키 속성
	- 일반 속성
<br>
#### 성능 데이터모델링 순서
1. 정규화
2. 용량산정
3. 트랜잭션 유형 파악
4. 반정규화
5. 이력모델의 조정, PK/FK 조정, 슈퍼타입/서브타입 조정
6. 데이터 모델 검증

#### 정규화 종류
- **1차 정규화** : 각 열은 원자적인 값만 포함 
- **2차 정규화** : 부분 종속 제거 (ex - 복합 키 중 일부 속성이 기본키에 종속되는 경우 실행)
- **3차 정규화** : 이행적 종속 제거 (ex - )
- **BCNF** : 결정자가 후보 키가 아니면 분리하여 새로운 테이블 생성
- **4차 정규화** : 하나의 속성이 여러 개의 독립적인 다중 값 속성을 갖지 않도록 다치 종속 제거
- **5차 정규화** : 다중 값 속성 간에 조인이 의존되지 않도록 조인 종속 해결
- **6차 정규화** : 레퍼런스 가능한 모든 종속을 처리하여 다른 정규 형태들이 해결하지 못하는 특별한 경우를 다


#### 로우체이닝
로우의 길이가 너무 길어서 데이터 블록 하나에 데이터가 모두 저장되지 않고 두 개 이상의 블록에 걸쳐 하나의 로우가 저장되어있는 형식


#### 절차적 DML, 비절차적 DML
- **절차적 DML** : 어떻게 데이터를 접근해야하는지 명세
	- ex) MySQL의 DELIMITER 사용
- **비절차적 DML** : 사용자가 무슨 데이터를 원하는지 명세
	- ex) SELECT * FROM TABLE


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
ALTER TABLE PRODUCT <br>
ADD CONSTRAINT PRODUCT_PK PRIMARY KEY (PROD_ID);
</code>


#### 제약 조건
- **CHECK** : 특정 열에 대하여 데이터의 유효성을 검증
	- ex) AGE INT CHECK (AGE>=0)

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

#### 순수 관계 연산자
- SELECT
- PROJECT
- JOIN
- DIVIDE

#### 윈도우 함수
- **RANK, DENSE_RANK**
- **ROW_NUMBER**
- **SUM, AVG, MIN, MAX**
- **LEAD, LAG**
- **FIRST_VALUE, LAST_VALUE**
- **COUNT**

