# exchange
```go
// 최근 거래 기록
type RecentTrades struct {
	Type int64
	Symbol string
	From string
	Address string
	Time string
	Amount string
	Quantity string
}
```

# market
```go
type Market struct {
	Address string
	Base string
	Quote string
	Name string
	Symbol string
	Price float64
	Change float64
	Change float64
	High float64
	Low float64
	//Volume 
	//Asks []Tick
	//Bids []Tick
	//Chart
	//Last
	Tick float64 
	//Recent []MarketRecent
}

type Tick struct {
	Price float64
	Balance float64
}

type MarketRecent struct {
	Time int64
	Price float64
	Balance float64
}
```