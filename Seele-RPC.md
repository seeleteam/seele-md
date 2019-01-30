# Seele JSON-RPC
JSON is a lightweight data exchange format. It can represent numbers, strings, ordered value sequences and key-value pairs.

JSON-RPC is a stateless, lightweight Remote Procedure Call (RPC) protocol. It defines several data structures and the relevant rules to handle them. JSON-RPC is transmission-agnostic, because it can be used in situations like process, socket, HTTP, or different message transmission environments. It uses JSON(RFC 4627) as the data format.

## Curl Examples Explained
The curl options below might return a response where the node complains about the content type, this is because the --data option sets the content type to application/x-www-form-urlencoded . If your node does complain, manually set the header by placing -H "Content-Type: application/json" at the start of the call.


## JSON-RPC Support
| Type | Supported? |
|-------|:------------:|
| JSON-RPC 1.0 | &#x2713; |
| JSON-RPC 2.0 | &#x2713; |
| Batch Requests | &#x2713; |
| HTTP | &#x2713; |
| WS | &#x2713; |

## JSON-RPC Port
Default port:

| Client | Type | Address |
|-------|-------|:------------|
| Go | jsonrpc-2.0 |http://localhost:8027 |
| Go | http |http://localhost:8037 |
| Go | websocket |http://localhost:8047 |

## JSON-RPC List
Currently, there are several RPCs with different namespaces：
- `seele`:node data manipulation and procurement / acquisition
- `txpool`:transaction pool management
- `download`:RPC collection provided for internal inquiry of blockchain node synchronization state.
- `network`:connection management
- `miner`:miner manipulation
- `debug`:node debugging
- `monitor`:node monitor

## JSON-RPC Contents
- [seele](#seele)

| Command | Full | Light | public | private |
|-------|:-------:|:-------:|:-------:|:-------:|
|[GetInfo](#getinfo)| &#x2713; || &#x2713; ||
|[GetBalance](#getbalance)| &#x2713; | &#x2713; | &#x2713; ||
|[AddTx](#addtx)| &#x2713; | &#x2713; | &#x2713; ||
|[GetAccountNonce](#getaccountnonce)| &#x2713; | &#x2713; | &#x2713; ||
|[GetBlockHeight](#getblockheight)| &#x2713; | &#x2713; | &#x2713; ||
|[GetBlock](#getblock)| &#x2713; | &#x2713; | &#x2713; ||
|[GetBlockByHash](#getblockbyhash)| &#x2713; | &#x2713; | &#x2713; ||
|[GetBlockByHeight](#getblockbyheight)| &#x2713; | &#x2713; | &#x2713; ||
|[Call](#call)| &#x2713; || &#x2713; ||
|GetLogs(Being Written)| &#x2713; || &#x2713; ||
|[GeneratePayload](#generatepayload)| &#x2713; || &#x2713; ||
|[EstimateGas](#estimategas)| &#x2713; || &#x2713; ||

- [txpool](#txpool)

| Command | Full | Light | public | private |
|-------------------------------|:-------:|:-------:|:-------:|:-------:|
|[GetBlockTransactionCount](#getblocktransactioncount)| &#x2713; | &#x2713; | &#x2713; ||
|[GetBlockTransactionCountByHeight](#getblockTransactioncountbyheight)| &#x2713; | &#x2713; | &#x2713; ||
|[GetBlockTransactionCountByHash](#getBlockTransactionCountByHash)| &#x2713; | &#x2713; | &#x2713; ||
|[GetTransactionByBlockIndex](#getTransactionbyblockindex)| &#x2713; | &#x2713; | &#x2713; ||
|[GetTransactionByBlockHeightAndIndex](#getTransactionbyblockheightandindex)| &#x2713; | &#x2713; | &#x2713; ||
|[GetTransactionByBlockHashAndIndex](#getTransactionbyblockhashandindex)| &#x2713; | &#x2713; | &#x2713; ||
|[GetReceiptByTxHash](#getreceiptbytxhash)| &#x2713; | &#x2713; | &#x2713; ||
|[GetTransactionByHash](#getTransactionbyhash)| &#x2713; | &#x2713; | &#x2713; ||
|[GetDebtByHash](#getdebtbyhash)| &#x2713; ||| &#x2713; |

- [download](#download)

| Command | Full | Light | public | private |
|-------------|:-------:|:-------:|:-------:|:-------:|
|[GetStatus](#getstatus)| &#x2713; ||| &#x2713; |

- [network](#network)

| Command | Full | Light | public | private |
|---------------------------|:-------:|:-------:|:-------:|:-------:|
|[GetPeersInfo](#getpeersinfo)| &#x2713; | &#x2713; || &#x2713; |
|[GetPeerCount](#getpeercount)| &#x2713; | &#x2713; || &#x2713; |
|[GetNetVersion](#getnetversion)| &#x2713; | &#x2713; || &#x2713; |
|[GetProtocolVersion](#getprotocolversion)| &#x2713; | &#x2713; || &#x2713; |
|[GetNetworkID](#getnetworkid)| &#x2713; | &#x2713; || &#x2713; |

- [miner](#miner)

| Command | Full | Light | public | private |
|-------|:-------:|:-------:|:-------:|:-------:|
|[Start](#start)| &#x2713; ||| &#x2713; |
|[Stop](#stop)| &#x2713; ||| &#x2713; |
|[Status](#status)| &#x2713; ||| &#x2713; |
|[GetCoinbase](#getcoinbase)| &#x2713; ||| &#x2713; |
|[SetThreads](#setthreads)| &#x2713; ||| &#x2713; |
|[SetCoinbase](#setcoinbase)| &#x2713; ||| &#x2713; |
|[GetEngineInfo](#getengineinfo)| &#x2713; ||| &#x2713; |

- [debug](#debug)

| Command | Full | Light | public | private |
|-----------------------------|:-------:|:-------:|:-------:|:-------:|
|[PrintBlock](#printblock)| &#x2713; ||| &#x2713; |
|[GetTxPoolContent](#gettxpoolcontent)| &#x2713; | &#x2713; || &#x2713; |
|[GetTxPoolTxCount](#gettxpooltxcount)| &#x2713; | &#x2713; || &#x2713; |
|[GetPendingTxs](#getpendingtxs)| &#x2713; | &#x2713; || &#x2713; |
|[GetPendingDebts](#getpendingdebts)| &#x2713; ||| &#x2713; |
|[DumpHeap](#dumpheap)| &#x2713; ||| &#x2713; |
|[GetTPS](#gettps)| &#x2713; ||| &#x2713; |

- [monitor](#monitor)

| Command | Full | Light | public | private |
|-----------------|:-------:|:-------:|:-------:|:-------:|
|[NodeInfo](#nodeinfo)| &#x2713; || &#x2713; ||
|[NodeStats](#nodestats)| &#x2713; || &#x2713; ||

### seele
RPC collection provided for public for blockchain node and transaction manipulation.

***

#### GetInfo

This method returns the node information.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getInfo","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `Coinbase`:`string` - node address
- `CurrentBlockHeight`:`uint64` - current block height
- `HeaderHash`:`string` - block hash
- `MinerStatus`:`string` - miner status
- `Shard`:`int` - shard number

##### Example
```js
// Request
curl  -X POST --data '{"jsonrpc":"2.0","method":"seele_getInfo","params":[],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "Coinbase": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
        "CurrentBlockHeight": 1722,
        "HeaderHash": "0x000001fa4cb11751fea2d4f7f9356303d44d2a02f37c3e62e657ffe29e5cb5fe",
        "Shard": 1,
        "MinerStatus": "Running"
    }
}
```
***

#### GetBalance

This method returns the account balance give the account address.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getBalance","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `Account`:`string` - account
- `hexHash`:`string` - hex form of a block hash, set to "" for the latest balance
- `height` :`uint64` - height of a block, set to -1 for the latest balance
##### Returns

- `Account`:`string` - account
- `Balance`:`big.Int` - account balance

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_getBalance","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","",-1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "Account": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
        "Balance": 265499990000
    }
}
```
***

#### AddTx

This method submits a transaction to the node.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_addTx","params":[types.Transaction],"id":1}` |

##### Parameters

- `tx`:`types.Transaction` - transaction struct (client command `sign` could be used to get transaction hash and signature)
  - `Hash`:`string` - transaction hash
  - `Data`:`json` - transaction data
    - `From`:`string` - transaction sender
    - `To`:`string` - transaction receiver
    - `Amount`:`uint64` - amount value, unit is fan
    - `Fee`:`uint64` - transaction fee
    - `Payload`:`string` - transaction payload
    - `AccountNonce`:`uint64` - transaction nonce
  - `Signature` : `crypto.Signature` - transaction signature struct
   ```
  type Signature struct {
	   Sig []byte // [R || S || V] format signature in 65 bytes.
  }
  ```

##### Returns

- `result`:`bool` - transaction send result

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_addTx","params":[{"Hash": "0x3393e5566cb905d714599f2f888ecc6d223b83403887460fa5b2771e89a0436e","Data": {"From": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21","To":"0x2a87b6504cd00af95a83b9887112016a2a991cf1","Amount": 1,"AccountNonce":0,"Fee": 0,"GasPrice":10, "GasLimit":21000},"Signature":{"Sig":"fAvgVTXDyJZbfv07NYBK4aSolfY4ycBPQRwnQFpHRMc7ooOZw27U50o4TBoRelYX3QCRyvKpbxVlxhu7AnSB6QE="}}],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": true
}
```
***

#### GetAccountNonce

This method is used to obtain the account nonce.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getAccountNonce","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - account
- `hexHash`:`string` - hex form of a block hash, set to "" for the latest nonce
- `height` :`uint64` - height of a block, set to -1 for the latest nonce
##### Returns

- `result`:`uint64` - account nonce

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_getAccountNonce","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","",-1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 3
}
```
***

#### GetBlockHeight

This method is used to obtain the height of the blockchain.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getBlockHeight","params":[string],"id":1}` |

##### Parameters

none

##### Returns

- `result`:`uint64` - block height

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockHeight","params":[],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 1928
}
```
***

#### GetBlock

This method is used to obtain the block content based on block height or block hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getBlock","params":[string,string,bool],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `height`:`string` - block height
- `fulltx, f`:`bool` - whether to include detailed transaction information

##### Returns

- `debts`:`array` - debts in block
- `Hash`:`string` - debts hash
- `Data`:`json` - debts data
- `TxHash`:`string` - txhash in debt
- `Shard`:`int` - shard number of seele node where debts on
- `Account`:`array` - debt account
- `Amount`:`int64` - debt amount
- `Fee`:`int64` - debt fee
- `Code`:`string` - debt code
- `hash`:`string` - block hash
- `header`:`json` - block header
- `CreateTimestamp`:`uint64` - create timestamp
- `Creator`:`string` - creator address
- `DebtHash`:`string` - debts hash
- `Difficulty`:`big.Int` - block difficulty
- `ExtraData`:`string` - extra data
- `Height`:`unit64` - block height
- `Nonce`:`unit64` - block nonce
- `PreviousBlockHash`:`string` - previous block hash
- `ReceiptHash`:`string` - Receipts hash
- `stateHash`:`string` - state tree hash
- `TxDebtHash`:`string` - debts hash
- `TxHash`:`string` - tx hash
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`big.Int` - timestamp
- `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
- `Data`:`json` - txDebts data
- `Account`:`string` - transaction account
- `Amount`:`int` - transaction amount
- `Code`:`string` - transaction code
- `Fee`:`int` - transaction fee
- `Shard`:`int` - transaction shard number
- `TxHash`:`string` - transaction hash
- `Hash`:`string` - txDebts hash

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlock","params":["",10368,true],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [
            {
                "Hash": "0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e",
                "Data": {
                    "TxHash": "0x58752f8aeb2c69dd2c32059d3ad8b2d3d860c6d92aa2b3b30ff985e564f60fae",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ],
        "hash": "0x000002069d9de64bad509239e2a121afbf7de183576457a1d1fb077d19fa3e8c",
        "header": {
            "PreviousBlockHash": "0x000001cba2c0b82402b3d2d2ad49f50ca0b21aee18c8123486377b2ec93aa0e0",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0x8af14975f636ace27571cfcdcd9a1a1b4a5b15228977cf6207e82f63abf96ffd",
            "TxHash": "0xdb00575ff0cc0de89bd6c1799d37e5f600687963785176ca76e81bebfde6a03f",
            "ReceiptHash": "0x02fa1d68e7bbf0b833f6e8719efb11b32c7f760e4ae050a4f9b58b8dd8ad1620",
            "TxDebtHash": "0x58d7c36b25a715f5076ccb878940920f6bb333ab142287452509f881103960d2",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 6563003,
            "Height": 10368,
            "CreateTimestamp": 1539050098,
            "Nonce": 17825487295277268182,
            "ExtraData": ""
        },
        "totalDifficulty": 68985339754,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 150000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x6fb17b265260caed33b4e8f58ad84b508dd8950b9bc93dae8518fc96912f76bb",
                "payload": "",
                "timestamp": 1539931510,
                "to": "0xd5a145191b7ca9cb4f3dc850e426c1e853d2a9f1"
            },
            {
                "accountNonce": 280,
                "amount": 10000,
                "from": "0xec759db47a65f6537d630517f6cd3ca39c6f93d1",
                "gasLimit": 21000,
                "gasPrice": 1,
                "hash": "0xf526dc404145cd409601e951fec4f2222f3abf578381cdaaea9db3a791a79cbd",
                "payload": "",
                "timestamp": 0,
                "to": "0xa00d22dc3624d4696eff8d1641b442f79c3379b1"
            }
        ],
        "txDebts": [
            {
                "Hash": "0xe1c24a636a7c27aea7c384f6eb61eb49168129105f4c081ffa8ca7e77198b3f6",
                "Data": {
                    "TxHash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ]
    }
}
```
***

#### GetBlockByHash

This method is used to obtain the block content based on block hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getBlockByHash","params":[string,bool],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `fulltx, f`:`bool` - whether to include detailed transaction information

##### Returns

- `debts`:`array` - debts in block
- `Hash`:`string` - debts hash
- `Data`:`json` - debts data
- `TxHash`:`string` - txhash in debt
- `Shard`:`int` - shard number of seele node where debts on
- `Account`:`array` - debt account
- `Amount`:`int64` - debt amount
- `Fee`:`int64` - debt fee
- `Code`:`string` - debt code
- `hash`:`string` - block hash
- `header`:`json` - block header
- `CreateTimestamp`:`uint64` - create timestamp
- `Creator`:`string` - creator address
- `DebtHash`:`string` - debts hash
- `Difficulty`:`big.Int` - block difficulty
- `ExtraData`:`string` - extra data
- `Height`:`unit64` - block height
- `Nonce`:`unit64` - block nonce
- `PreviousBlockHash`:`string` - previous block hash
- `ReceiptHash`:`string` - Receipts hash
- `stateHash`:`string` - state tree hash
- `TxDebtHash`:`string` - debts hash
- `TxHash`:`string` - tx hash
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`big.Int` - timestamp
- `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
- `Data`:`json` - txDebts data
- `Account`:`string` - transaction account
- `Amount`:`int` - transaction amount
- `Code`:`string` - transaction code
- `Fee`:`int` - transaction fee
- `Shard`:`int` - transaction shard number
- `TxHash`:`string` - transaction hash
- `Hash`:`string` - txDebts hash

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockByHash","params":["0x000002069d9de64bad509239e2a121afbf7de183576457a1d1fb077d19fa3e8c",true],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [
            {
                "Hash": "0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e",
                "Data": {
                    "TxHash": "0x58752f8aeb2c69dd2c32059d3ad8b2d3d860c6d92aa2b3b30ff985e564f60fae",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ],
        "hash": "0x000002069d9de64bad509239e2a121afbf7de183576457a1d1fb077d19fa3e8c",
        "header": {
            "PreviousBlockHash": "0x000001cba2c0b82402b3d2d2ad49f50ca0b21aee18c8123486377b2ec93aa0e0",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0x8af14975f636ace27571cfcdcd9a1a1b4a5b15228977cf6207e82f63abf96ffd",
            "TxHash": "0xdb00575ff0cc0de89bd6c1799d37e5f600687963785176ca76e81bebfde6a03f",
            "ReceiptHash": "0x02fa1d68e7bbf0b833f6e8719efb11b32c7f760e4ae050a4f9b58b8dd8ad1620",
            "TxDebtHash": "0x58d7c36b25a715f5076ccb878940920f6bb333ab142287452509f881103960d2",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 6563003,
            "Height": 10368,
            "CreateTimestamp": 1539050098,
            "Nonce": 17825487295277268182,
            "ExtraData": ""
        },
        "totalDifficulty": 68985339754,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 150000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x6fb17b265260caed33b4e8f58ad84b508dd8950b9bc93dae8518fc96912f76bb",
                "payload": "",
                "timestamp": 1539931510,
                "to": "0xd5a145191b7ca9cb4f3dc850e426c1e853d2a9f1"
            },
            {
                "accountNonce": 280,
                "amount": 10000,
                "from": "0xec759db47a65f6537d630517f6cd3ca39c6f93d1",
                "gasLimit": 21000,
                "gasPrice": 1,
                "hash": "0xf526dc404145cd409601e951fec4f2222f3abf578381cdaaea9db3a791a79cbd",
                "payload": "",
                "timestamp": 0,
                "to": "0xa00d22dc3624d4696eff8d1641b442f79c3379b1"
            }
        ],
        "txDebts": [
            {
                "Hash": "0xe1c24a636a7c27aea7c384f6eb61eb49168129105f4c081ffa8ca7e77198b3f6",
                "Data": {
                    "TxHash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ]
    }
}
```
***

#### GetBlockByHeight

This method is used to obtain the block content based on block height.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getBlockByHeight","params":[string,bool],"id":1}` |

##### Parameters

- `height`:`string` - block height
- `fulltx, f`:`bool` - whether to include detailed transaction information

##### Returns

- `debts`:`array` - debts in block
- `Hash`:`string` - debts hash
- `Data`:`json` - debts data
- `TxHash`:`string` - txhash in debt
- `Shard`:`int` - shard number of seele node where debts on
- `Account`:`array` - debt account
- `Amount`:`int64` - debt amount
- `Fee`:`int64` - debt fee
- `Code`:`string` - debt code
- `hash`:`string` - block hash
- `header`:`json` - block header
- `CreateTimestamp`:`uint64` - create timestamp
- `Creator`:`string` - creator address
- `DebtHash`:`string` - debts hash
- `Difficulty`:`big.Int` - block difficulty
- `ExtraData`:`string` - extra data
- `Height`:`unit64` - block height
- `Nonce`:`unit64` - block nonce
- `PreviousBlockHash`:`string` - previous block hash
- `ReceiptHash`:`string` - Receipts hash
- `stateHash`:`string` - state tree hash
- `TxDebtHash`:`string` - debts hash
- `TxHash`:`string` - tx hash
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`big.Int` - timestamp
- `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
- `Data`:`json` - txDebts data
- `Account`:`string` - transaction account
- `Amount`:`int` - transaction amount
- `Code`:`string` - transaction code
- `Fee`:`int` - transaction fee
- `Shard`:`int` - transaction shard number
- `TxHash`:`string` - transaction hash
- `Hash`:`string` - txDebts hash

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockByHeight","params":[10368,true],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [
            {
                "Hash": "0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e",
                "Data": {
                    "TxHash": "0x58752f8aeb2c69dd2c32059d3ad8b2d3d860c6d92aa2b3b30ff985e564f60fae",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ],
        "hash": "0x000002069d9de64bad509239e2a121afbf7de183576457a1d1fb077d19fa3e8c",
        "header": {
            "PreviousBlockHash": "0x000001cba2c0b82402b3d2d2ad49f50ca0b21aee18c8123486377b2ec93aa0e0",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0x8af14975f636ace27571cfcdcd9a1a1b4a5b15228977cf6207e82f63abf96ffd",
            "TxHash": "0xdb00575ff0cc0de89bd6c1799d37e5f600687963785176ca76e81bebfde6a03f",
            "ReceiptHash": "0x02fa1d68e7bbf0b833f6e8719efb11b32c7f760e4ae050a4f9b58b8dd8ad1620",
            "TxDebtHash": "0x58d7c36b25a715f5076ccb878940920f6bb333ab142287452509f881103960d2",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 6563003,
            "Height": 10368,
            "CreateTimestamp": 1539050098,
            "Nonce": 17825487295277268182,
            "ExtraData": ""
        },
        "totalDifficulty": 68985339754,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 150000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x6fb17b265260caed33b4e8f58ad84b508dd8950b9bc93dae8518fc96912f76bb",
                "payload": "",
                "timestamp": 1539931510,
                "to": "0xd5a145191b7ca9cb4f3dc850e426c1e853d2a9f1"
            },
            {
                "accountNonce": 280,
                "amount": 10000,
                "from": "0xec759db47a65f6537d630517f6cd3ca39c6f93d1",
                "gasLimit": 21000,
                "gasPrice": 1,
                "hash": "0xf526dc404145cd409601e951fec4f2222f3abf578381cdaaea9db3a791a79cbd",
                "payload": "",
                "timestamp": 0,
                "to": "0xa00d22dc3624d4696eff8d1641b442f79c3379b1"
            }
        ],
        "txDebts": [
            {
                "Hash": "0xe1c24a636a7c27aea7c384f6eb61eb49168129105f4c081ffa8ca7e77198b3f6",
                "Data": {
                    "TxHash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ]
    }
}
```
***

#### Call

This method is used to execute a given transaction on a statedb of a given block height. It does not affect the statedb or blockchain and is useful for executing and retrieving values. However, the height currently does not support optional and will remove the from parameter in the next version or more.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_call ","params":[CallRequest],"id":1}` |

##### Parameters

- `to`:`string` - to address
- `payload`:`string` - transaction payload info
- `Height`:`int64` - block height (default: -1)

##### Returns

- `contract`:`string` - contract address
- `failed`:`bool` - contract executes successfully or not
- `poststate`:`string` - state trie root hash after transaction execution
- `result`:`string` - transaction result
- `totalFee`:`int64` - transaction fee
- `txhash`:`string` - transaction hash
- `usedGas`:`int64` - transaction gas

##### Example
When using the example below, the contract must be deployed first. The solidity code file:
```
pragma solidity ^0.4.0;

contract SimpleStorage {
    uint storedData=23;

    function set(uint x) {
        storedData=x;
    }

    function get() constant returns(uint) {
        return storedData;
    }
}
```
As you can see, the example is testing the get function.
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_call","params":["0x9df8ed11ea024183bd584480e80952c9b04e0122","0x6d4ce63c",-1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "contract": "0x",
        "failed": false,
        "poststate": "0xb724c37fd2047d26c7e22da0f43d8c520aa15d9fc9358872583eb4a11b9c6787",
        "result": "0x0000000000000000000000000000000000000000000000000000000000000005",
        "totalFee": 101,
        "txhash": "0xefaa679d7b6bbbf2b56b198f45156a82a737a352cb1d42f2f5357ed3a4f91a16",
        "usedGas": 424
    }
}
```
***

#### GetLogs

This method gets the event logs by block height, the contract address, and the event name.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_getLogs ","params":[GetLogsRequest],"id":1}` |

##### Parameters

- `height`:`int64` - block height (default: -1)
- `contract`:`string` - contract code in hex
- `topic`:`string` - topic

##### Returns

TODO

##### Example
When using the example below, the contract must be deployed first. The solidity code file:
```
pragma solidity ^0.4.0;

contract simple_storage_1 {
    uint storedData=23;

    event getLog(address addr, string message);
    event getLog1(string message);
    event getLog2(string message);

    function set(uint x) public{
        getLog1("set getLog1");
        getLog2("set getLog2");
        storedData=x;
    }

    function get() constant public returns(uint) {
        getLog(msg.sender, "get getLog");
        getLog1("get getLog1");
        set(16);
        return storedData;
    }
}
```
As you can see, this example is testing the get function. In this situation, the height is the block height of the block containing the get transaction.
```js
// Request
TODO

// Result
TODO

```
***

#### GeneratePayload

This method generate the contract method payload.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_generatePayload","params":[string, string, []string],"id":1}` |

##### Parameters

- `abiJSON`:`string` - contract json string
- `methodName`:`string` - contract method name
- `args`:`string` - args of contract method

##### Returns

- `result`:`string` payload of contract method with args

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_generatePayload","params":["[{\"constant\":false,\"inputs\":[{\"name\":\"x\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"get\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]", "set", ["1"]],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x60fe47b10000000000000000000000000000000000000000000000000000000000000001"
}
```
***

#### EstimateGas

This method Estimate the gas of a transaction.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"seele_estimateGas","params":[types.Transaction],"id":1}` |

##### Parameters

- `Hash`:`string` - transaction hash
- `Data`:`json` - transaction data
  - `From`:`string` - transaction sender
  - `To`:`string` - transaction receiver
  - `Amount`:`uint64` - amount value, unit is fan
  - `GasPrice`:`uint64` - transaction gas price in Fan
  - `GasLimit`:`uint64` - maximum gas for transaction
  - `Payload`:`string` - transaction payload
  - `AccountNonce`:`uint64` - transaction nonce

##### Returns

- `result`:uint64 - gas amount

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"seele_estimateGas","params":[{"Hash": "0xd02530a4126ecea2787d59bf5e9611907c6043dd900f894554624bd1d25bcb32","Data": {"From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","To": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831","Amount": 20000,"AccountNonce": 1,"GasPrice": 10,"GasLimit": 200000,"Payload": ""}}],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 63000
}
```
***

### txpool
RPC collection provided for internal use for transaction pool inquiry manipulation.
***

#### GetBlockTransactionCount

This method is used to obtain the number of transactions in the transaction pool based on block height or hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getBlockTransactionCount","params":[string,int64],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex
- `height`:`int64` - block height (default: -1)

##### Returns

- `result`:`int` - transactions count

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getBlockTransactionCount","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922",-1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetBlockTransactionCountByHeight

This method is used to obtain the number of transactions in the transaction pool based on block height.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getBlockTransactionCountByHeight","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height (default: -1)

##### Returns

- `result`:`int` - transactions count

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getBlockTransactionCountByHeight","params":[-1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetBlockTransactionCountByHash

This method is used to obtain the number of transactions in the transaction pool based on block hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getBlockTransactionCountByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `result`:`int` - transactions count

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getBlockTransactionCountByHash","params":["0x0000004c0336e63f76e7bd2b7888514eff47b3528df67ca6ee95edb9dff79c00"],"id":1}' localhost:8037
// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetTransactionByBlockIndex

This method is used to obtain the transaction content based on block height or hash and transaction index.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getTransactionByBlockIndex","params":[string,int,int],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `height`:`int` - block height (default: -1)
- `index`:`int` - transaction index, start with 0 (default: 0)

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTransactionByBlockIndex","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922", -1, 1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "accountNonce": 0,
        "amount": 150000000,
        "from": "0x0000000000000000000000000000000000000000",
        "gasLimit": 0,
        "gasPrice": 0,
        "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
        "payload": "",
        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
    }
}
```
***

#### GetTransactionByBlockHeightAndIndex

This method is used to obtain the transaction content based on block height and transaction index.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getTransactionByBlockHeightAndIndex","params":[int,int],"id":1}` |

##### Parameters

- `height`:`int` - block height (default: -1)
- `index`:`int` - transaction index, start with 0 (default: 0)

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTransactionByBlockHeightAndIndex","params":[4202, 1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "accountNonce": 0,
        "amount": 150000000,
        "from": "0x0000000000000000000000000000000000000000",
        "gasLimit": 0,
        "gasPrice": 0,
        "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
        "payload": "",
        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
    }
}
```
***

#### GetTransactionByBlockHashAndIndex

This method is used to obtain the transaction content based on block hash and transaction index.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getTransactionByBlockHashAndIndex","params":[string,int],"id":1}` |

##### Parameters

- `hash`:`string` - block hash
- `index`:`int` - transaction index, start with 0 (default: 0)

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTransactionByBlockHashAndIndex","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922", 1],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "accountNonce": 0,
        "amount": 150000000,
        "from": "0x0000000000000000000000000000000000000000",
        "gasLimit": 0,
        "gasPrice": 0,
        "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
        "payload": "",
        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
    }
}
```
***

#### GetTransactionByHash

This method returns transaction information by hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getTransactionByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `blockHash`:`string` - block hash
- `blockHeight`:`int` - block height
- `status`:`string` - transaction status
- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `gasLimit`:`Int` - transaction gas limit
- `gasPrice`:`Int` - transaction gas price
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `txIndex`:`int` - transaction index in block

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTransactionByHash","params":["0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff"],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blockHash": "0x0000009c753570436b0bdd4ea1b9cfb1611f181f7aae82d4ba265761c50c8479",
        "blockHeight": 3608,
        "status": "block",
        "transaction": {
                "accountNonce": 0,
                "amount": 150000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x473ea3667d073491d5896a93fcf84d7dd822988d07482f21e7a875787539e62e",
                "payload": "",
                "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
        },
        "txIndex": 0
    }
}
```
***

#### GetReceiptByTxHash

This method is used to obtain the receipt contents based on transaction hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getReceiptByTxHash","params":[string,string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex
- `abi`:`string` - the abi file of contract

##### Returns

- `contract`:`string` - contract address
- `failed`:`bool` - transaction executes successfully or not
- `poststate`:`string` - state trie root hash after transaction execution
- `result`:`string` - transaction result
- `totalFee`:`int` - transaction fee
- `txhash`:`string` - transaction hash
- `usedGas`:`int` - transaction gas

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getReceiptByTxHash","params":["0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff","""],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "contract": "0x",
        "failed": false,
        "poststate": "0xdd0b0fc6605bbb2e76b8c22ccd466ea5eaa1a80e4860fbdf971be58ded3d782b",
        "result": "0x",
        "totalFee": 1,
        "txhash": "0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",
        "usedGas": 0
    }
}
```
***

#### GetDebtByHash

This method is used to obtain the debt contents based on debt hash.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"txpool_getDebtByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - debt hash value in hex

##### Returns

- `blockHash`:`string` - block hash of the debt on
- `blockHeight`:`int64` - block height of the debt on
- `debt`:`json` - debt json
  - `Hash`:`string` - debt hash
  - `Data`:`json` - debt data
    - `TxHash`:`string` - txhash in debt
    - `From`:`string` - address of the sender
    - `Nonce`: `uint64` - nonce of From address
    - `Account`:`string` - debt account
    - `Amount`:`int64` - debt amount
    - `Price`:`int64` - debt price
    - `Code`:`string` - debt contract code
- `debtIndex`:`int` - debt index of the block debts
- `status`:`string` - debt status

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"txpool_getDebtByHash","params":["0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e"],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blockHash": "0x000001fb7817c8d9eeaa9bbed6670f8db62b605ad174f561e74afc60ac18c97b",
        "blockHeight": 170,
        "debt": {
            "Hash": "0xa0089462915e0a1b99ce3d75f6b51cdd5caf9a52691f327c9a27d222e0e38d57",
            "Data": {
                "TxHash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                "From": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "Nonce": 100,
                "Account": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1",
                "Amount": 88,
                "Price": 10,
                "Code": ""
            }
        },
        "debtIndex": 0,
        "status": "block"
    }
}
```
***

### download
RPC collection provided for internal inquiry of blockchain node synchronization state.

***

#### GetStatus

This method returns synchronization information.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"download_getStatus","params":[],"id":2}` |

##### Parameters
none

##### Returns

- `Status`:`string` - synchronization state
- `Duration`:`string` - synchronization duration (seconds)
- `StartNum`:`uint64` - synchronization initial block height
- `Amount`:`uint64` - synchronization value
- `Downloaded`:`uint64` - Synchronization number of times

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"download_getStatus","params":[],"id":2}' localhost:8037

//Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "Status": "NotSyncing",
        "Duration": "",
        "StartNum": 0,
        "Amount": 0,
        "Downloaded": 0
    }
}
```
***

### network

RPC collection provided for internal inquiry of network node information.

***

#### GetPeersInfo

This method returns the information of peer nodes.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"network_getPeersInfo","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `id`:`string` - node ID
- `caps`:`array` - peer node protocol and version array
- `network`:`struct` - network access address collection
  - `localAddress`:`string` - local address
  - `remoteAddress`:`string` - remote address
- `protocols`:`map` - node collection, key is the node name
  - `version`:`int` - node protocal
  - `difficulty`:`big.Int` - node difficulty
  - `head`:`string` - current block hash of the node
- `shard`:`uint` - shard id of the node
##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"network_getPeersInfo","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
        {
            "id": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
            "caps": [
                "lightSeele_1/1",
                "lightSeele_2/1",
                "seele/1"
            ],
            "network": {
                "localAddress": "127.0.0.1:54652",
                "remoteAddress": "127.0.0.1:8058"
            },
            "protocols": {
                "lightSeele_1": {
                    "version": 1,
                    "difficulty": 54618694483,
                    "head": "0000040c0c7af9b83736210e0f177998e61d2ec8b314fd2d4f49b8a11c4a28b7"
                },
                "lightSeele_2": {
                    "version": 1,
                    "difficulty": 2395409154,
                    "head": "0000030e2940702b853faa83f01cf34d7324de11ad0e52b4f33851c41e41ecf0"
                },
                "seele": {
                    "version": 1,
                    "difficulty": 2395409154,
                    "head": "0000030e2940702b853faa83f01cf34d7324de11ad0e52b4f33851c41e41ecf0"
                }
            },
            "shard": 2
        }
    ]
}
```
***

#### GetPeerCount

This method returns the number of peer nodes.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"network_getPeerCount","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - peer number of node

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"network_getPeerCount","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetNetVersion

This method returns the network version.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"network_getNetVersion","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - version number

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"network_getNetVersion","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1.0
}
```
***

#### GetProtocolVersion

This method returns the protocol version.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"network_getProtocolVersion","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - version number

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"network_getProtocolVersion","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetNetworkID

This method returns the network id.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"network_getNetworkID","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - network id

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"network_getNetworkID","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "seele"
}
```
***

### miner
RPC collection provided for internal inquiry of miner information.
***

#### Start

This method starts the miner with an input number of threads.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_start","params":[int],"id":2}` |

##### Parameters

- `threads`:`int` - number of threads

##### Returns

- `result`:`bool` - start result

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_start","params":[2],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### Stop

This method stops the miner.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_stop","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`bool` - stop result

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_stop","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### Status

This method returns the miner status.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_status","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - miner status

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_status","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "running"
}
```
***

#### GetCoinbase

This method is used to obtain the node coinbase.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_getCoinbase","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - coinbase

##### Example
```js
curl -X POST --data '{"jsonrpc":"2.0","method":"miner.GetCoinbase","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
}
```

#### SetThreads

This method is used to set the threads of miner consensus.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_setThreads","params":[],"id":2}` |

##### Parameters

- `threads`:`int` - miner threads (default: 0)

##### Returns

- `result`:`bool` - SetThreads result

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_setThreads","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### SetCoinbase

This method is used to set the coinbase

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_setCoinbase","params":["string"],"id":2}` |

##### Parameters

- `coinbase`:`string` coinbase of the miner

##### Returns

- `result`:`bool` - SetCoinbase result

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_setcoinbase","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### GetEngineInfo

This method returns engine information of miner

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"miner_getEngineInfo","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `hashrate`:`float64` - hashrate
- `threads`:`int` - miner threads

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"miner_getEngineInfo","params":[],"id":2}' localhost:8037

// Result
{
	"hashrate": 495812.2433994204,
	"threads": 1
}
```
***

### debug
RPC collection provided for internal debugging.
***

#### PrintBlock

This method is used to print block information in dump format based on block height.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_printBlock","params":[int64],"id":2}` |

##### Parameters

- `height`:`int64` - block height

##### Returns

- `HeaderHash`:`string` - block header hash
- `Header`:`json` - block header
- `PreviousBlockHash`:`string` - previous block hash
- `Creator`:`string` - block creator
- `StateHash`:`string` - state hash
- `TxHash`:`string` - transactions hash
- `ReceiptHash`:`string` - receipts hash
- `TxDebtHash`:`string` - transaction debts hash
- `DebtHash`:`string` - debts hash
- `Difficulty`:`string` - block td
- `Height`:`int64` - block height
- `CreateTimestamp`:`string` - create timestamp
- `Nonce`:`int64` - block nonce
- `ExtraData`:`string` - extra data
- `Transactions`:`array` - transactions on block
- `Hash`:`string` - transaction hash
- `Data`:`string` - transaction data
- `From`:`string` - amount sender
- `To`:`string` - amount receiver
- `Amount`:`int64` - transaction amount
- `AccountNonce`:`int64` - account nonce
- `Fee`:`int64` - transaction fee
- `Timestamp`:`int64` - transaction timestamp
- `Payload`:`string` - payload
- `Signature`:`json` - transaction signature json
- `Sig`:`string` - transaction sig
- `Debts`:`array` - dump format of block information
- `Hash`:`string` - debts hash
- `Data`:`json` - debts data
- `TxHash`:`string` - txhash in debt
- `Shard`:`int` - shard number of seele node where debts on
- `Account`:`array` - debt account
- `Amount`:`int64` - debt amount
- `Fee`:`int64` - debt fee
- `Code`:`string` - debt code

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_printBlock","params":[10368],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "HeaderHash": "0x000001a8946d75258f9e269d516e797779ca6bd4b190c701f81456c60958c688",
        "Header": {
            "PreviousBlockHash": "0x000001f2ba4bc08c6a39fb35fa193698f35066c6ca14ca773b944eae25a6c360",
            "Creator": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
            "StateHash": "0x875cd1618715a8414eb48f957b8a92b70699a9b3a94848d92da2fa278494ecc3",
            "TxHash": "0x390b401fa139861dcc7b7d78f18b043672a729b6d688b8cba38946b2b4114bb9",
            "ReceiptHash": "0x62db1441782a734fa65ee8f0678a8dd028fc813a11e4784ad24b596f5a071f01",
            "TxDebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "DebtHash": "0x5b240a1f3d6369489307fee52be9bc759312f873bde832bda975ee774ecacfaa",
            "Difficulty": 6348338,
            "Height": 1112,
            "CreateTimestamp": 1539147474,
            "Nonce": 16880251435180988161,
            "ExtraData": ""
        },
        "Transactions": [
            {
                "Hash": "0x8bb8afe4222ed759af503ab95417015321b4992c7913b440f1be47536929d3b4",
                "Data": {
                    "From": "0x0000000000000000000000000000000000000000",
                    "To": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 150000000,
                    "AccountNonce": 0,
                    "Fee": 0,
                    "Timestamp": 1539147474,
                    "Payload": ""
                },
                "Signature": {
                    "Sig": ""
                }
            }
        ],
        "Debts": [
            {
                "Hash": "0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e",
                "Data": {
                    "TxHash": "0x58752f8aeb2c69dd2c32059d3ad8b2d3d860c6d92aa2b3b30ff985e564f60fae",
                    "Shard": 2,
                    "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                    "Amount": 10000,
                    "Fee": 0,
                    "Code": ""
                }
            }
        ]
    }
}
```
***

#### GetTxPoolContent

This method is used to obtain the transaction pool content.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_getTxPoolContent","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp
- `fee`:`int` - transaction fee

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_getTxPoolContent","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc":"2.0",
    "id":2,
    "result":{
        "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21": [
        		{
        			"accountNonce": 4,
        			"amount": 10000,
        			"fee": 1,
        			"from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
        			"hash": "0x1d9579c07e8cbcab36efdd810d2ebd27585c1b79eb379afde5e077c22ad46e44",
        			"payload": "",
        			"timestamp": 0,
        			"to": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71"
        		}
        	]
        ]
    }
}
```
***

#### GetTxPoolTxCount

This method is used to obtain the number of transactions in the transaction pool.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_getTxPoolTxCount","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`uint64` - number of transactions

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_getTxPoolTxCount","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetPendingTxs

This method is used to obtain pending transactions in the transaction pool.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_getPendingTransactions","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp
- `fee`:`int` - transaction fee

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_getPendingTransactions","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": [
              	{
              		"accountNonce": 6,
              		"amount": 10000,
              		"fee": 1,
              		"from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
              		"hash": "0x4ad5843af174d32e31b54ef81ddcbfeec43f4eb5d01885dfe9828f9ce907fb80",
              		"payload": "",
              		"timestamp": 0,
              		"to": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71"
              	}
              ]
}
```
***

#### GetPendingDebts

This method is used to obtain pending transactions in the transaction pool.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_getPendingDebts","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `Data`:`json` - debt data
- `Account`:`array` - debt account
- `Amount`:`int64` - debt amount
- `Code`:`string` - debt code
- `Fee`:`int64` - debt fee
- `Shard`:`int` - shard number of seele node where debts on
- `TxHash`:`string` - txhash in debt
- `Hash`:`string` - debts hash

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_getPendingDebts","params":[],"id":2}' localhost:8037

// Result
[
        {
                "Data": {
                        "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                        "Amount": 10000,
                        "Code": "",
                        "Fee": 0,
                        "Shard": 2,
                        "TxHash": "0x049305964eac1c62b19f0a6a0841b1d24683c4c4f9a3f23c69c87dcca9ec3e28"
                },
                "Hash": "0xdcf8489c27e934c3f289c4a1d843b86dbd3445e8943903613ce640d7fb043e87"
        }
]
```
***

#### DumpHeap

This method dump heap for profiling and returns the file path.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` file path

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}' url

// Result
{
    "jsonrpc":"2.0",
    "id":2,
    "result":"C:\Users\dell-2\.seele\heap.dump"
}
```
***

#### GetTPS

This method returns TPS of seele node.

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"debug_getTPS","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `StartHeight`:`int64` start height
- `EndHeight`:`int64` end height
- `Count`:`int` tps
- `Duration`:`int` elapsed time from start height to end height

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "StartHeight": 13929,
        "EndHeight": 13941,
        "Count": 0,
        "Duration": 166
    }
}
```
***

### monitor
node monitor.

***

#### NodeInfo

This method returns the node information of the node

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"monitor_nodeInfo","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `name`:`string` monitor name
- `node`:`string` node name
- `port`:`int` port
- `netVersion`:`string` node network version
- `protocol`:`string` node network protocol
- `api`:`string` monitor api
- `os`:`string` system os
- `os_v`:`string` system os architecture
- `client`:`string` client version
- `canUpdateHistory`:`bool` can update history?
- `shard`:`int` shard number

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"monitor_nodeInfo","params":[],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "name": "Test monitor",
        "node": "seele node1",
        "port": 0,
        "netVersion": "1.0",
        "protocol": "1.0",
        "api": "No",
        "os": "windows",
        "os_v": "amd64",
        "client": "1.0",
        "canUpdateHistory": true,
        "shard": 1
    }
}
```
***

#### NodeStats

This method returns the information of the node

| Type | Template|
|-------|-------|
| RPC | `{"jsonrpc":"2.0","method":"monitor_nodeStats","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `active`:`string` is node actively?
- `syncing`:`string` is node syncing?
- `mining`:`int` is node mining?
- `peers`:`string` node peers number

##### Example
```js
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"monitor_nodeStats","params":[],"id":1}' localhost:8037

// Result
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "active": true,
        "syncing": true,
        "mining": true,
        "peers": 0
    }
}
```
***
