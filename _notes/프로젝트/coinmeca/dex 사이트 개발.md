server : **Golang**
DB : **mongoDB**

기간 : 2024.04.06 ~ 진행중

참여 계기 : 오픈 카톡방에서 golang기반 백엔드 구축 인원을 모집하여 개발 실력을 확인하고자 참가
<img src="/assets/Pasted image 20240407211647.png">

맡은 역할 : 블록 스캔하여 crawling 된 자료를 이벤트에 따라 분류하여 오더북 최신화 및 차트를 생성   

백엔드 플로우 : <img src="/assets/Pasted image 20240410114930.png">

flow : Buy 또는 Sell tx 확인 -> contract의 get_orderbook call하여 정보 받기 -> orderbook마다 asks와 bids를 api-server에 전달 + chart 정보 전달


# mongoDB aggregate
```go
pipeline := []bson.M{
	{
		"$match": bson.M{
			"symbol": "BTC-USD",
		},
	},
	{
		"$group": bson.M{
			"_id": bson.M{
				"symbol": "$symbol", "time": bson.M{
					"$dateTrunc": bson.M{
						"date": "$time",
						"unit": "minute",
						"binSize": 5,
					},
				},
			},
			"high": bson.M{"$max": "$price"},
			"low": bson.M{"$min": "$price"},
			"open": bson.M{"$first": "$price"},
			"close": bson.M{"$last": "$price"},
		},
	},
	{
		"$sort": bson.M{"_id.time": 1},
	},
}
```

# 옵션
- $match - aggregate하려는 자료 구분 (filter의 역할)   
- $group - 출력할 내용을 정의
- $dateTrunc - 날짜 필드의 값을 특정 단위로 정리
- date - 날짜를 구별할 필드 지정
- unit, binSize - $dateTrunc 계산에 사용되는 기간을 지정
- $first - 그룹 내에서 가장 먼저 나오는 문서의 필드 값
- $last - 그룹 내에서 가장 나중에 나오는 문서의 필드 값
- $sort - 문서 정렬 방식