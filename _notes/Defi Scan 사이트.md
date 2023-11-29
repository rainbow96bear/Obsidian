# 프로젝트 목표

- Defi Scan 사이트를 통해 사용자들이 수많은 Defi들을 통합하여서 편하게 필터링 할 수 있으며, 한 개의 사이트내에서 수많은 메인넷들의 Defi들을 비교해 볼 수 있기에 편리해진다
- Auto-Compounding vaults 기능으로 수동으로 Claim을 한 후에 다시 Deposit을 하지 않아도 됨으로 굉장히 편리해진다
- 또한 트랜잭션이 일어날 때 마다 일정량의 Scan사이트에서 자체 발행한 Token을 Airdrop 해줌으로써 적절한 보상이 이루어질 수 있다

---

# 기간

2023.04.03 ~ 2023.05.22

---

# 프로젝트 GitHub

[Solar GitHub](https://github.com/rainbow96bear/Solar)

---

# 역할

- Defi 상품 정보를 불러오는 API 처리
- 자체 발행 토큰을 통한 AirDrop 기능
- Swap, Staking을 위한 Smart Contract 작성

---

<br>

# 겪은 문제

---

## 1. API 정보 부족

Beefy사이트가 제공하는 OpenAPI를 활용하려고 하였으나 필요로 하는 정보를 제공하지 않는 문제 발생

### 해결을 위한 시도

1. Beefy 공식 텔레그램을 통하여 필요한 정보를 얻을 수 있는 방법 문의
2. Beefy 이외에 다른 Aggregator 사이트 조사
3. 필요한 정보와 Beefy에서 제공하는 내용을 비교하는 자료를 만들어 보고

### 최종 결론

- API를 통하여 상품을 Staking하기 위해서는 가스 비용의 부담이 높아지는 문제가 있어 API 상품을 소개만 하기로 결정
- Staking과 Swap은 자체 발행 토큰을 통하여 진행하는 것으로 결정

---

## 2. 컨트랙트 배포 오류 발생

토큰을 거래 시 Token을 AirDrop하기 위하여 해당 기능의 Contract를 import하니 오류 발생  
**오류 메세지**  
Contract creation initialization returns data with length of more than 24576 bytes. The deployment will likely fails. More info: eip-170

## 원인

1. EIP-170에 따르면 스마트 컨트랙트의 최대 크기는 24,576 바이트 초과 불가

### 해결 방법

contract를 import하는 것이 아닌 해당 contract의 interface를 생성하여 interface를 import

---

# 결과 이미지

<img src="/assets/Pasted image 20231129155427.png">
<img src="/assets/Pasted image 20231129155451.png">
