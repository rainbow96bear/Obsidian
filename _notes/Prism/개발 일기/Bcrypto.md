# bcrypto란?
레인포우 테이블 공격 방지를 위해 솔트를 통합한 bcrypt는 적응형 함수의 하나   
시간이 지남에 따라 속도 저하를 위해 반복 횟수가 증가가 수반될 수 있으므로 연산 파워의 증가에도 브루트 포스 검색 공격에 대한 저항을 유지

## 예시

$2a\$10\$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy

2a : 해시 알고리즘 식별자   
10 : Cost Factor   
N9qo8uLOickgx2ZMRZoMye : 16바이트 솔트   
IjZAgcfl7p92ldGxad68LJZdL17lhWy : 24바이트 해시   

# bcrypto 작동 원리

암호화 하고 싶은 자료와 솔트를 합쳐 해시 함수를 통하여 해시화 합니다.   
Cost Factor의 수만큼 반복합니다. (2^Cost Factor)

## 예시

1. 0000을 솔트와 연결 => 0000N9qo8uLOickgx2ZMRZoMye
2. Cost Factor 만큼 해시 작업을 반복 (2^Cost Factor)
3. 사용한 해시 알고리즘, Cost Factor, 솔트, 해시 결과를 합쳐서 출력 => $2a\$10\$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy