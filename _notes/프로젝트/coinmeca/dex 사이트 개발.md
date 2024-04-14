기간 : 2024.04.06 ~ 진행중

참여 계기 : 오픈 카톡방에서 golang기반 백엔드 구축 인원을 모집하여 개발 실력을 확인하고자 참가
<img src="/assets/Pasted image 20240407211647.png">

맞은 역할 : gRPC server에서 crawling 된 자료를 분류하여 graphql에 전달하는 작업   

백엔드 플로우 : <img src="/assets/Pasted image 20240410114930.png">

flow : Buy 또는 Sell tx 확인 -> contract의 get_orderbook call하여 정보 받기 -> for문으로 orderbook마다 asks와 bids를 api-server에 전달 + chart 정보 전달

필요한 작업 :
- api-server : AddData switch case 추가 (Buy, Sell 등에 대한 정보 처리용)
- high와 low에 대한 정보 처리 방법
# ABI
- [[vault]]
- [[orderbook]]
- [[market]]
- [[farm]]
# API
거래 정보를 client에 전달하기 위한 graphQL API
- [[API]]
# Event struct
Buy와 Sell 요청에 담겨있는 event 값 ABI - [[orderbook]]의 Buy, Sell, Ask, Bid
- [[Event Struct]]
# dao
crawling한 정보를 DB에 저장 및 graphQL로 전달하기 위한 dao
- [[dao]]

