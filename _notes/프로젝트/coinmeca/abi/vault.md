# event
- `Deposit(address _address, address _token, uint256 _amount, uint256 _meca)`
- `Fee(uint256 fee)`
- `Listing(address _token, uint256 _quantity, uint256 _proof)`
- `Reward(uint256 reward)`
- `Withdraw(address _address, address _token, uint256 _amount, uint256 _meca)`
- `_Deposit(uint256 amount, uint256 quantity, uint256 proof)`
# view
- `get_all()`
	`-> {bool key, address addr, string name, string symbol, uint8 decimals, uint256 treasury, uint256 rate, uint256 weight, int256 need}`
- `get_key_tokens()`
	`->{bool key, address addr, string name, string symbol, uint8 decimals, uint256 treasury, uint256 rate, uint256 weight, int256 need}`
- `get_liquidity(address _base, address _quote)`
	`-> {uint256 l}`
- `get_tokens()`
	`->{bool key, address addr, string name, string symbol, uint8 decimals, uint256 treasury, uint256 rate, uint256 weight, int256 need}`


