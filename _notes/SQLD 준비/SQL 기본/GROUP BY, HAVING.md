# **1. GROUP BY**
주어진 열을 기준으로 데이터를 그룹화하여 소그룹에 대한 항목별 통계 정보를 얻을 때 주로 사용

## 예시 코드
<code>
SELECT CUSTOMER_ID, COUNT(ORDER_ID) <br>
FROM ORDERS <br>
GROUP BY CUSTOMER_ID;
</code>

<br>

### 기본 테이블
<table style="border-collapse: collapse; margin: 0 auto;">
	<tr>
		<th style="border: 1px solid #000; padding: 10px;">order_id</th>
		<th style="border: 1px solid #000; padding: 10px;">customer_id</th>
		<th style="border: 1px solid #000; padding: 10px;">order_date</th>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">1</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-05</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">102</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-10</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">3</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-12</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">4</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">103</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-15</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">5</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">102</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-20</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">6</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-25</td>
	</tr>
</table>

### 출력
<table style="border-collapse: collapse; width: 50%; margin: 0 auto;">
	<tr>
		<th style="border: 1px solid #000; padding: 10px;">customer_id</th>
		<th style="border: 1px solid #000; padding: 10px;">order_count</th>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">3</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">102</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">103</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">1</td>
	</tr>
</table>
<br>

# **2. HAVING**

GROUP BY로 그룹화된 결과에 대한 필터링을 수행하는 명령어   
WHERE와 비슷하지만 HAVING은 집계된 그룹을 필터링하는 데 사용

## 예시 코드
<code>
SELECT CUSTOMER_ID, COUNT(ORDER_ID) <br>
FROM ORDERS <br>
GROUP BY CUSTOMER_ID <br>
HAVING COUNT(ORDER_ID) >= 2;
</code>

<br>

### 기본 테이블
<table style="border-collapse: collapse; margin: 0 auto;">
	<tr>
		<th style="border: 1px solid #000; padding: 10px;">order_id</th>
		<th style="border: 1px solid #000; padding: 10px;">customer_id</th>
		<th style="border: 1px solid #000; padding: 10px;">order_date</th>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">1</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-05</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">102</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-10</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">3</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-12</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">4</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">103</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-15</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">5</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">102</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-20</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">6</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2023-01-25</td>
	</tr>
</table>

### 출력
<table style="border-collapse: collapse; width: 50%; margin: 0 auto;">
	<tr>
		<th style="border: 1px solid #000; padding: 10px;">customer_id</th>
		<th style="border: 1px solid #000; padding: 10px;">order_count</th>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">101</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">3</td>
	</tr>
	<tr>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">102</td>
		<td style="border: 1px solid #000; padding: 10px; text-align: center;">2</td>
	</tr>
</table>

