# WINDOW 함수

`OVER` 키워드와 함께 사용되며  역할에 따라 알와 같이 나눌 수있다. 

순위 함수: RANK, DENSE_RANK, ROW_NUMBER  
집계 함수: SUM, MAX, MIN, AVG, COUNT  
행 순서 함수: FIRST_VALUE, LAST_VALUE, LAG, LEAD  
비율 순서 함수: CUME_DIST, PERCENT_RANK, NITLE, RATIO_TO_PERCENT  

## 순위 함수
### RANK
순위를 매기면서 같은 순위가 존재하면 존재하는 수 만큼 다음 순위를 건너 뛴다.  
ex) 1, 2, 2, 4, 5, 5, 7 ,,,  

### DENSE_RANK  
순위를 매기면서 같은 순위가 존재히더라도 다음 순위를 건너뛰지 않고 이어서 매긴다. 
ex) 1, 2, 3, 4, 5, 6, 7, 7, 7, 8

### ROW_NUBER  
순위를 메기면서 동일한 값이라도 각기 다른 순위를 부여한다.  



## 집계 함수
### SUM
### MAX
### MIN
### AVG
### COUNT

## 행 순서 함수

### FIRST_VALUE
파티션 별 가장 선두에 위치한 데이터를 구하는 함수

### LAST_VALUE
파티션 별 가장 끝에 위치한 데이터를 구하는 함수

### LAG
파티션 별로 특정 수 만큼 앞선 데이터를 구하는 함수

### LEAD
파티션 별 특정 수 만큼 뒤에 있는 데이터를 구하는 함수

## 비율 순서 함수
### CUME_DIST 
해당 파티션에서의 누적 백분율을 구하는 함수.  
결과값은 0보다 크고 1보다 작거나 같은 값을 가진다.

### PERCENT_RANK
해당 파티션의 맨 위 끝행을 0, 맨 아래 끝 행을 1로 놓고 현재 행이 위치하는 백분위의 순위값을 구하는 함수

SQL Server의 행 그룹 내에서 행의 상대 순위를 계산합니다. 쿼리 결과 집합 또는 파티션 내에서 값의 상대 순위를 평가하는 데 사용합니다 PERCENT_RANK . PERCENT_RANK는 CUME_DIST 함수와 비슷합니다.

```
PERCENT_RANK( )
    OVER ( [ partition_by_clause ] order_by_clause )
```
### NITLE
주어진 수 만큼 행들을 n등분 한 후 현재 행에 해당하는 등급을 구하는 함수.
할당 행이 남았을 때는 맨 앞의 그룹부터 하나 씩 더 채워진다.(10개의 행이 있는데 3으로 분할 한 경우 첫 번째 그룹에 하나의 행이 더 채워 진다는 의미임)

### RATIO_TO_PERCENT  
파티션 별 합계에서 차지하는 비율을 구하는 함수



## 윈도우 함수 사용 옵션

WINDOWING절을 이용하여 집계하려는 데이터의 범위를 지정할 수 있다. 

### PARTITION BY   
특정 열을 기준으로 데이터를 그룹화합니다.
각 그룹 내에서 WINDOW 함수가 독립적으로 작동합니다.
예시: PARTITION BY department는 부서별로 데이터를 그룹화합니다.

### ORDER BY  
각 그룹 내에서 행의 순서를 지정합니다.
지정된 순서에 따라 WINDOW 함수가 적용됩니다.
예시: ORDER BY salary DESC는 급여를 기준으로 내림차순으로 정렬합니다.


### ROWS BETWEEN 또는 RANGE BETWEEN  
현재 행을 기준으로 WINDOW 함수가 적용될 행의 범위를 지정합니다.
ROWS는 물리적인 행의 개수를 기준으로 하고, RANGE는 값의 범위를 기준으로 합니다.

예시  
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW: 현재 행과 그 이전의 모든 행을 포함합니다.  
RANGE BETWEEN INTERVAL '1' DAY PRECEDING AND CURRENT ROW: 현재 행과 그 전날까지의 행을 포함합니다.  

### UNBOUNDED PRECEDING / UNBOUNDED FOLLOWING  
창의 시작 또는 끝을 무한대로 설정합니다.  
예시: UNBOUNDED PRECEDING는 그룹의 첫 번째 행부터 시작함을 의미합니다.

### CURRENT ROW  
현재 행을 기준으로 함을 나타냅니다.  
예시: ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING는 현재 행부터 그룹의 마지막 행까지 포함합니다.
