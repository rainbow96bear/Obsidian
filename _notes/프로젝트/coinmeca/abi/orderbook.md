# event
- `Ask(address _owner, address _token, uint256 _price, uint256 _amount)`
- `Bid(address _owner, address _token, uint256 _price, uint256 _amount)`
- `Buy(address _owner, address _token, uint256 _price, uint _amount, uint256 _quantity)`
- `Cancel(address _token, uint256 _price, uint256 _amount)`
- `Claim(address _owner, address _token, uint256 _price, uint256 _amount, uint256 _quantity)`
- `Liquidation(address _owner, address _token, uint256 _amount)`
- `Sell(address _owner, address _token, uint256 _price, uint256 _amount, uint256 _quantity)`

# view
- `get_asks(uint16 _range)`
	`-> {uint256 price, uint256 balance}`
- `get_bids(uint16 _range)`
	`-> {uint256 price, uint256 balance}`
- `get_info()`
	`-> {address, address, uint256, uint256, uint8, bool}`
		`base, quote, price, tick, fee, lock이 아닐까 추측`
- `get_nft()`
	`-> {address}`
- `get_orderbook(uint8 _range)`
	`-> { asks{uint256 price, uint256 balance}, bids{uint256 price, uint256 balance} }`