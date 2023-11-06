
# DDL (Data Definition Language) - 데이터 정의어

데이터 베이스의 구조를 정의하고 관리하는 언어

## 명령어

<table border="1">
  <tr>
    <th style="padding: 10px;">명령어</th>
    <th style="padding: 10px;">설명</th>
  </tr>
  <tr>
    <td style="padding: 10px;">CREATE</td>
    <td style="padding: 10px;">데이터 베이스 개체 생성</td>
  </tr>
  <tr>
    <td style="padding: 10px;">ALTER</td>
    <td style="padding: 10px;">데이터 베이스 개체의 구조 수정</td>
  </tr>
  <tr>
    <td style="padding: 10px;">DROP</td>
    <td style="padding: 10px;">데이터 베이스 개체 삭제</td>
  </tr>
  <tr>
    <td style="padding: 10px;">RENAME</td>
    <td style="padding: 10px;">데이터 베이스 개체 이름 변경</td>
  </tr>
</table>

## 데이터 형식

<table border="1">
  <tr>
    <th style="padding: 10px;">형식</th>
    <th style="padding: 10px;">설명</th>
  </tr>
  <tr>
    <td style="padding: 10px; text-align: center;">INTEGER</td>
    <td style="padding: 10px;">정수형 데이터</td>
  </tr>
  <tr>
    <td style="padding: 10px; text-align: center;">CHAR</td>
    <td style="padding: 10px;">고정 길이 문자열<br>지정된 길이보다 짧은 데이터는 공백으로 길이를 맞춘다.</td>
  </tr>
  <tr>
    <td style="padding: 10px; text-align: center;">VARCHAR</td>
    <td style="padding: 10px;">가변 길이 문자열<br>지정된 길이보다 짧은 데이터는 공
    </tr>
</table>

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

DDL