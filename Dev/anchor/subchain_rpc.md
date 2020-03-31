# Seele Subchain JSON-RPC

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

## JSON-RPC Contents
- [subchain](#subchain)

| Command                                         |   Full   | Light |  public  | private |
| ----------------------------------------------- |:--------:|:-----:|:--------:|:-------:|
| [GetBlockCreator](#getblockcreator)             | &#x2713; |       | &#x2713; |         |
| [GetBalanceTreeRoot](#getbalancetreeroot)       | &#x2713; |       | &#x2713; |         |
| [GetTxTreeRoot](#gettxtreeroot)                 | &#x2713; |       | &#x2713; |         |
| [GetBlockSignature](#getblocksignature)         | &#x2713; |       | &#x2713; |         |
| [GetBlockInfoForStem](#getblockinfoforstem)     | &#x2713; |       | &#x2713; |         |
| [GetTxMerkleInfo](#gettxmerkleinfo)             | &#x2713; |       | &#x2713; |         |
| [GetBalanceMerkleInfo](#getbalancemerkleinfo)   | &#x2713; |       | &#x2713; |         |
| [GetRecentTxTreeRoot](#getrecenttxtreeroot)     | &#x2713; |       | &#x2713; |         |
| [GetRecentTxMerkleInfo](#getrecenttxmerkleinfo) | &#x2713; |       | &#x2713; |         |
| [GetAccountTx](#getaccounttx)                   | &#x2713; |       | &#x2713; |         |
| [GetUpdatedAccountInfo](#getupdatedaccountinfo) | &#x2713; |       | &#x2713; |         |

### subchain
This RPC collection provides information of the subchain.

***

#### GetBlockCreator
This method returns the creator of a block.

| Type | Template                                                                        |
| ---- | ------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getBlockCreator","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height. Set to current block height if the given height is negative

##### Returns

- `result`: `string` - the creator of the block

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getBlockCreator","params":[10],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":"0xc78995a18569baf5e0f787c3d8d55a858602e381"
}

```
***

#### GetBalanceTreeRoot
This method returns the root hash of the balance merkle tree of a block.

| Type | Template                                                                           |
| ---- | ---------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getBalanceTreeRoot","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height. Set to current block height if the given height is negative


##### Returns

- `result`: `string` - the root hash of the balance merkle tree

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getBalanceTreeRoot","params":[5],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":"0x9f42c64b532f232abf470901aaec90c464e03c1c42f62c1cab98980ba7e270cd"
}
```

***

#### GetTxTreeRoot
This method returns the root hash of the transaction merkle tree of a block.

| Type | Template                                                                      |
| ---- | ----------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getTxTreeRoot","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height. Set to current block height if the given height is negative


##### Returns

- `result`: `string` - the root hash of the transaction merkle tree

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getTxTreeRoot","params":[5],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":"0x0000000000000000000000000000000000000000000000000000000000000000"
}
```

***

#### GetBlockSignature
This method returns the signature of a block.

| Type | Template                                                                          |
| ---- | --------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getBlockSignature","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height. Set to current block height if the given height is negative


##### Returns

- `result`: `string` - the signature of a block

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getBlockSignature","params":[5],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":"gnNE0tY4xh7bHSlPHwmYfynpiCEWww1Heh/fxPGgUDMbLF0zS5Aps7GYN74H96SFZzpaFD7VPqwDYLCtMDEVBAE="
}
```
***

#### GetBlockInfoForStem
This method returns some information of a block including the block creator, the root hash of tx tree and the root hash of balance tree.

| Type | Template                                                                            |
| ---- | ----------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getBlockInfoForStem","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height. Set to current block height if the given height is negative


##### Returns

- `result`: `string` - the RLP string of [block creator, block height, the root hash of tx tree, the root hash of balance tree]

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getBlockInfoForStem","params":[5],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":"+FiUx4mVoYVpuvXg94fD2NVahYYC44EFoAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoJ9CxktTLyMqv0cJAarskMRk4DwcQvYsHKuYmAun4nDN"
}
```
***

#### GetTxMerkleInfo
This method returns the index and merkle proof of a transaction on the transaction merkle tree.

| Type | Template                                                                         |
| ---- | -------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getTxMerkleInfo","params":[string],"id":1}` |

##### Parameters

- `hexHash`:`string` - hex form of a transaction hash


##### Returns

- `merkle index`: `int` - the index of the input transaction at the leaf level of the transaction merkle tree
- `merkle proof`: `string` - the merkle proof of the input transaction

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getTxMerkleInfo","params":["0x35504bd889343dac8c4d6a3fbb23ae3ee63929ee6555bf17a9e8e2fc007db6de"],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":
	{
		"merkle index":0,
		"merkle proof":"wA=="
	}
}
```
***

#### GetBalanceMerkleInfo
This method returns the index and merkle proof of an account on the balance merkle tree at a given height.

| Type | Template                                                                                     |
| ---- | -------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getBalanceMerkleInfo","params":[string, int64],"id":1}` |

##### Parameters

- `account`:`string` - account
- `height`:`int64` - block height. Set to current block height if the given height is negative

##### Returns

- `account`: `string` - account
- `balance`: `big.Int` - account balance
- `merkle index`: `int` - the index of the input account at the leaf level of the balance merkle tree
- `merkle proof`: `string` - the merkle proof of the input account
- `nonce`: `uint64` - account nonce

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getBalanceMerkleInfo","params":["0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1", 100],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,"result":
	{
		"account":"0xeeedb76e23cd27988543832f7a09ca8e80b7dc11",
		"balance":17499999999971922,
		"merkle index":1,
		"merkle proof":"+EKgn0LGS1MvIyq/RwkBquyQxGTgPBxC9iwcq5iYC6ficM2gfzJ8t/g1LaYrX8+NFCa1E3bwdHKQLs+BMDHrLAWTQvg=",
		"nonce":1}
	}
```
***

#### GetRecentTxTreeRoot
This method returns the root hash of the recent transaction merkle tree.

| Type | Template                                                                            |
| ---- | ----------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getRecentTxTreeRoot","params":[int64],"id":1}` |

##### Parameters

- `height`:`int64` - block height. Set to current block height if the given height is negative


##### Returns

- `result`: `string` - the root hash of the recent transaction merkle tree; return empty hash if this block is not a relay block

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getRecentTxTreeRoot","params":[80],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":"0x07c0f93a6ddff59831c6975fd39b5a3eb048775c2c10fcfd8801c512078bbd6a"
}
```

***

#### GetRecentTxMerkleInfo
This method returns the index and merkle proof of an account on the recent transaction merkle tree at a given height.

| Type | Template                                                                                      |
| ---- | --------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getRecentTxMerkleInfo","params":[string, int64],"id":1}` |

##### Parameters

- `account`:`string` - account
- `height`:`int64` - block height. Set to current block height if the given height is negative

##### Returns

- `account`: `string` - account
- `merkle index`: `int` - the index of the input account at the leaf level of the recent transaction merkle tree
- `merkle proof`: `string` - the merkle proof of the input account

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getRecentTxMerkleInfo","params":["0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1", 80],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":
	{
		"account":"0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1",
		"merkle index":1,
		"merkle proof":"4aCr4Xf+YSGbnph4GbrIHmWWT33zlCGFSE1zDEl8HtZw4w=="
	}
}
```
***

#### GetAccountTx
This method returns the transactions and stem signatures(used in Stem contract) of an account between two blocks(inclusive).

| Type | Template                                                                                    |
| ---- | ------------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getAccountTx","params":[string, int64, int64],"id":1}` |

##### Parameters

- `account`:`string` - account
- `startHeight`:`int64` - start height. Set to current block height if the given height is negative
- `endHeight`:`int64` - end height. Set to current block height if the given height is negative


##### Returns

- `account`: `string` - account
- `txs`: `string` - the RLP string of the transaction array of the input account from startHeight to endHeight
- `signatures`: `string` - the RLP string of the Stem signature array corresponding to the transaction array

##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getAccountTx","params":["0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1", 60, 80],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":
	{
		"account":"0x8cd42eebf7ccc855b303e8bba75674c8f3d0f1e1",
		"signatures":"+EO4QRJt2rePmjk3Elw97AP5jsg0KJNWSxtK/7cD46+tsVEWGWXjb/jD6VaHj1/PiwPLr+5ZE8Rc2gvZj4aP2q9VOhIA",
		"txs":"87LxlO7tt24jzSeYhUODL3oJyo6At9wRlIzULuv3zMhVswPou6dWdMjz0PHhAoABgx6EgA=="
	}
}
```
***

#### GetUpdatedAccountInfo
This method returns the recent updated accounts.

| Type | Template                                                                              |
| ---- | ------------------------------------------------------------------------------------- |
| RPC  | `{"jsonrpc":"2.0","method":"subchain_getUpdatedAccountInfo","params":[int64],"id":1}` |

##### Parameters

- `height`:`uint64` - block height

##### Returns

- `updated accounts`: `string` - the RLP string of the array of recent updated accounts from height - relayInterval + 1 to height
- `balances`: `string` - the RLP string of the balance array corresponding to updated accounts


##### Example
- Request

```js
curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"subchain_getUpdatedAccountInfo","params":[80],"id":1}' localhost:8031
```

- Result

```js
{
	"jsonrpc":"2.0",
	"id":1,
	"result":
	{
		"balances":"yoCHPiwoQ5FSUgI=",
		"updated accounts":"+D+Ux4mVoYVpuvXg94fD2NVahYYC44GU7u23biPNJ5iFQ4MvegnKjoC33BGUjNQu6/fMyFWzA+i7p1Z0yPPQ8eE="
	}
}
```
***
