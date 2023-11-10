# **1. 계층형 질의**
계층적인 구조를 가진 데이터를 쿼리하는 기술

## 계층 구조 데이터 용어
### 루트 노드
- 계층 구조에서 최상위에 위치한 노드 
### 형제 노드
- 동일한 부모를 가진 노드
### 리프 노드
- 계층 구조에서 말단에 위치한 노드
- 자식 노드가 없는 노드

![[Pasted image 20231110142535.png]]

## 계층형 질의 가상 칼럼
- **LEVEL** : 루트 데이터를 1로 주고 하위로 가면서 1씩 증가
- **CONNECT_BY_LEFT** : 해당 데이터가 리프노드면 1, 그렇지 않으면 0을 출력
- **CONNECT_BY_ISCYCLE** : 순환구조의 경우 1, 그렇지 않으면 0을 출력

## 예시 테이블

<table style="border-collapse: collapse; width: 100%;">
    <tr>
        <th style="border: 1px solid #dddddd; padding: 10px;">employee_id</th>
        <th style="border: 1px solid #dddddd; padding: 10px;">employee_name</th>
        <th style="border: 1px solid #dddddd; padding: 10px;">manager_id</th>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">John</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">null</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">2</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Jane</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">3</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Bob</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">2</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">4</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Alice</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">3</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">5</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Charlie</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">4</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">6</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">David</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">5</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">7</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Eve</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">6</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">8</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Frank</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">7</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">9</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Grace</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">10</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Hank</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">9</td>
    </tr>
</table>

## 예시 코드
<code>
SELECT <br>
  employee_id, <br>
  employee_name, <br>
  manager_id, <br>
  CONNECT_BY_ISCYCLE AS is_cycle <br>
FROM employees <br>
CONNECT BY NOCYCLE PRIOR employee_id = manager_id <br>
START WITH manager_id IS NULL; <br>
</code>

## 출력 

<table style="border-collapse: collapse; width: 100%;">
    <tr>
        <th style="border: 1px solid #dddddd; padding: 10px;">employee_id</th>
        <th style="border: 1px solid #dddddd; padding: 10px;">employee_name</th>
        <th style="border: 1px solid #dddddd; padding: 10px;">manager_id</th>
        <th style="border: 1px solid #dddddd; padding: 10px;">is_cycle</th>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">John</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">null</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">2</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Jane</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">3</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Bob</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">2</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">4</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Alice</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">3</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">5</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Charlie</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">4</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">6</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">David</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">5</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">7</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Eve</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">6</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">8</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Frank</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">7</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">9</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Grace</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">1</td>
    </tr>
    <tr>
        <td style="border: 1px solid #dddddd; padding: 10px;">10</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">Hank</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">9</td>
        <td style="border: 1px solid #dddddd; padding: 10px;">0</td>
    </tr>
</table>


# **2. SELF JOIN**
하나의 테이블 내에서 자체적으로 JOIN을 수행하는 경우   
테이블 내에 저장된 데이터 간의 관계를 다룰 때 유용   

## 예시 테이블
![[Pasted image 20231110135013.png]]
![[Pasted image 20231110135013.png]]

## 예시 코드
<code>
SELECT <br>
E.EMPLOYEE_ID, <br>
E.NAME E_NAME, <br>
E.MANAGER_ID '매니저', <br>
M.MANAGER_ID '매니저의 매니저' <br>
FROM ETABLE AS E <br>
JOIN ETABLE AS M ON E.MANAGER_ID = M.EMPLOYEE_ID;
</code>

## 출력 
![[Pasted image 20231110145533.png]]
