```go
type EventAsk struct {
	Owner common.Address
	Token common.Address
	Price *big.Int
	Amount *big.Int
}

type EventBid struct {
	Owner common.Address
	Token common.Address
	Price *bigInt
	Amount *big.Int
}

type EventBuy struct {
	Owner common.Address
	Token common.Address
	Price *bigInt
	Amount *big.Int
	Quantity *big.Int
}

type EventSell struct {
	Owner common.Address
	Token common.Address
	Price *bigInt
	Amount *big.Int
	Quantity *big.Int
}
```