# Seele Client
Seele comes with a client which has support for all management APIs described here.

## JSON-RPC Support
| Type | Supported? |
|-------|:------------:|
| JSON-RPC 1.0 | &#x2713; |
| JSON-RPC 2.0 | &#x2713; |

## JSON-RPC Port
Default port:

| Client | Type | Address |
|-------|-------|:------------|
| Go | jsonrpc-2.0 |localhost:8027 |

## Client Command List
| Command | Full | Light |
|-------|:-------:|:-------:|
|[GetInfo](#getinfo)| &#x2713; ||
|[GetBalance](#getbalance)| &#x2713; | &#x2713; |
|[AddTx](#addtx)| &#x2713; | &#x2713; |
|[GetAccountNonce](#getaccountnonce)| &#x2713; | &#x2713; |
|[GetBlockHeight](#getblockheight)| &#x2713; | &#x2713; |
|[GetBlock](#getblock)| &#x2713; | &#x2713; |
|[SaveKey](#savekey)| &#x2713; | &#x2713; |
|[GetAccountShardNum](#getaccountshardnum)| &#x2713; | &#x2713; |
|[Call](#call)| &#x2713; ||
|GetLogs (Being Written)| &#x2713; ||
|[GetBlockTransactionCount](#getblocktransactioncount)| &#x2713; | &#x2713; |
|[GetTransactionByBlockIndex](#gettransactionbyblockindex)| &#x2713; | &#x2713; |
|[GetTransactionByHash](#gettransactionbyhash)| &#x2713; | &#x2713; |
|[GetReceiptByTxHash](#getreceiptbytxhash)| &#x2713; | &#x2713; |
|[GetDebtByHash](#getdebtbyhash)| &#x2713; ||
|[GetPeersInfo](#getpeersinfo)| &#x2713; | &#x2713; |
|[GetPeerCount](#getpeercount)| &#x2713; | &#x2713; |
|[GetNetworkVersion](#getnetworkversion)| &#x2713; | &#x2713; |
|[GetProtocolVersion](#getprotocolversion)| &#x2713; | &#x2713; |
|[GetNetworkID](#getnetworkid)| &#x2713; | &#x2713; |
|[Miner Start](#miner-start)| &#x2713; ||
|[Miner Stop](#miner-stop)| &#x2713; ||
|[Miner Status](#miner-status)| &#x2713; ||
|[Miner GetCoinbase](#miner-getcoinbase)| &#x2713; ||
|[Miner SetThreads](#miner-setthreads)| &#x2713; ||
|[Miner SetCoinbase](#miner-setcoinbase)| &#x2713; ||
|[Miner GetEngineInfo](#miner-getengineinfo)| &#x2713; ||
|[GetTxPoolContent](#gettxpoolcontent)| &#x2713; | &#x2713; |
|[GetTxPoolTxCount](#gettxpooltxcount)| &#x2713; | &#x2713; |
|[GetPendingTransactions](#getpendingtransactions)| &#x2713; | &#x2713; |
|[GetPendingDebts](#getpendingdebts)| &#x2713; ||
|[DumpHeap](#dumpheap)| &#x2713; ||
|[Key](#key)| &#x2713; | &#x2713; |
|[Sign](#sign)| &#x2713; | &#x2713; |
|[GeneratePayload](#generatepayload)| &#x2713; | &#x2713; |
|[CreateHTLC](#createhtlc)| &#x2713; ||
|[DecodeHTLC](#decodehtlc)| &#x2713; ||
|[GetHTLC](#gethtlc)| &#x2713; ||
|[GenerateHTLCKey](#generatehtlckey)| &#x2713; ||
|[RefundFromHTLC](#refundfromhtlc)| &#x2713; ||
|[GenerateHTLCStamptime](#generatehtlcstamptime)| &#x2713; ||
|[WithdrawFromHTLC](#withdrawfromhtlc)| &#x2713; ||
|[RegisterDomainName](#registerdomainname)| &#x2713; ||
|[GetDomainNameOwner](#getdomainnameowner)| &#x2713; ||
|GenSubChainCfgFile (Being Written)| &#x2713; ||
|QuerySubChain (Being Written)| &#x2713; ||
|RegisterSubChain (Being Written)| &#x2713; ||
### GetInfo
This method returns node information.

| Type | Template|
|-------|-------|
| Console | `client getinfo -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")

#### Returns

- `Coinbase`:`string` - node address
- `CurrentBlockHeight`:`uint64` - current block height
- `HeaderHash`:`string` - block hash
- `MinerStatus`:`string` - miner status
- `Shard`:`uint64` - shard number

#### Example
```js
// Request
client getinfo

// Result
{
	"Coinbase": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
	"CurrentBlockHeight": 1697,
	"HeaderHash": "0x0000008ad39a1f7c31f3aa730210170b95129ba9c3f15b2cc8fa3ec0f92015b6",
	"MinerStatus": "Running",
	"Shard": 1
}
```
***

### GetBalance

This method returns the account balance. If the account flag is null, the node address balance is returned.

| Type | Template|
|-------|-------|
| Console | `client getbalance --account 0x<public address> -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `account`:`string` - wallet address

#### Returns

- `Account`:`string` - account
- `Balance`:`big.Int` - account balance

#### Example
```js
// Request
client getbalance --account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21

// Result
{
	"Account": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
	"Balance": 261899990000
}
```
***

### AddTx

This method submits a transaction to the node.

| Type | Template|
|-------|-------|
| Console | `client sendtx --amount 10000 --fee 1 --from keyfile --to <string> -a <rpc address> ` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `from`:`types.Transaction.Data.From` - transaction 'from' address
- `to`:`types.Transaction.Data.To` - transaction 'to' address
- `amount`:`types.Transaction.Data.Amount` - transaction amount
- `fee`:`types.Transaction.Data.Fee` - transaction fee
- `payload`:`types.Transaction.Data.Payload` - transaction payload
- `nonce`:`types.Transaction.Data.AccountNonce` - transaction nonce


#### Returns

- `Hash`:`string` - transaction hash
- `From`:`types.Transaction.Data.From` - transaction 'from' address
- `To`:`types.Transaction.Data.To` - transaction 'to' address
- `Amount`:`types.Transaction.Data.Amount` - transaction amount
- `AccountNonce`:`types.Transaction.Data.AccountNonce` - transaction nonce
- `Fee`:`types.Transaction.Data.Fee` - transaction fee
- `Timestamp`:`int` - Time stamp
- `Payload`:`types.Transaction.Data.Payload` - transaction payload
- `Sig`:`string` - transaction signature

#### Example
```js
// Request
client sendtx --amount 10000 --fee 1 --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --to 0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71

// Result:
{
        "Hash": "0x02c240f019adc8b267b82026aef6b677c67867624e2acc1418149e7f8083ba0e",
        "Data": {
                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "To": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71",
                "Amount": 10000,
                "AccountNonce": 0,
                "Fee": 1,
                "Timestamp": 0,
                "Payload": ""
        },
        "Signature": {
                "Sig": "71r/IIg8ObGLYf0yRQiJ/vTw/3MZv2KNP8YSBZPixyxzT+FmP3+MN9GzAECV6aGo0oIzVaq+XGXyGW5R9BsV/AE="
        }
}
```
***

### GetAccountNonce

This method is used to obtain the nonce of the address.

| Type | Template|
|-------|-------|
| Console | `client getnonce -a <rpc address> --account 0x<public address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `account`:`string` - wallet address

#### Returns

- `result`:`uint64` - nonce

#### Example
```js
// Request
client getnonce --account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21

// Result
3
```
***

### GetBlockHeight

This method is used to obtain the height of the blockchain.

| Type | Template|
|-------|-------|
| Console | `client getblockheight -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")

#### Returns

- `result`:`uint64` - nonce

#### Example
```js
// Request
client getblockheight

// Result
1928
```
***

### GetBlock

This method is used to obtain the block content based on block height or block hash.

| Type | Template|
|-------|-------|
| Console | `client getblock --height -1 --hash -f=true -a <rpc address>`|

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `hash`:`string` - block hash
- `height`:`string` - block height
- `fulltx, f`:`boll` - whether to include detailed transaction information 

#### Returns

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
- `fee`:`Int` - transaction fee
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

#### Example
```js
// Request
client getblock --height 10368 --fulltx=true

// Result
{
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
                "CreateTimestamp": 1539050098,
                "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "Difficulty": 6563003,
                "ExtraData": "",
                "Height": 10368,
                "Nonce": 17825487295277270000,
                "PreviousBlockHash": "0x000001cba2c0b82402b3d2d2ad49f50ca0b21aee18c8123486377b2ec93aa0e0",
                "ReceiptHash": "0x02fa1d68e7bbf0b833f6e8719efb11b32c7f760e4ae050a4f9b58b8dd8ad1620",
                "StateHash": "0x8af14975f636ace27571cfcdcd9a1a1b4a5b15228977cf6207e82f63abf96ffd",
                "TxDebtHash": "0x58d7c36b25a715f5076ccb878940920f6bb333ab142287452509f881103960d2",
                "TxHash": "0xdb00575ff0cc0de89bd6c1799d37e5f600687963785176ca76e81bebfde6a03f"
        },
        "totalDifficulty": 68985339754,
        "transactions": [
                {
                        "accountNonce": 0,
                        "amount": 150000000,
                        "fee": 0,
                        "from": "0x0000000000000000000000000000000000000000",
                        "hash": "0x5c5c72b14ff8599cdd70c85c090ff74d4db0a5e2a9dbb5a702c31200de8245ae",
                        "payload": "",
                        "timestamp": 1539050098,
                        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
                },
                {
                        "accountNonce": 9,
                        "amount": 10000,
                        "fee": 1,
                        "from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "hash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62",
                        "payload": "",
                        "timestamp": 0,
                        "to": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831"
                }
        ],
        "txDebts": [
                {
                        "Data": {
                                "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                                "Amount": 10000,
                                "Code": "",
                                "Fee": 0,
                                "Shard": 2,
                                "TxHash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62"
                        },
                        "Hash": "0xe1c24a636a7c27aea7c384f6eb61eb49168129105f4c081ffa8ca7e77198b3f6"
                }
        ]
}
// Request
client getblock --hash 0x000002069d9de64bad509239e2a121afbf7de183576457a1d1fb077d19fa3e8c --fulltx=true

// Result
{
        "debts": [],
        "hash": "0x000002069d9de64bad509239e2a121afbf7de183576457a1d1fb077d19fa3e8c",
        "header": {
                "CreateTimestamp": 1539050098,
                "Creator": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "DebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "Difficulty": 6563003,
                "ExtraData": "",
                "Height": 10368,
                "Nonce": 17825487295277270000,
                "PreviousBlockHash": "0x000001cba2c0b82402b3d2d2ad49f50ca0b21aee18c8123486377b2ec93aa0e0",
                "ReceiptHash": "0x02fa1d68e7bbf0b833f6e8719efb11b32c7f760e4ae050a4f9b58b8dd8ad1620",
                "StateHash": "0x8af14975f636ace27571cfcdcd9a1a1b4a5b15228977cf6207e82f63abf96ffd",
                "TxDebtHash": "0x58d7c36b25a715f5076ccb878940920f6bb333ab142287452509f881103960d2",
                "TxHash": "0xdb00575ff0cc0de89bd6c1799d37e5f600687963785176ca76e81bebfde6a03f"
        },
        "totalDifficulty": 68985339754,
        "transactions": [
                {
                        "accountNonce": 0,
                        "amount": 150000000,
                        "fee": 0,
                        "from": "0x0000000000000000000000000000000000000000",
                        "hash": "0x5c5c72b14ff8599cdd70c85c090ff74d4db0a5e2a9dbb5a702c31200de8245ae",
                        "payload": "",
                        "timestamp": 1539050098,
                        "to": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
                },
                {
                        "accountNonce": 9,
                        "amount": 10000,
                        "fee": 1,
                        "from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "hash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62",
                        "payload": "",
                        "timestamp": 0,
                        "to": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831"
                }
        ],
        "txDebts": [
                {
                        "Data": {
                                "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                                "Amount": 10000,
                                "Code": "",
                                "Fee": 0,
                                "Shard": 2,
                                "TxHash": "0x0b30a6edf95a16933a0a77ffd3eb15680d4e3cb79466f21c1181c013a68eae62"
                        },
                        "Hash": "0xe1c24a636a7c27aea7c384f6eb61eb49168129105f4c081ffa8ca7e77198b3f6"
                }
        ]
}
```
***

### SaveKey

This method saves the private key.

| Type | Template|
|-------|-------|
| Console | `client savekey --privatekey 0x<privatekey> --file <filename> |

#### Parameters

- `privatekey`:`string` - private key for account
- `file`:`string` -  key store file name (default: ".keystore")


#### Returns

- none

#### Example
```js
// Request
client savekey --privatekey 0x52117b49022b246ee3921a7ff6771df065594a0dde555e40d8ce940a3ecfb654

// Result
Password:
Repeat password:
store key successful
```
***

### GetAccountShardNum
This method is used to get the account shard number with the specified account.

| Type | Template|
|-------|-------|
| Console | `client getshardnum --account <string>` <br>`client getshardnum --privatekey <string>` |

#### Parameters

- `account`:`string` - account address
- `privatekey`:`string` - private key for account

#### Returns

- `shard number`:`int` - shard number

#### Example
```js
// Request
client getshardnum --account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21

// Result
shard number: 1

// Request
client getshardnum --privatekey 0xf65e40c6809643b25ce4df33153da2f3338876f181f83d2281c6ac4a987b1479

// Result
shard number: 1

```
***

### Call

This method is used to execute a given transaction on a statedb of a given block height. It does not affect the statedb or blockchain and is useful for executing and retrieving values. However, the height currently does not support optional and will remove the from parameter in the next version or more.

| Type | Template|
|-------|-------|
| Console | `client call -a <rpc address> --payload 0x<abi bytecode> --to <string> --height <int>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `height`:`int64` - block height (default: -1)
- `payload`:`string` - transaction payload info
- `to`:`string` - to address

#### Returns

- `contract`:`string` - contract address
- `failed`:`bool` - contract executes successfully or not
- `poststate`:`string` - state trie root hash after transaction execution
- `result`:`string` - transaction result
- `totalFee`:`int64` - transaction fee
- `txhash`:`string` - transaction hash
- `usedGas`:`int64` - transaction gas


#### Example
When using the example below, the contract must be deployed first. The solidity code file:
```solidity
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
client call --payload 0x6d4ce63c --to 0x9df8ed11ea024183bd584480e80952c9b04e0122 --height -1

// Result
succeeded in calling a contract
{
        "contract": "0x",
        "failed": false,
        "poststate": "0x7c8b22f29b0f9e4db9d61264d3ea6bb8fdff412fc667d411a5e9e98205d36197",
        "result": "0x0000000000000000000000000000000000000000000000000000000000000005",
        "totalFee": 101,
        "txhash": "0x16330ce64136bd756491d4685b4fadd1d81fc36e88eff7987d1784bec466da77",
        "usedGas": 424
}
```
***

### GetLogs

This method gets the event logs by block height, the contract address, and the event name.

| Type | Template|
|-------|-------|
| Console | `client getlogs --height <block height> --address 0x<contract address> --topic 0x<event name hash>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `height`:`int64` - block height (default: -1)
- `contract`:`string` - contract code in hex
- `topic`:`string` - topic

#### Returns

- `response`:`GetLogsResponse` - response parameter struct
- `Txhash`:`string` - transaction hash
- `LogIndex`:`uint` - log index in receipt's logs 
- `Log`:`string` - log json

#### Example
When using the example below, the contract must be deployed first. The solidity code file:
```solidity
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
client getlogs --height 299 --address 0x40bdd5ab58a26cf761607684bd0230b1ea8200f2 --topic 0x978acaf30839c63aff19afed19ff8f3a430103773a67e3890aa1639af9a71bc4

// Result
[
        {
                "Log": {
                        "address": "0x40bdd5ab58a26cf761607684bd0230b1ea8200f2",
                        "blockNumber": 299,
                        "data": "AAAAAAAAAAAAAAAACleicU4ZO3rFBHXOYl8tz7SD10EAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKZ2V0IGdldExvZwAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=",
                        "topics": [
                                "0x978acaf30839c63aff19afed19ff8f3a430103773a67e3890aa1639af9a71bc4"
                        ],
                        "transactionIndex": 1
                },
                "LogIndex": 0,
                "Txhash": "0x2a06accc3739845451d50c74bc28a66c6152e9e536e263c3549a404abe8259fc"
        }
]
```
***

### GetBlockTransactionCount

This method is used to obtain the number of transactions in the transaction pool based on block height or hash.

| Type | Template|
|-------|-------|
| Console | `client getblocktxcount --height -1 -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `hash`:`string` - hash value in hex
- `height`:`int64` - block height (default: -1)

#### Returns

- `result`:`int` - number of transaction

#### Example
```js
// Request
client getblocktxcount --height 4202

// Result
2

// Request
client getblocktxcount --hash 0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922

// Result
2
```
***

### GetTransactionByBlockIndex

This method is used to obtain the transaction content based on block height and transaction index.

| Type | Template|
|-------|-------|
| Console | `client gettxinblock --height -1 --index 0 -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `hash`:`string` - block height
- `height`:`int` - block height (default: -1)
- `index`:`int` - transaction index, start with 0 (default: 0)

#### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `fee`:`Int` - transaction fee
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp

#### Example
```js
// Request
client gettxinblock --hash 0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922 --height -1 --index 1

// Result
{
	"accountNonce": 3,
	"amount": 10000,
	"fee": 1,
	"from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
	"hash": "0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",
	"payload": "",
	"timestamp": 0,
	"to": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71"
}
```
***

### GetTransactionByHash
This method returns tx information by hash.

| Type | Template|
|-------|-------|
| Console | `client gettxbyhash --hash <string> -a <rpc address>` |

#### Parameters

- `hash`:`string` - hash value in hex
- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")

#### Returns

- `blockHash`:`string` - block hash
- `blockHeight`:`int` - block height
- `status`:`string` - transaction status
- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `fee`:`Int` - transaction fee
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`int64` - transaction timestamp
- `txIndex`:`int` - transaction index in block

#### Example
```js
// Request
client gettxbyhash --hash 0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff

// Result
{
	"blockHash": "0x0000015592fab87d6efa10e63d7722f6f359d90a1aff9e70930b291931c34922",
	"blockHeight": 4202,
	"status": "block",
	"transaction": {
		"accountNonce": 3,
		"amount": 10000,
		"fee": 1,
		"from": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
		"hash": "0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",
		"payload": "",
		"timestamp": 0,
		"to": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71"
	},
	"txIndex": 1
}
```
***

### GetReceiptByTxHash
This method is used to obtain the receipt contents based on transaction hash.

| Type | Template|
|-------|-------|
| Console | `client getreceipt --hash <string> -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `hash`:`string` - hash value in hex

#### Returns

- `contract`:`string` - contract address
- `failed`:`bool` - transaction executes successfully or not
- `poststate`:`string` - state trie root hash after transaction execution
- `result`:`string` - transaction result
- `totalFee`:`int` - transaction fee
- `txhash`:`string` - transaction hash
- `usedGas`:`int` - transaction gas

#### Example
```js
// Request
client getreceipt --hash 0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff

// Result
{
	"contract": "0x",
	"failed": false,
	"poststate": "0xdd0b0fc6605bbb2e76b8c22ccd466ea5eaa1a80e4860fbdf971be58ded3d782b",
	"result": "0x",
	"totalFee": 1,
	"txhash": "0xbd2ca4f9869c714e589ad6a3b16731c8cb066de40d0e27e220cc1e014577baff",
	"usedGas": 0
}
```
***

### GetDebtByHash
This method is used to obtain the receipt contents based on transaction hash.

| Type | Template|
|-------|-------|
| Console | `client getdebtbyhash --hash <string> -a <rpc address>` |

#### Parameters

- `address, a`:`string` - address for client to request (default: "127.0.0.1:8027")
- `hash`:`string` - hash value in hex

#### Returns

- `blockHash`:`string` - block hash of the debt on
- `blockHeight`:`int64` - block height of the debt on
- `debt`:`json` - debt json
- `Data`:`json` - debt data
- `Account`:`string` - debt account
- `Amount`:`int64` - debt amount
- `Code`:`string` - debt code
- `Fee`:`int64` - debt fee
- `Shard`:`int` - shard number of seele node where debts on
- `TxHash`:`string` - txhash in debt
- `Hash`:`string` - debts hash
- `debtIndex`:`json` - debt index json
- `BlockHash`:`string` - block hash of the debt on
- `Index`:`string` - debt index of the block debts
- `status`:`string` - debt status

#### Example
```js
// Request
client getdebtbyhash --hash 0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e

// Result
{
        "blockHash": "0x000001a8946d75258f9e269d516e797779ca6bd4b190c701f81456c60958c688",
        "blockHeight": 1112,
        "debt": {
                "Data": {
                        "Account": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                        "Amount": 10000,
                        "Code": "",
                        "Fee": 0,
                        "Shard": 2,
                        "TxHash": "0x58752f8aeb2c69dd2c32059d3ad8b2d3d860c6d92aa2b3b30ff985e564f60fae"
                },
                "Hash": "0x0da1ed893e7f0ca2558c193b3b82ed20575a6978bea5b14f282309c69fee368e"
        },
        "debtIndex": {
                "BlockHash": "0x000001a8946d75258f9e269d516e797779ca6bd4b190c701f81456c60958c688",
                "Index": 0
        },
        "status": "block"
}
```
***

### GetPeersInfo

This method returns the information of peer nodes.

| Type | Template|
|-------|-------|
| Console | `client peersinfo -a <rpc address>` |

#### Parameters

none

#### Returns

- `id`:`string` - node ID
- `caps`:`array` - peer node protocol and version array
- `network`:`struct` - network access address collection
- `localAddress`:`string` - local address
- `remoteAddress`:`string` - remote address
- `protocols`:`mao` - node collection, key is the node name
- `version`:`struct` - node protocal
- `difficulty`:`struct` - node difficulty
- `head`:`struct` - current block hash of the node 

#### Example
```js
// Request
client getpeersinfo

// Result
[
	{
		"caps": [
			"lightSeele/1",
			"seele/1"
		],
		"id": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
		"network": {
			"localAddress": "127.0.0.1:55239",
			"remoteAddress": "127.0.0.1:8058"
		},
		"protocols": {
			"lightSeele": "handshake",
			"seele": "handshake"
		},
		"shard": 2
	}
]
```
***

### GetPeerCount

This method returns the number of peer nodes.

| Type | Template|
|-------|-------|
| Console | `client peers -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`int` - Peer note quantity

#### Example
```js
// Request
client peers

// Result
1
```
***

### GetNetworkVersion

This method returns the network version.

| Type | Template|
|-------|-------|
| Console | `client netversion -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`uint64` - version number

#### Example
```js
// Request
client netversion

// Result
1.0
```
***

### GetProtocolVersion

This method returns the protocol version.

| Type | Template|
|-------|-------|
| Console | `client protocolversion -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`uint64` - version number

#### Example
```js
// Request
client protocolversion

// Result
1
```
***

### GetNetworkID

This method returns the network id.

| Type | Template|
|-------|-------|
| Console | `client networkid -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`string` - network id

#### Example
```js
// Request
client networkid

// Result
seele
```
***

### Miner Start

This method starts the miner with an input number of threads.

| Type | Template|
|-------|-------|
| Console | `client miner start --threads <miner threads num> -a <rpc address>` |

#### Parameters

- `threads`:`int` - number of threads

#### Returns

none

#### Example
```js
// Request
client miner start --threads 2

// Result
true
```
***

### Miner Stop

This method stops the miner.

| Type | Template|
|-------|-------|
| Console | `client miner stop -a <rpc address>` |

#### Parameters

none

#### Returns

none

#### Example
```js
// Request
client miner stop

// Result
true
```
***

### Miner Status

This method returns the miner's status.

| Type | Template|
|-------|-------|
| Console | `client miner status -a <rpc address>` |

#### Parameters

none

#### Returns

none

#### Example
```js
// Request
client miner status

// Result
Running
```
***

### Miner GetCoinbase

This method is used to obtain the coinbase of miner consensus.

| Type | Template|
|-------|-------|
| Console | `client miner getcoinbase -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`string` - coinbase

#### Example
```js
// Request
client miner getcoinbase

// Result
"0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
```
***

### Miner SetThreads

This method is used to set the threads of miner consensus.

| Type | Template|
|-------|-------|
| Console | `client miner setthreads --threads <int> -a <rpc address>` |

#### Parameters

- `threads`:`int` - miner threads (default: 0)

#### Returns

- `result`:`int` - threads

#### Example
```js
// Request
client miner setthreads --threads 2

// Result
true
```
***

### Miner SetCoinbase

This method is used to set the coinbase

| Type | Template|
|-------|-------|
| Console | `client miner setcoinbase --coinbase <string> -a <rpc address>` |

#### Parameters

- `coinbase`:`string` coinbase of the miner

#### Returns

- none

#### Example
```js
// Request
client miner setcoinbase --coinbase 0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71

// Result
true
```
***

### Miner GetEngineInfo

This method returns engine information of miner

| Type | Template|
|-------|-------|
| Console | `client getengineinfo -a <rpc address>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")

#### Returns

- none

#### Example
```js
// Request
client getengineinfo

// Result
{
	"hashrate": 495812.2433994204,
	"threads": 1
}
```
***

### GetTxPoolContent

This method is used to obtain the transaction pool content.

| Type | Template|
|-------|-------|
| Console | `client gettxpoolcontent -a <rpc address>` |

#### Parameters

none

#### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp
- `fee`:`int` - transaction fee

#### Example
```js
// Request
client gettxpoolcontent

// Result
{
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
}
```
***

### GetTxPoolTxCount

This method is used to obtain the number of transactions in the transaction pool.

| Type | Template|
|-------|-------|
| Console | `client gettxpoolcount -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`uint64` - number of transactions

#### Example
```js
// Request
client gettxpoolcount

// Result
1
```
***

### GetPendingTransactions

This method is used to obtain pending transactions in the transaction pool.

| Type | Template|
|-------|-------|
| Console | `client getpendingtxs -a <rpc address>` |

#### Parameters

none

#### Returns

- `accountNonce`:`unit64` - account nonce
- `amount`:`Int` - transaction amount
- `from`:`string` - transaction provider
- `to`:`string` - transaction receiver
- `hash`:`string` - transaction hash
- `payload`:`array` - transaction payload
- `timestamp`:`string` - transaction timestamp
- `fee`:`int` - transaction fee

#### Example
```js
// Request
client getpendingtxs

// Result
[
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
```
***

### GetPendingDebts

This method is used to obtain pending debts in the debts pool.

| Type | Template|
|-------|-------|
| Console | `client getdebts -a <rpc address>` |

#### Parameters

none

#### Returns

- `Data`:`json` - debt data
- `Account`:`array` - debt account
- `Amount`:`int64` - debt amount
- `Code`:`string` - debt code
- `Fee`:`int64` - debt fee
- `Shard`:`int` - shard number of seele node where debts on
- `TxHash`:`string` - txhash in debt
- `Hash`:`string` - debts hash

#### Example
```js
// Request
client getdebts

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

### DumpHeap

This method dump heap for profiling and returns the file path.

| Type | Template|
|-------|-------|
| Console | `client dumpheap -a <rpc address>` |

#### Parameters

none

#### Returns

- `result`:`string` file path

#### Example
```js
// Request
client dumpheap

// Result
C:\Users\dell-2\.seele\heap.dump
```
***

### Key

This method is used to generate a public/private key pair and print them with hex values.

| Type | Template|
|-------|-------|
| Console | `client key --shard <int>` |

#### Parameters

- `shard`:`uint` shard number

#### Returns

- `public key`:`string` - public key
- `private key`:`string` - private key

#### Example
```js
// Request
client key

// Result
public key:  0xf66b94477311556da1767e267e0a5782045eea61
private key: 0x52117b49022b246ee3921a7ff6771df065594a0dde555e40d8ce940a3ecfb654
```
***

### Sign

This method is used to sign data with your private key.

| Type | Template|
|-------|-------|
| Console | `client sign --amount <int> --payload <string> --fee <int> --nonce <int> --privatekey <string> --to <string> -a <rpc address>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `privatekey`:`string` private key
- `to`:`string` public address of the receiver
- `amount`:`unit64` the amount of the transferred coins
- `fee`:`unit64` transaction fee
- `payload`:`string` transaction payload
- `nonce`:`int` transaction nonce

#### Returns

- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`string` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`string` transaction fee
- `Timestamp`:`string` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig

#### Example
```js
// Request
client sign --amount 20000 --fee 1 --nonce 7 --privatekey 0xf65e40c6809643b25ce4df33153da2f3338876f181f83d2281c6ac4a987b1479 --to 0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831

// Result
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 7, sending nonce: 7
{
        "Hash": "0x9ba03f6c4fcbe61a19f1721ec46c3f9dd3db91d236083a33b17396220c4accea",
        "Data": {
                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "To": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                "Amount": 20000,
                "AccountNonce": 7,
                "Fee": 1,
                "Timestamp": 0,
                "Payload": ""
        },
        "Signature": {
                "Sig": "BFkYL2KdCsoXl/njQs+v9/rwj3c5DVAMjfGTF7P6IdxiL1ra/NpLG/cM2HabPgqD1lV8PBjBy6UAmHuNxz5M1gA="
        }
}
```
***

### GeneratePayload

This method is used to generate payload.

| Type | Template|
|-------|-------|
| Console | `client payload --abi <string> --method <string> --args <string>` |

#### Parameters

- `abi`:`string` the abi file of contract
- `method`:`string` the method name of contract
- `args`:`string` the parameters of contract method

#### Returns

- `payload`:`string` payload data

#### Example
```js
// Request
client payload --abi test.sol --method set --args 10

// Result
payload:  0x60fe47b1000000000000000000000000000000000000000000000000000000000000000a
```
***

### CreateHTLC
This method is used to create HTLC.

| Type | Template|
|-------|-------|
| Console | `client htlc create --amount <unit64> --fee <unit64> --from <file> --to <string> --hash <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `to`:`string` to address
- `amount`:`unit64` amount value, unit is fan
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `hash`:`string`  hash value in hex
- `time`:`int` time lock in the HTLC (default: 0)

#### Returns

- `HashLock`:`string` contract hash lock
- `TimeLock`:`string` lock time
- `Tx`:`struct` tx
- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig

#### Example
```js
// Request
client htlc create --amount 10000 --fee 1 --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --to 0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71 --hash 0x9b9d066a68bc533fca7be7aaaffd21c9c971bb4b4960e79dcb36c532b67753dc

// Result
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 7, sending nonce: 7
{
        "HashLock": "0x9b9d066a68bc533fca7be7aaaffd21c9c971bb4b4960e79dcb36c532b67753dc",
        "TimeLock": 0,
        "Tx": {
                "Hash": "0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36",
                "Data": {
                        "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "To": "0x0000000000000000000000000000000000000103",
                        "Amount": 10000,
                        "AccountNonce": 7,
                        "Fee": 1,
                        "Timestamp": 0,
                        "Payload": "0x007b22486173684c6f636b223a22307839623964303636613638626335333366636137626537616161666664323163396339373162623462343936306537396463623336633533326236373735336463222c2254696d654c6f636b223a302c22546f223a223078313666626135666362396263346565376333623766656436363765343163
39613032343864613731227d"
                },
                "Signature": {
                        "Sig": "Kfup/u6aNxxCucvrollCfCNlL5iXd6ZXyEsQr5GE/9VirAgrNvIjkqmra9eTd9lxCZZXOtDMZNrAzpAQCXT3sAE="
                }
        }
}
```
***

### DecodeHTLC
This method is used to decode HTLC contract information.

| Type | Template|
|-------|-------|
| Console | `client htlc decode --payload` |

#### Parameters

- `payload`:`string` transaction payload info

#### Returns

- `HashLock`:`string` contract hash lock
- `TimeLock`:`string` lock time
- `Tx`:`struct` tx
- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig
- `To`:`string` transaction receiver
- `Refunded`:`bool` whether refunded
- `Withdrawed`:`bool` whether withdrawed
- `Preimage`:`string` HTLC preimage

#### Example
```js
// Request
client htlc decode --payload 0x7b22486173684c6f636b223a22307839623964303636613638626335333366636137626537616161666664323163396339373162623462343936306537396463623336633533326236373735336463222c2254696d654c6f636b223a302c22546f223a22307831366662613566636239626334656537633362376665643636376534316339613032343864613731227d

// Result
{
        "Tx": null,
        "HashLock": "0x9b9d066a68bc533fca7be7aaaffd21c9c971bb4b4960e79dcb36c532b67753dc",
        "TimeLock": 0,
        "To": "0x16fba5fcb9bc4ee7c3b7fed667e41c9a0248da71",
        "Refunded": false,
        "Withdrawed": false,
        "Preimage": ""
}
```
***

### GetHTLC
This method is used to get HTLC information.

| Type | Template|
|-------|-------|
| Console | `client htlc get --fee <unit64> --from <file> --nonce <int> --hash <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `hash`:`string`  hash value in hex

#### Returns

- `HashLock`:`string` contract hash lock
- `TimeLock`:`string` lock time
- `Tx`:`struct` tx
- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig
- `hash`:`string` get hash

#### Example
```js
// Request
client htlc get --fee 1 --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --nonce 7 --hash 0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36

// Result
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 7, sending nonce: 7
{
        "Tx": {
                "Hash": "0xc0efd904a084bb5b043cf08e0d826a68a71e0c6a01a4a279c2814802c5a1238d",
                "Data": {
                        "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "To": "0x0000000000000000000000000000000000000103",
                        "Amount": 0,
                        "AccountNonce": 7,
                        "Fee": 1,
                        "Timestamp": 0,
                        "Payload": "0x03c6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36"
                },
                "Signature": {
                        "Sig": "IySR/k7YpfXX0l8n8bwd7KRbrgE7hTVlfzqvS1diKT9X8zKXlMfQ8ijfvd4EVSY6TcLWpAb9TfoeRVjIGoVXJgE="
                }
        },
        "hash": "0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36"
}
```
***

### GenerateHTLCKey
This method is used to generate preimage key and key hash.

| Type | Template|
|-------|-------|
| Console | `client htlc key` |

#### Parameters

none

#### Returns

- `preimage`:`string` preimage key
- `hash`:`string` key hash

#### Example
```js
// Request
client htlc key

// Result
preimage: 0xffacc1067faf412f19db50b53b0b6a87d3f8a3af1778342edaa6d7f448a60b6a
hash: 0x39e29785892df0be30d54f406381cbb7c3566510fb6d6862c4da6ca4a16a66fe
```
***

### RefundFromHTLC
This method is used to refund from HTLC.

| Type | Template|
|-------|-------|
| Console | `client htlc refund --fee <unit64> --from <file> --nonce <int> --hash <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `hash`:`string`  hash value in hex

#### Returns

- `HashLock`:`string` contract hash lock
- `TimeLock`:`string` lock time
- `Tx`:`struct` tx
- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig
- `hash`:`string` get hash

#### Example
```js
// Request
client htlc refund --fee 1 --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --nonce 7 --hash 0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36

// Result
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 7, sending nonce: 7
{
        "Tx": {
                "Hash": "0x3662a1e37c654db07e9b72f8b756e3f1890da5fa105fa81101a790f7161469ea",
                "Data": {
                        "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "To": "0x0000000000000000000000000000000000000103",
                        "Amount": 0,
                        "AccountNonce": 7,
                        "Fee": 1,
                        "Timestamp": 0,
                        "Payload": "0x02c6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36"
                },
                "Signature": {
                        "Sig": "vxrwq8LbniTBuTi0TX/0AC57k74MWkViTPpl7BMsKoVZIXvF0NLTQ1fZsKrlBS//Co1SHjhZ8Ttjc73up115IwE="
                }
        },
        "hash": "0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36"
}
```
***

### GenerateHTLCStamptime
This method is used to generate unix timestamp.

| Type | Template|
|-------|-------|
| Console | `client htlc time --time <int>` |

#### Parameters

- `time`:`uint64` time lock in the HTLC (default: 0)

#### Returns

- `locktime`:`uint64` unix time stamptime

#### Example
```js
// Request
client htlc time

// Result
locktime: 1538982094
```
***

### WithdrawFromHTLC
This method is used to withdraw from HTLC.

| Type | Template|
|-------|-------|
| Console | `client htlc withdraw --fee <unit64> --from <file> --nonce <int> --hash <string> --preimage <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `hash`:`string`  hash value in hex
- `preimage`:`string`  preimage of hash in the HTLC

#### Returns

- `HashLock`:`string` contract hash lock
- `TimeLock`:`string` lock time
- `Tx`:`struct` tx
- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig
- `hash`:`string` get hash
- `preimage`:`string`  preimage of hash in the HTLC

#### Example
```js
// Request
client htlc withdraw --fee 1 --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --nonce 7 --hash 0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36 --preimage 0xffacc1067faf412f19db50b53b0b6a87d3f8a3af1778342edaa6d7f448a60b6a

// Result
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 7, sending nonce: 7
{
        "Tx": {
                "Hash": "0x44ffbd4aef7481b4375fc0b7cdba135986e8f822a59d222f4517ac43be11ea16",
                "Data": {
                        "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "To": "0x0000000000000000000000000000000000000103",
                        "Amount": 0,
                        "AccountNonce": 7,
                        "Fee": 1,
                        "Timestamp": 0,
                        "Payload": "0x017b2248617368223a22307863366563303439393235636132663965633938363038303663373563636261646466633630653263386137313764333562653930356263316631313733653336222c22507265696d616765223a2230786666616363313036376661663431326631396462353062353362306236613837643366386133616631
3737383334326564616136643766343438613630623661227d"
                },
                "Signature": {
                        "Sig": "gYUQC4KpPJKIdL4G160QQXEYBSqZzVbDevtshXN/mRJcDfYNBPDJmKTBpe07Fz9IhDt8RKJY/uEyEQrQNbhD6AA="
                }
        },
        "hash": "0xc6ec049925ca2f9ec9860806c75ccbaddfc60e2c8a717d35be905bc1f1173e36",
        "preimage": "0xffacc1067faf412f19db50b53b0b6a87d3f8a3af1778342edaa6d7f448a60b6a"
}
```
***

### RegisterDomainName
This method is used to register a domain name.

| Type | Template|
|-------|-------|
| Console | `client domain register --fee <unit64> --from <file> --nonce <int> --name <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `name`:`string`  domain or subchain name

#### Returns

- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig

#### Example
```js
// Request
client domain register --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --fee 1 --name test1

// Result
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 7, sending nonce: 7
{
        "Hash": "0x654c264e25bbe4db8b4e8600ef5407f6f3ac420b916f805f10015362aeb16af8",
        "Data": {
                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "To": "0x0000000000000000000000000000000000000101",
                "Amount": 0,
                "AccountNonce": 7,
                "Fee": 1,
                "Timestamp": 0,
                "Payload": "0x007465737431"
        },
        "Signature": {
                "Sig": "kqXargvc/ltBDPIQXwJAIUY/wn9uDb6UM7JkTiMTkGYmcF+y22mb0peCXx2OBpF6Y9vKXJUTNIFD2G/RNA3FpwA="
        }
}
```
***

### GetDomainNameOwner
This method is used to get the domain name owner.

| Type | Template|
|-------|-------|
| Console | `client domain owner --fee <unit64> --from <file> --nonce <int> --name <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `name`:`string`  domain or subchain name

#### Returns

- `Hash`:`string` transaction hash
- `Data`:`struct` transaction data
- `From`:`string`  transaction provider
- `To`:`string` transaction receiver
- `Amount`:`uint64` public address of the receiver
- `AccountNonce`:`unit64`  account nonce
- `Fee`:`unit64` transaction fee
- `Timestamp`:`unit64` transaction timestamp
- `Payload`:`string` transaction payload
- `Signature`:`string` transaction signature
- `Sig`:`string` transaction sig

#### Example
```js
// Request
client domain owner --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --fee 1 --name test1

// Result
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 8, sending nonce: 8
{
        "Hash": "0xb468f33fe8bfb0558aef0bd123cd086a51d4fd0bd224398d6394ef2998009a1a",
        "Data": {
                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "To": "0x0000000000000000000000000000000000000101",
                "Amount": 0,
                "AccountNonce": 8,
                "Fee": 1,
                "Timestamp": 0,
                "Payload": "0x017465737431"
        },
        "Signature": {
                "Sig": "3uEYGubuV/qCpad4reomXRNq3QyKNVG9c302C7u4WZoK7YZYiBd7mxCFq/vQwbU2opt9Rnp6NUHrU608Y/5VIQE="
        }
}
```
***

### GenSubChainCfgFile
This method is used to generate sub chain config file.

| Type | Template|
|-------|-------|
| Console | `client subchain config --fee <unit64> --from <file> --nonce <int> --name <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `coinbase`:`string` miner coinbase in hex
- `privatekey`:`string` private key for account
- `name`:`string`  domain or subchain name
- `output, o`:`string` subchain config file path
- `shard`:`string` shard number (default: 0)
- `node, n`:`string` subchain static node, for example:-n address:port -n address:prot

#### Returns

TODO

#### Example
```js
// Request
TODO

// Result
TODO

```
***

### QuerySubChain
This method is used to query sub chain.

| Type | Template|
|-------|-------|
| Console | `client subchain query --fee <unit64> --from <file> --nonce <int> --name <string>` |

#### Parameters

- `address, a`:`string` address for client to request (default: "127.0.0.1:8027")
- `from`:`string` key file of the sender
- `fee`:`unit64` transaction fee
- `nonce`:`int` transaction nonce (default: 0)
- `name`:`string`  domain or subchain name

#### Returns

TODO

#### Example
```js
// Request
TODO

// Result
TODO
```
***
