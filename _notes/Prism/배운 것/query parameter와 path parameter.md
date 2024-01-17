# 목차
1. path Parameter
2. Query Parameter

-----

# path Parameter
특정 리소스를 가리키는 URI의 역할

## ex)
- GET /products : 상품들의 정보를 조회
- GET /products/1 : 1번 상품의 정보를 조회
- POST /products/1 : 1번 상품의 정보를 수정


-----

# Query Parameter
Query parameter는 HTTP의 GET, DELETE 요청에서만 사용하고 유일 값을 식별하기 위한 용도가 아닌 옵션을 줄 때 사용

- 데이터 필터링
- 데이터 정렬
- 검색 등

## ex)
- GET /products?price=3000 : 상품들 중 가격이 3000인 상품들을 조회

-----

# 참고 자료
- https://velog.io/@juno97/API-Path-parameter-VS-Query-Parameter-%EA%B8%B0%EB%A1%9D%EC%9A%A9