GROUP BY를 사용할 때 집계 함수를 사용하여 그룹 단위로 데이터를 집계할 수 있습니다. 이러한 함수를 GROUP FUNCTION이라 부르기도 합니다.

## 예시 테이블

<img src="/assets/Pasted image 20231109120430.png">
<br>


# **1. ROLLUP**
그룹의 조건을 추가하며 집계를 구하는 방식

## 예시 코드
<code>
SELECT DEPARTMENT, JOB, SUM(SALARY) AS TotalAmount
FROM EMPLOYEES
GROUP BY ROLLUP(DEPARTMENT, JOB)
</code>

<img src="/assets/Pasted image 20231109121335.png">
<br>
### MySQL 코드
<code>
SELECT  <br>
DEPARTMENT, JOB, SUM(SALARY) AS TotalAmount <br>
FROM employees <br>
GROUP BY DEPARTMENT, JOB WITH ROLLUP;
</code>

<br>

# **2. CUBE**
조합 가능한 모든 그룹에 대하여 집계를 구하는 방식

## 예시 코드
<code>
SELECT <br>
DEPARTMENT, JOB, SUM(SALARY) AS TotalAmount <br>
FROM EMPLOYEES <br>
GROUP BY CUBE(DEPARTMENT, JOB)
</code>


<img src="/assets/Pasted image 20231109121840.png">
<br>

### MySQL 코드
<code>
SELECT <br>
    CASE WHEN GROUPING(DEPARTMENT) = 1 THEN NULL  <br>
    ELSE DEPARTMENT END AS DEPARTMENT,
    <br>
    CASE WHEN GROUPING(job) = 1 THEN NULL ELSE job  <br>
    END AS job, 
    <br>
    SUM(SALARY) AS TotalSalary  <br>
FROM EMPLOYEES  <br>
GROUP BY DEPARTMENT, job WITH ROLLUP  <br>
HAVING GROUPING(DEPARTMENT) = 0 OR GROUPING(JOB) = 0  <br>
union  <br>
SELECT DEPARTMENT, job, SUM(SALARY)  <br>
FROM EMPLOYEES <br>
GROUP BY job, DEPARTMENT WITH ROLLUP;
</code>

<br>


# **3. GROUPING SETS**
지정한 그룹에 대하여 집계를 구하는 방식

## 예시 코드
<code>
SELECT <br>
DEPARTMENT, JOB, SUM(SALARY) AS TotalAmount <br>
FROM EMPLOYEES <br>
GROUP BY GROUPING SETS 
(DEPARTMENT, JOB)
</code>



<img src="/assets/Pasted image 20231109120233.png">


### MySQL 코드
<code>
SELECT <br>
COALESCE(DEPARTMENT, 'Total') AS DEPARTMENT,   <br>
COALESCE(JOB, 'Total') AS JOB , SUM(SALARY)  <br>
FROM EMPLOYEES  <br>
GROUP BY DEPARTMENT, JOB;
</code>

