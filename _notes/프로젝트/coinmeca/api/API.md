```go
// Recent trades 최근 거래 기록
type MarketRecent {
	time: Int!
	price: Float!
	balance: Float!
}

// chart와 orderbook의 호가창 관련 정보
type MarketLast {
	asks: [Ticks]
	bibs: [Ticks]
	chart: MarketChart
	volume: [MarketVolume]
}

//chart에 대한 정보 최신화
type MarketChartPrice {
	time: Int!
	open: Int!
	high: Int!
	low: Int!
	close: Int!
}
```