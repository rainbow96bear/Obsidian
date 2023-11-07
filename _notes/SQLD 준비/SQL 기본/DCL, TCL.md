# **1. DCL (Data Control Language)** - 데이터 제어어

데이터베이스 객체에 대한 권한과 보안을 관리하기 위한 언어

## 명령어

<table border="1" cellspacing="0" cellpadding="10">
	<tr>
		<th>명령어</th>
		<th>설명</th>
	</tr>
	<tr>
		<td>GRANT</td>
		<td>사용자나 역할에 대해 특정 데이터베이스 객체에 대한 권한 부여</td>
	</tr>
	<tr>
		<td>REVOKE</td>
		<td>부여한 권한을 회수</td>
	</tr>
</table>

## 예시 코드

<code>
GRANT SELECT ON 테이블 명 TO 사용자 ID;
</code>   

사용자 ID에게 테이블 명에 해당하는 테이블의 SELECT 권한을 부여

<code>
REVOKE SELECT ON 테이블 명 FROM 사용자 ID;
</code>   

사용자 ID에게서 테이블 명에 해당하는 테이블의 SELECT 권한을 취소

# **2. TCL (Transaction Control Language) - 트랜잭션 제어어**

데이터베이스에서 트랜잭션을 관리하는 명령어

## 명령어

<table border="1" cellpadding="10">
  <tr>
    <th>명령어</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>COMMIT</td>
    <td>데이터베이스 트랜잭션을 확정</td>
  </tr>
  <tr>
    <td>ROLLBACK</td>
    <td>트랜잭션을 취소하고 변경사항을 이전으로 돌림</td>
  </tr>
</table>
