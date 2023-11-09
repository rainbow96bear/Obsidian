결과 집합을 작은 부분 집합으로 나누고 각 부분집합에 대하여 원하는 집계를 보여주는 명령어

## 예시 테이블
<img src="/assets/Pasted image 20231109120430.png">

# **1. PARTITION BY**
GROUP BY 처럼 OVER의 출력에 대하여 그룹을 지정하는 방법

## 예시 코드
<code>
SELECT <br>
  DEPARTMENT, JOB,  AVG(SALARY) OVER (PARTITION BY JOB),  <br>
  COUNT(*) OVER (PARTITION BY JOB) <br>
FROM EMPLOYEES;
</code>

<img src="/assets/Pasted image 20231109151749.png">
<br>

# **2. ORDER BY**
OVER의 출력에 대하여 누적 합계형식으로 출력하는 방법

## 예시 코드
<code>
SELECT <br>
  DEPARTMENT, JOB,  AVG(SALARY) OVER (PARTITION BY JOB, ORDER BY EMPLOYEE_ID), <br>
  COUNT(*) OVER (PARTITION BY JOB, ORDER BY EMPLOYEE_ID) <br>
FROM EMPLOYEES;
</code>

<img src="/assets/Pasted image 20231109152011.png">