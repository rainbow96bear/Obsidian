# DML (Data Manipulation Language) - 데이터 조작어

## 명령어

<table border="1">
  <tr>
    <th style="padding: 10px;">명령어</th>
    <th style="padding: 10px;">설명</th>
  </tr>
  <tr>
    <td style="padding: 10px;">INSERT</td>
    <td style="padding: 10px;">데이터 추가 </td>
  </tr>
  <tr>
    <td style="padding: 10px;">UPDATE</td>
    <td style="padding: 10px;">데이터 수정</td>
  </tr>
  <tr>
    <td style="padding: 10px;">DELETE</td>
    <td style="padding: 10px;">데이터 삭제</td>
  </tr>
  <tr>
    <td style="padding: 10px;">SELECT</td>
    <td style="padding: 10px;">데이터 출력</td>
  </tr>
</table>

## 예시 코드

### INSERT

<code>
INSERT INTO 테이블 명 (컬럼 명1, 컬럼 명2, ... )
VALUES (값1, 값2, ...);   
</code>   

컬럼 명과 값을 1:1로 매칭하여 데이터 추가

<code>
INSERT INTO 테이블 명
VALUES (값1, 값2, ... , 값n);   
</code>   

값을 컬럼 순서대로 하나씩 입력   
비우고 싶은 값은 NULL 입력

### UPDATE

<code>
UPDATE 테이블 명 
SET 컬럼 명1 = 값1, 컬럼 명2 = 값 2;
</code>   

SET의 컬럼에 해당하는 테이블에 모든 값을 입력된 값으로 변경

<code>
UPDATE 테이블 명
SET 컬럼 명1 = 값1, 컬럼 명2 = 값 2
WHERE 컬럼 명3 = 값3;
</code>   

WHERE 조건이 일치하는 자료들만 SET의 컬럼에 해당하는 값을 입력된 값으로 변경을 변경

### DELETE 

<code>
DELETE FROM TABLE;
</code>   

테이블의 모든 내용을 지움

<code>
DELETE FROM TABLE
WHERE 컬럼 명 = 값
</code>   

WHERE 조건이 일치하는 자료들을 지움

### SELECT

<code>
SELECT 컬럼 명1, 컬럼 명2 FROM 테이블 명
</code>   

컬럼 명에 해당하는 자료들을 출력

<code>
SELECT * FROM 테이블 명
</code>   

테이블의 모든 자료를 출력
