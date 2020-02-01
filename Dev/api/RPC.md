# Seele JSON-RPC

*( node version >= v1.3.0 )*

JSON is a lightweight data exchange format. It can represent numbers, strings, ordered value sequences and key-value pairs.

JSON-RPC is a stateless, lightweight Remote Procedure Call (RPC) protocol. It defines several data structures and the relevant rules to handle them. JSON-RPC is transmission-agnostic, because it can be used in situations like process, socket, HTTP, or different message transmission environments. It uses JSON(RFC 4627) as the data format.

## Curl Examples Explained
The curl options below might return a response where the node complains about the content type, this is because the --data option sets the content type to application/x-www-form-urlencoded .


## JSON-RPC Support
| Type           | Supported? |
| -------------- |:----------:|
| JSON-RPC 1.0   |  &#x2713;  |
| JSON-RPC 2.0   |  &#x2713;  |
| Batch Requests |  &#x2713;  |
| HTTP           |  &#x2713;  |
| WS             |  &#x2713;  |

## JSON-RPC Port
Default port:

| Client | Type        | Address               |
| ------ | ----------- |:--------------------- |
| Go     | jsonrpc-2.0 | http://localhost:8027 |
| Go     | http        | http://localhost:8037 |
| Go     | websocket   | http://localhost:8047 |

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

| Command                                                                     |   Full   |  Light   |  public  | private |
| --------------------------------------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetInfo](#getinfo)                                                         | &#x2713; |          | &#x2713; |         |
| [GetBalance](#getbalance)                                                   | &#x2713; | &#x2713; | &#x2713; |         |
| [AddTx](#addtx)                                                             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetAccountNonce](#getaccountnonce)                                         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockHeight](#getblockheight)                                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlock](#getblock)                                                       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockByHash](#getblockbyhash)                                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockByHeight](#getblockbyheight)                                       | &#x2713; | &#x2713; | &#x2713; |         |
| [Call](#call)                                                               | &#x2713; |          | &#x2713; |         |
| [GetLogs](#getlogs)                                                         | &#x2713; |          | &#x2713; |         |
| [GetCode](#getcode)                                                         | &#x2713; |          | &#x2713; |         |
| [GeneratePayload](#generatepayload)                                         | &#x2713; |          | &#x2713; |         |
| [EstimateGas](#estimategas)                                                 | &#x2713; |          | &#x2713; |         |
| [GetBlockTransactionCount](#getblocktransactioncount)                       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionsFrom](#gettransactionsfrom)                                 | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionsTo](#gettransactionsto)                                     | &#x2713; | &#x2713; | &#x2713; |         |
| [GetAccountTransactions](#getaccounttransactions)                           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionsByHeight](#getblocktransactionsbyheight)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionsByHash](#getblocktransactionsbyhash)                   | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactions](#getblocktransactions)                               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionCountByHeight](#getblocktransactioncountbyheight)       | &#x2713; | &#x2713; | &#x2713; |         |
| [GetBlockTransactionCountByHash](#getblocktransactioncountbyhash)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockIndex](#gettransactionbyblockindex)                   | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockHeightAndIndex](#gettransactionbyblockheightandindex) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTransactionByBlockHashAndIndex](#gettransactionbyblockhashandindex)     | &#x2713; | &#x2713; | &#x2713; |         |
| [GetReceiptByTxHash](#getreceiptbytxhash)                                   | &#x2713; | &#x2713; | &#x2713; |         |

- [txpool](#txpool)

| Command                                       |   Full   |  Light   |  public  | private |
| --------------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetTxPoolContent](#gettxpoolcontent)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetTxPoolTxCount](#gettxpooltxcount)         | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingTxs](#getpendingtxs)               | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPendingDebts](#getpendingdebts)           | &#x2713; |          | &#x2713; |         |
| [GetTransactionByHash](#gettransactionbyhash) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetDebtByHash](#getdebtbyhash)               | &#x2713; |          | &#x2713; |         |
| [GetGasPrice](#getgasprice)                   | &#x2713; | &#x2713; | &#x2713; |         |

- [download](#download)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [IsSyncing](#issyncing) | &#x2713; |       | &#x2713; |         |
| [GetStatus](#getstatus) | &#x2713; |       | &#x2713; |         |

- [network](#network)

| Command                                   |   Full   |  Light   |  public  | private |
| ----------------------------------------- |:--------:|:--------:|:--------:|:-------:|
| [GetPeersInfo](#getpeersinfo)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetPeerCount](#getpeercount)             | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetVersion](#getnetversion)           | &#x2713; | &#x2713; | &#x2713; |         |
| [GetProtocolVersion](#getprotocolversion) | &#x2713; | &#x2713; | &#x2713; |         |
| [GetNetworkID](#getnetworkid)             | &#x2713; | &#x2713; | &#x2713; |         |
| [IsListening](#islistening)               | &#x2713; | &#x2713; | &#x2713; |         |

- [miner](#miner)

| Command                     |   Full   | Light | public | private  |
| --------------------------- |:--------:|:-----:|:------:|:--------:|
| [Start](#start)             | &#x2713; |       |        | &#x2713; |
| [Stop](#stop)               | &#x2713; |       |        | &#x2713; |
| [Status](#status)           | &#x2713; |       |        | &#x2713; |
| [GetCoinbase](#getcoinbase) | &#x2713; |       |        | &#x2713; |
| [GetTarget](#gettarget)     | &#x2713; |       |        | &#x2713; |
| [GetWork](#getwork)         | &#x2713; |       |        | &#x2713; |
| [SetThreads](#setthreads)   | &#x2713; |       |        | &#x2713; |
| [SetCoinbase](#setcoinbase) | &#x2713; |       |        | &#x2713; |
| [GetThreads](#getthreads)   | &#x2713; |       |        | &#x2713; |

- [debug](#debug)

| Command                   |   Full   | Light | public | private  |
| ------------------------- |:--------:|:-----:|:------:|:--------:|
| [PrintBlock](#printblock) | &#x2713; |       |        | &#x2713; |
| [DumpHeap](#dumpheap)     | &#x2713; |       |        | &#x2713; |
| [GetTPS](#gettps)         | &#x2713; |       |        | &#x2713; |

- [monitor](#monitor)

| Command                 |   Full   | Light |  public  | private |
| ----------------------- |:--------:|:-----:|:--------:|:-------:|
| [NodeInfo](#nodeinfo)   | &#x2713; |       | &#x2713; |         |
| [NodeStats](#nodestats) | &#x2713; |       | &#x2713; |         |

### seele
RPC collection provided for public for blockchain node and transaction manipulation.

***

#### GetInfo

This method returns the node information.

| Type | Template                                                        |
| ---- | --------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getInfo","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `Coinbase`:`string` - node address
- `CurrentBlockHeight`:`uint64` - current block height
- `HeaderHash`:`string` - block hash
- `MinerStatus`:`string` - miner status
- `Shard`:`int` - shard number
- `Version`:`string` - version number of the node
- `BlockAge`:`big.Int` - the age of the latest block of the node
- `PeerCnt`:`string` - total peer count and the peer count of each shard  

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getInfo","params":[],"id":1}' localhost:8037
```
- Result

```js
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": {
      "Coinbase": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
      "CurrentBlockHeight": 1759971,
      "HeaderHash": "0x64ac24b6463d2cf14b9fd8b1c38ea6347977b38f105f76e34baf24fcc46f6aaf",
      "Shard": 1,
      "MinerStatus": "Stopped",
      "Version": "v1.2.7",
      "BlockAge": -5,
      "PeerCnt": "11 (2 3 3 3)"
   }
}
```
***

#### GetBalance

This method returns the account balance given the account address.

| Type | Template                                                                                |
| ---- | --------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBalance","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `Account`:`string` - account
- `hexHash`:`string` - hex form of a block hash, set to "" for the latest balance
- `height` :`uint64` - height of a block, set to -1 for the latest balance

##### Returns

- `Account`:`string` - account
- `Balance`:`big.Int` - account balance

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBalance","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","",-1],"id":1}' localhost:8037
```
- Result

```js
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

| Type | Template                                                                       |
| ---- | ------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_addTx","params":[types.Transaction],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_addTx","params":[{"Hash": "0x3393e5566cb905d714599f2f888ecc6d223b83403887460fa5b2771e89a0436e","Data": {"From": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21","To":"0x2a87b6504cd00af95a83b9887112016a2a991cf1","Amount": 1,"AccountNonce":0,"Fee": 0,"GasPrice":10, "GasLimit":21000},"Signature":{"Sig":"fAvgVTXDyJZbfv07NYBK4aSolfY4ycBPQRwnQFpHRMc7ooOZw27U50o4TBoRelYX3QCRyvKpbxVlxhu7AnSB6QE="}}],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": true
}
```
***

#### GetAccountNonce

This method is used to obtain the account nonce.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getAccountNonce","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - account
- `hexHash`:`string` - hex form of a block hash, set to "" for the latest nonce
- `height` :`uint64` - height of a block, set to -1 for the latest nonce

##### Returns

- `result`:`uint64` - account nonce

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getAccountNonce","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21","",-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 3
}
```
***

#### GetBlockHeight

This method is used to obtain the height of the blockchain.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockHeight","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `result`:`uint64` - block height

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockHeight","params":[],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 1928
}
```
***

#### GetBlock

This method is used to obtain the block content based on block height or block hash.

| Type | Template                                                                           |
| ---- | ---------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlock","params":[string,string,bool],"id":1}` |

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
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - creator address
  - `TxHash`:`string` - tx hash
  - `ReceiptHash`:`string` - Receipts hash
  - `stateHash`:`string` - state tree hash
  - `TxDebtHash`:`string` - debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block difficulty
  - `Height`:`unit64` - block height
  - `CreateTimestamp`:`uint64` - create timestamp
  - `Witness`:`string` - block nonce
  - `Consensus`:`int` - consensus algorithm
  - `ExtraData`:`string` - extra data
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
  - `accountNonce`:`unit64` - account nonce
  - `amount`:`Int` - transaction amount
  - `from`:`string` - transaction provider
  - `gasLimit`:`Int` - transaction gas limit
  - `gasPrice`:`Int` - transaction gas price
  - `hash`:`string` - transaction hash
  - `payload`:`array` - transaction payload
  - `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
  - `Hash`:`string` - txDebts hash
  - `Data`:`json` - txDebts data
    - `TxHash`:`string` - transaction hash
    - `From`:`string` - transaction sender
    - `Nonce`:`unit64` - sender nonce
    - `Account`:`string` - transaction account
    - `Amount`:`int` - transaction amount
    - `Price`:`int` - transaction gas price
    - `Code`:`string` - transaction code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlock","params":["",19018,true],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [],
        "hash": "0x000002f75910694bf33a9a2f3e0cab454ac4b14ff9d32aee7b59efc20260f00c",
        "header": {
            "PreviousBlockHash": "0x000005f39610211ad1e888940a0e6affb538ea2397f73e08f1f894537997118c",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0xde119fb11c8c74b34a71ce376589a1711af5acef99aaf36827fbaafaeb9fe617",
            "TxHash": "0xa5dea280e6e880af7547ffea5c54526b0a3fae9dcd977a0a5a00e14852eb08ce",
            "ReceiptHash": "0xd6efdf2db85d6a5ab3fdc14925f67b9c97fb7ebdb733e5b2bb5776c694bc9073",
            "TxDebtHash": "0x8fde2b990967a9e51cb5218acc3318faea7a50429760cef37867b12c62f30b78",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 2258387,
            "Height": 19018,
            "CreateTimestamp": 1548821456,
            "Witness": "MTI4ODU5Njk2MTcyODI5NzQ3MzM=",
            "Consensus": 0,
            "ExtraData": ""
        },
        "totalDifficulty": 52970343102,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 1200000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x0071c67a94f3619d9c7acb6fd40750956df24beb5dfaa5372e87a83bc06e219c",
                "payload": "",
                "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
            },
            {
                "accountNonce": 100,
                "amount": 88,
                "from": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "gasLimit": 63000,
                "gasPrice": 10,
                "hash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                "payload": "",
                "to": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1"
            }
        ],
        "txDebts": [
            {
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
            }
        ]
    }
}
```
***

#### GetBlockByHash

This method is used to obtain the block content based on block hash.

| Type | Template                                                                          |
| ---- | --------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockByHash","params":[string,bool],"id":1}` |

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
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - creator address
  - `TxHash`:`string` - tx hash
  - `ReceiptHash`:`string` - Receipts hash
  - `stateHash`:`string` - state tree hash
  - `TxDebtHash`:`string` - debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block difficulty
  - `Height`:`unit64` - block height
  - `CreateTimestamp`:`uint64` - create timestamp
  - `Witness`:`string` - block nonce
  - `Consensus`:`int` - consensus algorithm
  - `ExtraData`:`string` - extra data
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
  - `accountNonce`:`unit64` - account nonce
  - `amount`:`Int` - transaction amount
  - `from`:`string` - transaction provider
  - `gasLimit`:`Int` - transaction gas limit
  - `gasPrice`:`Int` - transaction gas price
  - `hash`:`string` - transaction hash
  - `payload`:`array` - transaction payload
  - `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
  - `Hash`:`string` - txDebts hash
  - `Data`:`json` - txDebts data
    - `TxHash`:`string` - transaction hash
    - `From`:`string` - transaction sender
    - `Nonce`:`unit64` - sender nonce
    - `Account`:`string` - transaction account
    - `Amount`:`int` - transaction amount
    - `Price`:`int` - transaction gas price
    - `Code`:`string` - transaction code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockByHash","params":["0x000002f75910694bf33a9a2f3e0cab454ac4b14ff9d32aee7b59efc20260f00c",true],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "debts": [],
        "hash": "0x000002f75910694bf33a9a2f3e0cab454ac4b14ff9d32aee7b59efc20260f00c",
        "header": {
            "PreviousBlockHash": "0x000005f39610211ad1e888940a0e6affb538ea2397f73e08f1f894537997118c",
            "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
            "StateHash": "0xde119fb11c8c74b34a71ce376589a1711af5acef99aaf36827fbaafaeb9fe617",
            "TxHash": "0xa5dea280e6e880af7547ffea5c54526b0a3fae9dcd977a0a5a00e14852eb08ce",
            "ReceiptHash": "0xd6efdf2db85d6a5ab3fdc14925f67b9c97fb7ebdb733e5b2bb5776c694bc9073",
            "TxDebtHash": "0x8fde2b990967a9e51cb5218acc3318faea7a50429760cef37867b12c62f30b78",
            "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "Difficulty": 2258387,
            "Height": 19018,
            "CreateTimestamp": 1548821456,
            "Witness": "MTI4ODU5Njk2MTcyODI5NzQ3MzM=",
            "Consensus": 0,
            "ExtraData": ""
        },
        "totalDifficulty": 52970343102,
        "transactions": [
            {
                "accountNonce": 0,
                "amount": 1200000000,
                "from": "0x0000000000000000000000000000000000000000",
                "gasLimit": 0,
                "gasPrice": 0,
                "hash": "0x0071c67a94f3619d9c7acb6fd40750956df24beb5dfaa5372e87a83bc06e219c",
                "payload": "",
                "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
            },
            {
                "accountNonce": 100,
                "amount": 88,
                "from": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "gasLimit": 63000,
                "gasPrice": 10,
                "hash": "0xf7288fbc1ab3bea992dd5f311644f220b1accf8011f59df4778ca526843d1f68",
                "payload": "",
                "to": "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1"
            }
        ],
        "txDebts": [
            {
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
            }
        ]
    }
}
```
***

#### GetBlockByHeight

This method is used to obtain the block content based on block height.

| Type | Template                                                                            |
| ---- | ----------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockByHeight","params":[string,bool],"id":1}` |

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
  - `PreviousBlockHash`:`string` - previous block hash
  - `Creator`:`string` - creator address
  - `TxHash`:`string` - tx hash
  - `ReceiptHash`:`string` - Receipts hash
  - `stateHash`:`string` - state tree hash
  - `TxDebtHash`:`string` - debts hash
  - `DebtHash`:`string` - debts hash
  - `Difficulty`:`big.Int` - block difficulty
  - `Height`:`unit64` - block height
  - `CreateTimestamp`:`uint64` - create timestamp
  - `Witness`:`string` - block nonce
  - `SecondWitness`:`string` - second block nonce (degenerated)
  - `Consensus`:`int` - consensus algorithm
  - `ExtraData`:`string` - extra data
- `totalDifficulty`:`big.Int` - total difficulty
- `transactions`:`array` - transaction array
  - `accountNonce`:`unit64` - account nonce
  - `amount`:`Int` - transaction amount
  - `from`:`string` - transaction provider
  - `gasLimit`:`Int` - transaction gas limit
  - `gasPrice`:`Int` - transaction gas price
  - `hash`:`string` - transaction hash
  - `payload`:`array` - transaction payload
  - `to`:`string` - transaction receiver
- `txDebts`:`array` - transaction debts
  - `Hash`:`string` - txDebts hash
  - `Data`:`json` - txDebts data
    - `TxHash`:`string` - transaction hash
    - `From`:`string` - transaction sender
    - `Nonce`:`unit64` - sender nonce
    - `Account`:`string` - transaction account
    - `Amount`:`int` - transaction amount
    - `Price`:`int` - transaction gas price
    - `Code`:`string` - transaction code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockByHeight","params":[19018,true],"id":1}' localhost:8037
```
- Result

```js
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": {
      "debts": [],
      "hash": "0x430216878d75c4beeb5218158e9920a664e5e883a8311600dd4cb21c91b8d9a2",
      "header": {
         "PreviousBlockHash": "0x359e1148e8eb8bb2bc0e7878fff034cba775df8338a71d65e3c0b48668f11c45",
         "Creator": "0xd63a23ba710c16fb121f53a4e38163a23c053e31",
         "StateHash": "0xe0a7e462dda0df064521581ef482c43460a8ae4a313f42513b6f67f688e3f5fd",
         "TxHash": "0x1555ed359bcc999483174709a48218f0c1871756441025937fc45f85bf11dc99",
         "ReceiptHash": "0xc1da588af38fb099399b8b2f8d98183c2934d903a973a90f326a9ce1115e3c1e",
         "TxDebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
         "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
         "Difficulty": 5990106,
         "Height": 19018,
         "CreateTimestamp": 1554386780,
         "Witness": "NTkwOTMxOTAwNTgwMDIzMDA4NQ==",
         "SecondWitness": "NTkwOTMxOTAwNTgwMDQxODM3NQ==",
         "Consensus": 0,
         "ExtraData": ""
      },
      "totalDifficulty": 108806815827,
      "transactions": [
         {
            "accountNonce": 0,
            "amount": 600000000,
            "from": "0x0000000000000000000000000000000000000000",
            "gasLimit": 0,
            "gasPrice": 0,
            "hash": "0x48e3e648f8231bd3b48e356ead95412511e0576aa5be3614da4a57d7badb80e9",
            "payload": "",
            "signature": {
               "Sig": ""
            },
            "to": "0xd63a23ba710c16fb121f53a4e38163a23c053e31"
         }
      ],
      "txDebts": []
   }
}
```
***

#### Call

This method is used to execute a given transaction on a statedb of a given block height. It does not affect the statedb or blockchain and is useful for executing and retrieving values. However, the height currently does not support optional and will remove the from parameter in the next version or more.

| Type | Template                                                                 |
| ---- | ------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_call ","params":[CallRequest],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_call","params":["0x9df8ed11ea024183bd584480e80952c9b04e0122","0x6d4ce63c",-1],"id":1}' localhost:8037
```
- Result

```js
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

| Type | Template                                                                       |
| ---- | ------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getLogs ","params":[GetLogsRequest],"id":1}` |

##### Parameters

- `height`:`int64` - block height (default: -1)
- `contract`:`string` - contract address
- `abi`:`string` - contract abi
- `event`:`string` - event name

##### Returns

- `address`:`string` - contract address
- `topics`:`array` - topic array
- `data`:`string` - data
- `blocknumber`:`uint64` - block height
- `transactionNumber`:`uint` - the index of the transaction in the block

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getLogs","params":[1760936,"0x4df9ac0d329c07da15f202090649258c109a0022","[{\"constant\":false,\"inputs\":[{\"name\":\"x\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"addr\",\"type\":\"address\"},{\"indexed\":false,\"name\":\"message\",\"type\":\"string\"}],\"name\":\"getLog\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"message\",\"type\":\"string\"}],\"name\":\"getLog1\",\"type\":\"event\"},{\"anonymous\":false,\"inputs\":[{\"indexed\":false,\"name\":\"message\",\"type\":\"string\"}],\"name\":\"getLog2\",\"type\":\"event\"},{\"constant\":true,\"inputs\":[],\"name\":\"get\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]","getLog2"],"id":1}' localhost:8037
```
- Result

```js
{"jsonrpc":"2.0","id":1,"result":[{"address":"0x4df9ac0d329c07da15f202090649258c109a0022","topics":["0xe84bb31d4e9adbff26e80edeecb6cf8f3a95d1ba519cf60a08a6e6f8d62d8100"],"data":"0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000b736574206765744c6f6732000000000000000000000000000000000000000000","blockNumber":1760936,"transactionIndex":1}]}
```
***

#### GetCode

This method gets the contract code by block height and contract address.

| Type | Template                                                                      |
| ---- | ----------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getCode ","params":[string, int64],"id":1}` |

##### Parameters

- `contract`:`string` - contract address
- `height`:`int64` - block height (default: -1)

##### Returns

- `payload`:`string` - contract code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getCode","params":["0xe2b99c9e86ebe7b087ede32b2cca3a4b3ee10032", 1077640],"id":1}' localhost:8037
```
- Result

```js
{"jsonrpc":"2.0","id":1,"result":"0x610646610030600b82828239805160001a6073146000811461002057610022565bfe5b5030600052607381538281f300730000000000000000000000000000000000000000301460806040526004361061008f576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680634c5e1cae1461009457806375a3e8e8146100e857806388d0443714610159578063a21ab71614610197578063ab517b4f146101cb578063c8fccc691461023a575b600080fd5b6100d260048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff16906020019092919050505061027c565b6040518082815260200191505060405180910390f35b61011060048036038101908080359060200190929190803590602001909291905050506102cb565b604051808373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020018281526020019250505060405180910390f35b610181600480360381019080803590602001909291908035906020019092919050505061035d565b6040518082815260200191505060405180910390f35b6101b5600480360381019080803590602001909291905050506103c6565b6040518082815260200191505060405180910390f35b8180156101d757600080fd5b5061022060048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506103f9565b604051808215151515815260200191505060405180910390f35b6102626004803603810190808035906020019092919080359060200190929190505050610580565b604051808215151515815260200191505060405180910390f35b60008260000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060010154905092915050565b60008083600101838154811015156102df57fe5b9060005260206000200160000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1691508360000160008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206001015490509250929050565b60008082905080806001019150505b8360010180549050811080156103aa5750836001018181548110151561038e57fe5b9060005260206000200160000160149054906101000a900460ff165b156103bc57808060010191505061036c565b8091505092915050565b60006103f2827fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff61035d565b9050919050565b6000808460000160008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600001549050828560000160008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060010181905550600081111561049e5760019150610578565b8460010180548091906001016104b49190610594565b9050600181018560000160008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000206000018190555083856001018281548110151561051457fe5b9060005260206000200160000160006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff1602179055508460020160008154809291906001019190505550600091505b509392505050565b600082600101805490508210905092915050565b8154818355818111156105bb578183600052602060002091820191016105ba91906105c0565b5b505050565b61061791905b8082111561061357600080820160006101000a81549073ffffffffffffffffffffffffffffffffffffffff02191690556000820160146101000a81549060ff0219169055506001016105c6565b5090565b905600a165627a7a72305820b794fd1c17a9ff0d50981b40ff2dd307a38ab6776bc963e8a4bff7df0b11f5170029"}
```
***

#### GeneratePayload

This method generates the contract method payload.

| Type | Template                                                                                        |
| ---- | ----------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_generatePayload","params":[string, string, []string],"id":1}` |

##### Parameters

- `abiJSON`:`string` - contract json string
- `methodName`:`string` - contract method name
- `args`:`string` - args of contract method

##### Returns

- `result`:`string` payload of contract method with args

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_generatePayload","params":["[{\"constant\":false,\"inputs\":[{\"name\":\"x\",\"type\":\"uint256\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"get\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]", "set", ["1"]],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x60fe47b10000000000000000000000000000000000000000000000000000000000000001"
}
```
***

#### EstimateGas

This method estimates the gas of a transaction.

| Type | Template                                                                             |
| ---- | ------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_estimateGas","params":[types.Transaction],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_estimateGas","params":[{"Hash":"0xa56fc9d8fb292c989c61be57d3a2e77902d68331d19cfb689e491574c679b7a0","Data":{"Type":0,"From":"0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1","To":"0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1","Amount":10,"AccountNonce":64,"GasPrice":1,"GasLimit":21000,"Timestamp":0,"Payload":""},"Signature":{"Sig":"3a/HhtAao9QiLmGkjgcv2tRSsvMxx1myWJoCVYpaJ64T49rYmYWWpE0JCAjYVqPkK8t4V88C+0VTLKkBfd68+wA="}}],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 21000
}
```
***

#### GetBlockTransactionCount

This method is used to obtain the number of transactions in the block based on block height or hash.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockTransactionCount","params":[string,int64],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex
- `height`:`int64` - block height (default: -1)

##### Returns

- `result`:`int` - transactions count

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockTransactionCount","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922",-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetBlockTransactionCountByHeight

This method is used to obtain the number of transactions in the block based on block height.

| Type | Template                                                                                      |
| ---- | --------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockTransactionCountByHeight","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height (default: -1)

##### Returns

- `result`:`int` - transactions count

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockTransactionCountByHeight","params":[-1],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetBlockTransactionCountByHash

This method is used to obtain the number of transactions in the block based on block hash.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockTransactionCountByHash","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `result`:`int` - transactions count

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockTransactionCountByHash","params":["0x0000004c0336e63f76e7bd2b7888514eff47b3528df67ca6ee95edb9dff79c00"],"id":1}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2
}
```
***

#### GetTransactionByBlockIndex

This method is used to obtain the transaction content based on block height or hash and transaction index.

| Type | Template                                                                                         |
| ---- | ------------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getTransactionByBlockIndex","params":[string,int,int],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getTransactionByBlockIndex","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922", -1, 1],"id":1}' localhost:8037
```
- Result

```js
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

| Type | Template                                                                                           |
| ---- | -------------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getTransactionByBlockHeightAndIndex","params":[int,int],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getTransactionByBlockHeightAndIndex","params":[4202, 1],"id":1}' localhost:8037
```
- Result

```js
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

| Type | Template                                                                                            |
| ---- | --------------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getTransactionByBlockHashAndIndex","params":[string,int],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getTransactionByBlockHashAndIndex","params":["0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922", 1],"id":1}' localhost:8037
```
- Result

```js
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

#### GetReceiptByTxHash

This method is used to obtain the receipt contents based on transaction hash.

| Type | Template                                                                                |
| ---- | --------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getReceiptByTxHash","params":[string,string],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getReceiptByTxHash","params":["0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",""],"id":1}' localhost:8037
```
- Result

```js
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

#### GetTransactionsFrom

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                         |
| ---- | ------------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getTransactionsFrom","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - from account
- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getTransactionsFrom","params":["0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1","",177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasPrice" : 10,
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "amount" : 100000000,
            "payload" : "",
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "accountNonce" : 0,
            "gasLimit" : 21000,
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"
         }
      }
   ]
```
***

#### GetTransactionsTo

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                       |
| ---- | ---------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getTransactionsTo","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - from account
- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getTransactionsTo","params":["0x75b86ef99c31bb858032d46bd533b18356c61aa1","",177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasLimit" : 21000,
            "accountNonce" : 0,
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "amount" : 100000000,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "gasPrice" : 10,
            "payload" : "",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"
         }
      }
]
```
***


#### GetAccountTransactions

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                            |
| ---- | --------------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getAccountTransactions","params":[string,string ,uint64],"id":1}` |

##### Parameters

- `account`:`string` - from account
- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getAccountTransactions","params":["0x75b86ef99c31bb858032d46bd533b18356c61aa1","",177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasLimit" : 21000,
            "accountNonce" : 0,
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "amount" : 100000000,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "gasPrice" : 10,
            "payload" : "",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"
         }
      }
]
```
***

#### GetBlockTransactions

This method returns transactions at specific height or block hash.

| Type | Template                                                                                   |
| ---- | ------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockTransactions","params":[string ,uint64],"id":1}` |

##### Parameters

- `hexHash`:`string` - hex form of a block hash
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockTransactions","params":["",177],"id":1}' localhost:8037
```
- Result
```js
{
   "result" : [
      {
         "transaction 1" : {
            "amount" : 600000000,
            "gasPrice" : 0,
            "payload" : "",
            "gasLimit" : 0,
            "accountNonce" : 0,
            "to" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "from" : "0x0000000000000000000000000000000000000000",
            "hash" : "0xecc860869602e90b6f170e0106459fb243a637b49d5cf732b8f4526998bac1c5"
         }
      },
      {
         "transaction 2" : {
            "amount" : 100000000,
            "gasPrice" : 10,
            "payload" : "",
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b",
            "gasLimit" : 21000,
            "accountNonce" : 0
         }
      }
   ],
   "jsonrpc" : "2.0",
   "id" : 1
}
```
***

#### GetBlockTransactionsByHeight

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                   |
| ---- | ------------------------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockTransactionsByHeight","params":[uint64],"id":1}` |

##### Parameters

<!-- - `account`:`string` - from account -->
<!-- - `hexHash`:`string` - hex form of a block hash -->
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockTransactionsByHeight","params":[177],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasPrice" : 0,
            "to" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasLimit" : 0,
            "hash" : "0xecc860869602e90b6f170e0106459fb243a637b49d5cf732b8f4526998bac1c5",
            "amount" : 600000000,
            "payload" : "",
            "from" : "0x0000000000000000000000000000000000000000"
         }
      },
      {
         "transaction 2" : {
            "payload" : "",
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasPrice" : 10,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b",
            "amount" : 100000000,
            "gasLimit" : 21000
         }
      }
   ]
```
***

#### GetBlockTransactionsByHash

This method returns transactions from one account at specific height or block hash.

| Type | Template                                                                                 |
| ---- | ---------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"seele_getBlockTransactionsByHash","params":[string],"id":1}` |

##### Parameters

<!-- - `account`:`string` - from account -->
<!-- - `hexHash`:`string` - hex form of a block hash -->
- `height` :`uint64` - height of a block

##### Returns

- `transaction index`:`string` - transaction index
- `from`:`string` - transaction provider
- `amount`:`Int` - transaction amount
- `payload`:`array` - transaction payload
- `to`:`string` - transaction receiver
- `accountNonce`:`unit64` - account nonce
- `gasLimit`:`Int` - transaction gas limit
- `hash`:`string` - transaction hash


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"seele_getBlockTransactionsByHash","params":["0x1220bd0253ac24aff8152ea19ad50e6724bac08f914630cea1e901ba19dbe021"],"id":1}' localhost:8037
```
- Result
```js
[
      {
         "transaction 1" : {
            "gasPrice" : 0,
            "to" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasLimit" : 0,
            "hash" : "0xecc860869602e90b6f170e0106459fb243a637b49d5cf732b8f4526998bac1c5",
            "amount" : 600000000,
            "payload" : "",
            "from" : "0x0000000000000000000000000000000000000000"
         }
      },
      {
         "transaction 2" : {
            "payload" : "",
            "from" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
            "accountNonce" : 0,
            "gasPrice" : 10,
            "to" : "0x75b86ef99c31bb858032d46bd533b18356c61aa1",
            "hash" : "0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b",
            "amount" : 100000000,
            "gasLimit" : 21000
         }
      }
   ]
```
***

### txpool
RPC collection provided for internal use for transaction pool inquiry manipulation.
***

#### GetTransactionByHash

This method returns transaction information by hash.

| Type | Template                                                                            |
| ---- | ----------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getTransactionByHash","params":[string],"id":1}` |

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
- `signature`:`string` - transaction signature
- `txIndex`:`int` - transaction index in block

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTransactionByHash","params":["0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff"],"id":1}' localhost:8037
```
- Result

```js
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": {
      "blockHash": "0x702dc20ce8379ba340aff4a05d37faa818542032c3326832237a8c4f90a6ff2d",
      "blockHeight": 1733757,
      "status": "block",
      "transaction": {
         "accountNonce": 64,
         "amount": 10,
         "from": "0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1",
         "gasLimit": 21000,
         "gasPrice": 1,
         "hash": "0xa56fc9d8fb292c989c61be57d3a2e77902d68331d19cfb689e491574c679b7a0",
         "payload": "",
         "signature": {
            "Sig": "3a/HhtAao9QiLmGkjgcv2tRSsvMxx1myWJoCVYpaJ64T49rYmYWWpE0JCAjYVqPkK8t4V88C+0VTLKkBfd68+wA="
         },
         "to": "0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1"
      },
      "txIndex": 1
   }
}
```
***

#### GetDebtByHash

This method is used to obtain the debt contents based on debt hash.

| Type | Template                                                                     |
| ---- | ---------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getDebtByHash","params":[string],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getDebtByHash","params":["0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e"],"id":1}' localhost:8037
```
- Result

```js
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
#### GetGasPrice

This method returns the tx gas price.

| Type | Template                                                                   |
| ---- | -------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getGasPrice","params":[string],"id":1}` |

##### Parameters

- `hash`:`string` - hash value in hex

##### Returns

- `gasPrice`:`Int` - transaction gas price


##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getGasPrice","params":["0xff5db63c516ddd0bd428bc464ef09add60647007ca2f3afc584be7a98e0cf52b"],"id":1}' localhost:8037
```
- Result
```js
{
	"gasPrice": 10
}
```
Or (if transaction is not found)
```js
{
	"error": "the transaction not found"
}
```
***

#### GetTxPoolContent

This method is used to obtain the transaction pool content.

| Type | Template                                                                  |
| ---- | ------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getTxPoolContent","params":[],"id":2}` |

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
- `GasPrice`:`int64` - transaction gas price
- `GasLimit`:`int64` - transaction gas limit

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTxPoolContent","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "0x3b691130ec4166bfc9ec7240217fc8d08903cf21": [
            {
                "accountNonce": 102,
                "amount": 1,
                "from": "0x3b691130ec4166bfc9ec7240217fc8d08903cf21",
                "gasLimit": 21000,
                "gasPrice": 10,
                "hash": "0x1a4eb0f6754ef9b973c084f9b285296d616bd36cb9e3707e743d38db9edc7e8f",
                "payload": "",
                "to": "0x2a87b6504cd00af95a83b9887112016a2a991cf1"
            }
        ]
    }
}
```
***

#### GetTxPoolTxCount

This method is used to obtain the number of transactions in the transaction pool.

| Type | Template                                                                  |
| ---- | ------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getTxPoolTxCount","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`uint64` - number of transactions

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getTxPoolTxCount","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetPendingTransactions

This method is used to obtain pending transactions in the transaction pool.

| Type | Template                                                                        |
| ---- | ------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getPendingTransactions","params":[],"id":2}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getPendingTransactions","params":[],"id":2}' localhost:8037
```
- Result

```js
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

| Type | Template                                                                 |
| ---- | ------------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"txpool_getPendingDebts","params":[],"id":2}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"txpool_getPendingDebts","params":[],"id":2}' localhost:8037
```
- Result

```js
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


### download
RPC collection provided for internal inquiry of blockchain node synchronization state.

***

#### GetStatus

This method returns synchronization information.

| Type | Template                                                             |
| ---- | -------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"download_getStatus","params":[],"id":2}` |

##### Parameters
none

##### Returns

- `Status`:`string` - synchronization state
- `Duration`:`string` - synchronization duration (seconds)
- `StartNum`:`uint64` - synchronization initial block height
- `Amount`:`uint64` - synchronization value
- `Downloaded`:`uint64` - Synchronization number of times

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"download_getStatus","params":[],"id":2}' localhost:8037
```
- Result

```js
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

#### IsSyncing

This method returns the synchronization status.

| Type | Template                                                             |
| ---- | -------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"download_isSyncing","params":[],"id":2}` |

##### Parameters
none

##### Returns

- `result`:`bool` - synchronization state

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"download_isSyncing","params":[],"id":2}' localhost:8037
```
- Result

```js
{
	"jsonrpc":"2.0",
	"id":2,
	"result":false
}
```
***

### network

RPC collection provided for internal inquiry of network node information.

***

#### GetPeersInfo

This method returns the information of peer nodes.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getPeersInfo","params":[],"id":2}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getPeersInfo","params":[],"id":2}' localhost:8037
```
- Result

```js
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

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getPeerCount","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - peer number of node

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getPeerCount","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetNetVersion

This method returns the network version.

| Type | Template                                                                |
| ---- | ----------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getNetVersion","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - version number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getNetVersion","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1.0
}
```
***

#### GetProtocolVersion

This method returns the protocol version.

| Type | Template                                                                     |
| ---- | ---------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getProtocolVersion","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - version number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getProtocolVersion","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 1
}
```
***

#### GetNetworkID

This method returns the network id.

| Type | Template                                                               |
| ---- | ---------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_getNetworkID","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - network id

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_getNetworkID","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "seele"
}
```
***

#### IsListening

This method returns whether the node network is listening or not.

| Type | Template                                                              |
| ---- | --------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"network_isListening","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`bool` - listening status

##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"network_isListening","params":[],"id":2}' localhost:8037
```
- Result
```js
{
   "id" : 2,
   "jsonrpc" : "2.0",
   "result" : true
}
```
***

### miner
RPC collection provided for internal inquiry of miner information.
***

#### Start

This method starts the miner with an input number of threads.

| Type | Template                                                         |
| ---- | ---------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_start","params":[int],"id":2}` |

##### Parameters

- `threads`:`int` - number of threads

##### Returns

- `result`:`bool` - start result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_start","params":[2],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### Stop

This method stops the miner.

| Type | Template                                                     |
| ---- | ------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"miner_stop","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`bool` - stop result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_stop","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### Status

This method returns the miner status.

| Type | Template                                                       |
| ---- | -------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_status","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - miner status

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_status","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "running"
}
```
***

#### GetCoinbase

This method is used to obtain the node coinbase.

| Type | Template                                                            |
| ---- | ------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getCoinbase","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - coinbase

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getCoinbase","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
}
```
***

#### GetTarget

This method is used to obtain current SPOW mining difficulty.

| Type | Template                                                          |
| ---- | ----------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getTarget","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` - current SPOW mining difficulty

##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getTarget","params":[],"id":2}' localhost:8037
```
- Result
```js
{
   "jsonrpc" : "2.0",
   "id" : 2,
   "result" : "569762050"
}
```
***


#### GetWork

This method return miner current mining task.

| Type | Template                                                        |
| ---- | --------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getWork","params":[],"id":2}` |

##### Parameters

- `threads`:`int` - miner threads

##### Returns

- `result`:`bool` - SetThreads result

##### Example
- Request
```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getWork","params":[4],"id":2}' localhost:8037
```
- Result
```js
{
   "result" : {
      "debts" : null,
      "txs" : [
         {
            "Data" : {
               "GasPrice" : 0,
               "From" : "0x0000000000000000000000000000000000000000",
               "Type" : 1,
               "Timestamp" : 1580171186,
               "Payload" : "",
               "AccountNonce" : 0,
               "Amount" : 600000000,
               "GasLimit" : 0,
               "To" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1"
            },
            "Signature" : {
               "Sig" : ""
            },
            "Hash" : "0x3a3aa0d94085291262dbd7a177cd451d694618a6315692a68cf22cc6db98a89f"
         }
      ],
      "receipts" : [
         {
            "TxHash" : "0x3a3aa0d94085291262dbd7a177cd451d694618a6315692a68cf22cc6db98a89f",
            "TotalFee" : 0,
            "Result" : null,
            "PostState" : "0x09976f41a4a82d87a60450f5701264aca52544b89731f86707a7f970e01b3df8",
            "Logs" : null,
            "UsedGas" : 0,
            "Failed" : false,
            "ContractAddress" : null
         }
      ],
      "header" : {
         "Witness" : null,
         "ReceiptHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "DebtHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "SecondWitness" : null,
         "PreviousBlockHash" : "0xe84c9437d787e93676f891d9da54056272a8b460f7b057ea6a343bc3089f6c12",
         "CreateTimestamp" : 1580171186,
         "TxHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "Creator" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1",
         "TxDebtHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
         "Difficulty" : 8769846,
         "ExtraData" : null,
         "Height" : 3021,
         "StateHash" : "0x09976f41a4a82d87a60450f5701264aca52544b89731f86707a7f970e01b3df8",
         "Consensus" : 0
      },
      "coinbase" : "0xe5260a5fa3ac4b0df6287d6b197d6b3cd5befef1"
   },
   "jsonrpc" : "2.0",
   "id" : 2
}
```
***


#### SetThreads

This method is used to set the threads of miner consensus.

| Type | Template                                                           |
| ---- | ------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"miner_setThreads","params":[],"id":2}` |

##### Parameters

- `threads`:`int` - miner threads

##### Returns

- `result`:`bool` - SetThreads result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_setThreads","params":[4],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### SetCoinbase

This method is used to set the coinbase

| Type | Template                                                                    |
| ---- | --------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"miner_setCoinbase","params":["string"],"id":2}` |

##### Parameters

- `coinbase`:`string` coinbase of the miner

##### Returns

- `result`:`bool` - SetCoinbase result

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_setCoinbase","params":["0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": true
}
```
***

#### GetThreads

This method is used to get the threads of miner consensus.

| Type | Template                                                           |
| ---- | ------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"miner_getThreads","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`int` - miner threads

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"miner_getThreads","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": 2
}
```
***

### debug
RPC collection provided for internal debugging.
***

#### PrintBlock

This method is used to print block information in dump format based on block height.

| Type | Template                                                                |
| ---- | ----------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"debug_printBlock","params":[int64],"id":2}` |

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
  - `Difficulty`:`big.Int` - block td
  - `Height`:`uint64` - block height
  - `CreateTimestamp`:`big.Int` - create timestamp
  - `Witness`:`string` - block nonce
  - `Consensus`:`int` - 0 for POW consensus
  - `ExtraData`:`string` - extra data
- `Transactions`:`array` - transactions on block
  - `Hash`:`string` - transaction hash
  - `Data`:`string` - transaction data
    - `Type`:`int` - transaction type, 0 for regular type, 1 for reward type
    - `From`:`string` - amount sender
    - `To`:`string` - amount receiver
    - `Amount`:`int64` - transaction amount
    - `AccountNonce`:`int64` - account nonce
    - `GasPrice`:`int64` - transaction gas price
    - `GasLimit`:`int64` - maximum gas for contract creation/execution
    - `Timestamp`:`int64` - transaction timestamp
    - `Payload`:`string` - payload
    - `Signature`:`json` - transaction signature json
      - `Sig`:`string` - transaction sig
- `Debts`:`array` - dump format of block information
  - `Hash`:`string` - debts hash
  - `Data`:`json` - debts data
    - `TxHash`:`string` - txhash in debt
    - `From`:`string` - sender address
    - `Nonce`:`int64` - sender nonce
    - `Account`:`string` - debt account
    - `Amount`:`int64` - debt amount
    - `Price`:`int64` - debt gas price
    - `Code`:`string` - debt code

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"debug_printBlock","params":[10368],"id":2}' localhost:8037
```
- Result

```js
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


#### DumpHeap

This method dump heap for profiling and returns the file path.

| Type | Template                                                         |
| ---- | ---------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `result`:`string` file path

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"debug_dumpHeap","params":[],"id":2}' localhost:8037
```
- Result

```js
{
    "jsonrpc":"2.0",
    "id":2,
    "result":"C:\Users\dell-2\.seele\heap.dump"
}
```
***

#### GetTPS

This method returns TPS of seele node.

| Type | Template                                                       |
| ---- | -------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"debug_getTPS","params":[],"id":2}` |

##### Parameters

none

##### Returns

- `StartHeight`:`int64` start height
- `EndHeight`:`int64` end height
- `Count`:`int` tps
- `Duration`:`int` elapsed time from start height to end height

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"debug_getTPS","params":[],"id":2}' localhost:8037
```
- Result

```js
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

| Type | Template                                                           |
| ---- | ------------------------------------------------------------------ |
| RPC  | `{"jsonrpc":"2.0","method":"monitor_nodeInfo","params":[],"id":1}` |

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
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"monitor_nodeInfo","params":[],"id":1}' localhost:8037
```
- Result

```js
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

| Type | Template                                                            |
| ---- | ------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"monitor_nodeStats","params":[],"id":1}` |

##### Parameters

none

##### Returns

- `active`:`string` is node active？
- `syncing`:`string` is node syncing？
- `mining`:`int` is node mining?
- `peers`:`string` node peers number

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"monitor_nodeStats","params":[],"id":1}' localhost:8037
```
- Result

```js
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
