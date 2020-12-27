# TechFlare External Adapter 
External Adapter for Chainlink to query the TechFlare API.
This adapter hasn't been yet open in chainlink market.


To give TechFlare API own description:
> TechFlare collects and aggregates precise and reliable information from multiple sources in web. It provides financial data and technical indicators in the decentralized oracle Chainlink. Our success is driven by our futuristic mind and a disciplined focus on democratizing access to data.

### Contract Usage
To use this adapter on-chain, find a node that supports this adapter and build your request like so:
```
Chainlink.Request memory request = buildChainlinkRequest(jobId, this, this.fulfill.selector);
run.add("n", "btc");
run.add("p", "m");
string[] memory copyPath = new string[](2);
copyPath[0] = "disparity";
copyPath[1] = "5";
request.addStringArray("copyPath", path);
int timesAmount = 10**18;
request.addInt("times", timesAmount);
```

### Usage
Pass parameters a symbol of token `n` and a period of ohlc data `p`.

Supported tokens
```
btc
eth
ltc
bch
ada
bnb
dot
link
```
 
Supported periods
```
m
h
d
```
 

```
curl -X POST -H 'Content-Type: application/json' \
-d @- << EOF
{
    "jobRunId": "1",
    "data": {
        "n": "btc",
        "p": "m"
    }
}
EOF
```
Response:
```json
{
    "jobRunId": "1",
    "data": {
        "name": "btc",
        "std": {"5": 72.69628786962369, "20": 603.850574126043, "3": 76.30369781353097},
        "momentum": {"5": 6.5, "20": 1693.7599999999984, "3": 68.2599999999984},
        "sma": {"5": 23109.73200000001, "20": 22955.602000000003, "3": 23147.51666666668},
        "ema": {"5": 27820.245474540803, "20": 27501.09968838345, "3": 27855.8362013757},
        "disparity": {"5": 1.0008787639770116, "20": 1.0040799627036572, "3": 0.9992449874032557},
        "return": {"5": 0.007453312263817402, "20": 0.012471145842255948, "3": 0.0024148057234190112}
    },
    "statusCode": 200
}
```
