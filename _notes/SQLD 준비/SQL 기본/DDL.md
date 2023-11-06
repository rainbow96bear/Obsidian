
# DDL (Data Definition Language) - 데이터 정의어

데이터 베이스의 구조를 정의하고 관리하는 언어

## 명령어

| 명령어 | 설명 |
| :-- | :-- |
| CREATE | 데이터 베이스 개체 생성 |
| ALTER | 데이터 베이스 개체의 구조 수정 |
| DROP | 데이터 베이스 개체 삭제 |
| RENAME | 데이터 베이스 개체 이름 변경 |

## 데이터 형식

| 형식 | 설명 |
| :---: | :--- |
| INTEGER | 정수형 데이터 |
| CHAR | 고정 길이 문자열 <br> 지정된 길이보다 짧은 데이터는 공백으로 길이를 맞춘다. |
| VARCHAR | 가변 길이 문자열 <br> 지정된 길이보다 짧은 데이터는 공백을 추가하지 않는다. |
| DATE | 날짜와 시각 정보 |


## 예시 코드
### CREATE

<code>
CREATE TABLE Employees ( <br> 
	EmployeeID INT PRIMARY KEY, <br> 
	Name VARCHAR(50), <br> 
	Birth_Date DATE, <br> 
	Salary DECIMAL(10, 2) <br> 
);
</code>
Employees 테이블 생성
### ALTER

#### 열 추가
<code>
ALTER TABLE Employees <br> 
ADD Email VARCHAR(100);
</code>

#### 열 삭제
<code>
ALTER TABLE Employees <br> 
DROP COLUMN Email;
</code>

## DROP
<code>
DROP TABLE Employees
</code>
Employees 테이블 삭제

## RENAME

<code>
ALTER TABLE Employees RENAME TO EmployeesList;
</code>
테이블 이름은 Employees 에서 EmployeesList로 변경