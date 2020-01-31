# Getting Started With Seele

## Setting Up a Node

- Preparations:
  - Install [Go v1.10](https://golang.org/doc/install) or higher, [Git](https://git-scm.com/downloads), and the [C compiler](#gcc-install-newbie-guide)(if you have not installed GO, Git or C compiler please follow README).
  - Clone the go-seele repository to the [GOPATH](https://github.com/golang/go/wiki/SettingGOPATH) directory :
`
go get -u -v github.com\seeleteam\go-seele\...
`
- In `seeleteam\go-seele\cmd\node`, run: `go build`; if you are running this for the first time a node executable object will appear.

	-	Something you may need to know before running a node:

		 1. If you run into the error related to "genesis block hash mismatch", follow the solution located [here](#genesis-block-hash-mismatch).  
		 2. If you want to run a light node, just replace node1.json with light_node1.json. Of course, don't forget to start a full node before you do this.
		 3. Unless otherwise stated, the nodes mentioned below refer to the full node.

- Get an account:

	You will need an account to send transactions, deploy contracts and start mining on the mainnet. See [How to create an account](How-To-Create-An-Account.html) to create your own account. However, if you just want to run a seele node locally or in a test environment, you can skip this step. Some default accounts are provided for testing.

- Running a Node:

  - In go-seele/cmd/node:
     - On Windows:
         - Running a Single Node：
             - In the cmd window, run: `node start -c .\config\node1.json`
             - By default this will start the miner, not metrics. You can add flags `-m stop` to not start the miner, or `-t true` to [start metrics](#start-metrics).
         - Running Multiple Nodes：
             - In one cmd window, run: `node start -c .\config\node1.json`
             - In a second cmd window, run: `node start -c .\config\node2.json`

     - On Linux & Mac:
         - Running a Single Node：
             - On terminal, run: `./node start -c ./config/node1.json`
             - By default this will start the miner, not metrics. You can add flags `-m stop` to not start the miner, or `-t true` to [start metrics](#start-metrics).
         - Running Multiple Nodes：
             - In one terminal window, run: `./node start -c ./config/node1.json`
             - In another terminal window, run: `./node start -c ./config/node2.json`

            **Important note:** under seeleteam/go-seele/cmd/node/config, there are 4 node configurations (with filename node*.json) that can be used as examples. To use your own account to interact with the mainnet, make sure you use the correct coinbase, p2p private key and shard information in one of these json files. For details, see [How to customize your node configurations](#How to customize your node configurations).

      If you want to have a quickstart in a test or private blockchain environment, you can use the default node configurations and accounts. For example:

            ./node start -c ./config/node1.json --accounts ./config/accounts.json

		Note that seeleteam/go-seele/cmd/node/config/accounts.json only contains test accounts, do not use them if you are going to connect to the Seele mainnet.

 - The node configuration and test accounts are shown as follows. To modify it for your own account, see [How to customize my node configurations](#How to customize my node configurations).

node1.json:
```
{
  "basic":{
    "name": "seele node1",
    "version": "1.0",
    "dataDir": "node1",
    "address": "0.0.0.0:8027",
    "coinbase": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
    "algorithm": "sha256"
  },
  "p2p": {
    "privateKey": "0xf65e40c6809643b25ce4df33153da2f3338876f181f83d2281c6ac4a987b1479",
    "staticNodes": [],
    "address": "0.0.0.0:8057",
    "networkID": "seele"
  },
  "log": {
    "isDebug": true,
    "printLog": true
  },
  "httpServer": {
    "address": "0.0.0.0:8037",
    "crossorigins": [
      "*"
    ],
    "whiteHost": [
      "*"
    ]
  },
  "wsserver": {
    "address": "0.0.0.0:8047",
    "crossorigins": [
      "*"
    ]
  },
  "metrics": {
    "address": "0.0.0.0:8087",
    "duration": 10,
    "database": "influxdb",
    "username": "test",
    "password": "test123"
  },
  "genesis": {
    "difficult":8000000,
    "shard":1,
    "timestamp":1539742676
  }
}
```

accounts.json:
```
{
  "0x007d1b1ea335e8e4a74c0be781d828dc7db934b1": 1000000000000,
  "0x0a57a2714e193b7ac50475ce625f2dcfb483d741": 1000000000000,
  "0x2a23825407740fa7163069257c57452c4d4fc3d1": 1000000000000,
  "0x2a87b6504cd00af95a83b9887112016a2a991cf1": 1000000000000,
  "0x3b691130ec4166bfc9ec7240217fc8d08903cf21": 1000000000000,
  "0x4eea165e9266f20bf6e5e08e0c11d38e8fc02661": 1000000000000,
  "0x4fb7c8b0287378f0cf8b5a9262bf3ef7e101f8d1": 1000000000000,
  "0xec759db47a65f6537d630517f6cd3ca39c6f93d1": 1000000000000,
  "0xfaf78f23293cc537154c275c874ede0f8c8b8801": 1000000000000,
  "0xfbe506bdaf256682551873290d0a794d51bac4d1": 1000000000000
}
```

<table> <tbody>
<tr>
<th>Domain</th>
<th>Parameter</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="6">basic</th>
<td>name</td>
<td>Name of node</td>
</tr>
<tr>
<td>version</td>
<td>Version of node</td>
</tr>
<tr>
<td>dataDir</td>
<td>System file path of node, used to store data</td>
</tr>
<tr>
<td>address</td>
<td>Address to start RPC server</td>
</tr>
<tr>
<td>coinbase</td>
<td>Coinbase used to mine</td>
</tr>
<tr>
<td>algorithm</td>
<td>consensus algorithm of the network</td>
</tr>


<tr>
<th rowspan="4">p2p</th>
<td>privateKey</td>
<td>Private key for the p2p module, not used as an account</td>
</tr>
<tr>
<td>staticNodes</td>
<td>A static node. When the node is started, it will be connected to search for more nodes.</td>
</tr>
<tr>
<td>address</td>
<td>The p2p server will listen on the TCP connection, which is used as the UDP address for the Kad protocol.</td>
</tr>
<tr>
<td>networkID</td>
<td>Used to indicate the network type. For example, 1 is testnet, 2 is mainnet.</td>
</tr>


<tr>
<th rowspan="2">log</th>
<td>isDebug</td>
<td>If IsDebug is true, the log will be on the debug level, otherwise it will be on the info level.</td>
</tr>
<tr>
<td>printLog</td>
<td>If PrintLog is true, then all logs will be printed on the console, otherwise it will be written and stored in a file.</td>
</tr>


<tr>
<th rowspan="3">httpServer</th>
<td>address</td>
<td>HTTP RPC's service address.</td>
</tr>
<tr>
<td>crossorgins</td>
<td>Sent to the client's cross-origin resource sharing origin. Note that CORS is a type of forced safety measure by the browser, which is irrelevant to the client's custom HTTP.</td>
</tr>
<tr>
<td>whiteHost</td>
<td>Whitelist of permitted hosts.</td>
</tr>


<tr>
<th rowspan="1">wsserver</th>
<td>address</td>
<td>Address of Websocket RPC server.</td>
</tr>

<tr>
<th rowspan="3">genesis</th>
<td>timestamp</td>
<td>Timestamp of the genesis block.</td>
</tr>
<tr>
<td>difficult</td>
<td>Difficulty level: should be difficult near the beginning in order for easier block creation.</td>
</tr>
<tr>
<td>shard</td>
<td>Number of shards in the genesis block.</td>
</tr>
</table>


- Help:
<a name="help1">

	Use "node -h" for a list of available commands.

	Use "node [command] --help" for more information about a command.
</a>

## Create a Full Node Client:

- Preparations:
  - Install go v1.10 or higher and the C compiler (if you haven't install GO, Git or C compiler please follow README).
  - In `seeleteam\go-seele\cmd\client`, run: `go build`. If you are running this for the first time, a client executable object will appear.

- Running a Full Node Client:
  - On Windows:
    - In the command window, run: `client`
  - On Mac & Linux:
    - In the command window, run: `./client`  

- Help:

```
client -h
NAME:
   client - interact with a full node process

USAGE:
   client [global options] command [command options] [arguments...]

AUTHOR:
   seeleteam <dev@seelenet.com>

COMMANDS:
     call              call contract
     deckeyfile        Decrypt key file
     domain            system domain name commands
     dumpheap          dump heap for profiling, return the file path
     getbalance        get balance info
     getblock          get block by height or hash
     getblockheight    get block height
     getblocktxcount   get block transaction count by block height or block hash
     getdebtbyhash     get debt by debt hash
     getdebts          get pending debts
     getinfo           get node info
     getlogs           get logs
     getnonce          get account nonce
     getpendingtxs     get pending transactions
     getreceipt        get receipt by transaction hash
     getshardnum       get account shard number
     gettxbyhash       get transaction by transaction hash
     gettxinblock      get transaction by block height or block hash with index of the transaction in the block
     gettxpoolcontent  get transaction pool contents
     gettxpoolcount    get transaction pool transaction count
     htlc              Hash time lock contract commands
     key               generate key with or without shard number
     miner             miner commands
     p2p               p2p commands
     payload           generate the payload according to the abi file and method name and args
     savekey           save private key to a keystore file
     sendtx            send transaction to node
     sign              generate a signed transaction and print it out
     subchain          system sub chain commands
     help, h           Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h  show help
```

## Create a Light Node Client:

- Preparations:
  - Install go v1.10 or higher and the C compiler.
  - In `seeleteam\go-seele\cmd\client\light`, run: `go build`. If you are running this for the first time, a client executable object will appear.

- Running a Light Node Client:
  - On Windows:
    - In the command window, run: `light`
  - On Mac & Linux:
    - In the command window, run: `./light`  

- Help:

```js
light -h
NAME:
   light - interact with a light node process

USAGE:
   light [global options] command [command options] [arguments...]

AUTHOR:
   seeleteam <dev@seelenet.com>

COMMANDS:
     deckeyfile        Decrypt key file
     getbalance        get balance info
     getblock          get block by height or hash
     getblockheight    get block height
     getblocktxcount   get block transaction count by block height or block hash
     getnonce          get account nonce
     getpendingtxs     get pending transactions
     getreceipt        get receipt by transaction hash
     getshardnum       get account shard number
     gettxbyhash       get transaction by transaction hash
     gettxinblock      get transaction by block height or block hash with index of the transaction in the block
     gettxpoolcontent  get transaction pool contents
     gettxpoolcount    get transaction pool transaction count
     key               generate key with or without shard number
     p2p               p2p commands
     payload           generate the payload according to the abi file and method name and args
     savekey           save private key to a keystore file
     sendtx            send transaction to node
     sign              generate a signed transaction and print it out
     help, h           Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h  show help
```

## Some common-used commands:

### 0. Get an account

  - [How to create an account](How-To-Create-An-Account.html) will help you get a Seele account.

### 1. Transfer

  - Of course, you need an account with money in it to transfer money (for example, 10 fans) to A.    
    > Use the following example need to add the `--accounts` parameter when you need to start the node, In seeleteam/go-seele/cmd/node:
    command:`node start -c ./config/node1.json --accounts ./config/accounts.json`

```js
  // Request (if not given value,  default value will be : gasprice = 10, gaslimit = 21000)
  client sendtx --amount 10000 --price 1 --gas 2 --from .keystore-shard-1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --to 0xb286933bccbec9ca1cd92257d12d12ebab9b1201

  // Response (If we want use coherent name as savekey step in “How To Create An Account”, it is recommended to use .keystore-shard1& It is .keystore-shard1 not .keystore-shard-1)

  In seeleteam/go-seele/cmd/node:

  Please input your key file password:
  account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 0, sending nonce: 0
  transaction sent successfully
  {
	"Hash": "0x9c0e2565b8a0b33c3f69aa6eb9bad4a86c3925a1fe12272e2082091b9b1c5609",
	"Data": {
		"From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
		"To": "0xb286933bccbec9ca1cd92257d12d12ebab9b1201",
		"Amount": 10000,
		"AccountNonce": 0,
		"GasPrice": 1,
		"GasLimit": 21000,
		"Timestamp": 0,
		"Payload": ""
	},
	"Signature": {
		"Sig": "N8XzJ/GEpU73dpzW5t5WShmVPFb8gQOrInGdypul8aBaDakmhbZ2rdqekA5bWslHQBfsoafeMukF5b7A1/6JWQA="
	}
  }
```

  - Query the transfer result with the tx `Hash`.

```js
  // Request
  client getreceipt --hash 0x9c0e2565b8a0b33c3f69aa6eb9bad4a86c3925a1fe12272e2082091b9b1c5609

  // Resposne
  {
	"contract": "0x",
	"failed": false,
	"poststate": "0xef59ced1b06d3ec77aa5c3b0fa1bd7cdd83890961f49d06aabe0a2d57583dd3b",
	"result": "0x",
	"totalFee": 21000,
	"txhash": "0x9c0e2565b8a0b33c3f69aa6eb9bad4a86c3925a1fe12272e2082091b9b1c5609",
	"usedGas": 21000
  }
```

The result of `"failure": false`row, indicating that the transfer was successful.
By the way, if tx is not packed by the miner or the miner is packing, you may see`get error when call rpc leveldb: not found`. Don't worry, just wait for servals seconds, or you can use `client gettxbyhash` to query tx `status`.

  - Confirm the A balance.

```js
  // Request
  client getbalance --account 0xb4153ca4090a11af1984cdf20b0d0cbed5ff97a1

  // Response
  {
        "Account": "0xb4153ca4090a11af1984cdf20b0d0cbed5ff97a1",
        "Balance": 10
  }
```

### 2. Deploy contract
  - For the sake of convenience, use A to deploy the `simple_storage.sol` contract. [Using the contract simulator](Using-the-contract-simulator.html) will help you to get the contract binary data.

```js
  // Request
client sendtx --amount 0 --from .keystore-shard-1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --payload 0x608060405234801561001057600080fd5b50600560008190555060df806100276000396000f3006080604052600436106049576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806360fe47b114604e5780636d4ce63c146078575b600080fd5b348015605957600080fd5b5060766004803603810190808035906020019092919050505060a0565b005b348015608357600080fd5b50608a60aa565b6040518082815260200191505060405180910390f35b8060008190555050565b600080549050905600a165627a7a723058207f6dc43a0d648e9f5a0cad5071cde46657de72eb87ab4cded53a7f1090f51e6d0029

  // Response
Please input your key file password:
account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 0, sending nonce: 0
transaction sent successfully
{
	"Hash": "0xc4674bf0a3ee0796d3ae139ac40a480fa40d4e59ed0af9aa22d57dbc3c21a96e",
	"Data": {
		"From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
		"To": "0x0000000000000000000000000000000000000000",
		"Amount": 0,
		"AccountNonce": 0,
		"GasPrice": 10,
		"GasLimit": 200000,
		"Timestamp": 0,
		"Payload": "0x608060405234801561001057600080fd5b50600560008190555060df806100276000396000f3006080604052600436106049576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806360fe47b114604e5780636d4ce63c146078575b600080fd5b348015605957600080fd5b5060766004803603810190808035906020019092919050505060a0565b005b348015608357600080fd5b50608a60aa565b6040518082815260200191505060405180910390f35b8060008190555050565b600080549050905600a165627a7a723058207f6dc43a0d648e9f5a0cad5071cde46657de72eb87ab4cded53a7f1090f51e6d0029"
	},
	"Signature": {
		"Sig": "Ws2zZlCiAyZYIx/iQQwz7hAG+K99gR5B8db2GZ0zKW8hTUfSBt1XH3swcB+dtZR/yUC1tl+jRY3Jv6fwRtYiiwA="
	}
}
  ```

If you display `get error when call rpc balance is not enough, account:0xb4153ca4090a11af1984cdf20b0d0cbed5ff97a1, balance:10, amount:0, fee:123`, that's right, I deliberately, quickly fill the money.

  - Query the contract deploy result

```js
// Request
client getreceipt --hash 0xc4674bf0a3ee0796d3ae139ac40a480fa40d4e59ed0af9aa22d57dbc3c21a96e

// Response
{
	"contract": "0x12fe58608430e36ba6bfb0a9bc5623a634530002",
	"failed": false,
	"poststate": "0x6bccb0ae94795ae716644300257863e157dd5717a00ca3293bd1d7e0cc1ece61",
	"result": "0x6080604052600436106049576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806360fe47b114604e5780636d4ce63c146078575b600080fd5b348015605957600080fd5b5060766004803603810190808035906020019092919050505060a0565b005b348015608357600080fd5b50608a60aa565b6040518082815260200191505060405180910390f35b8060008190555050565b600080549050905600a165627a7a723058207f6dc43a0d648e9f5a0cad5071cde46657de72eb87ab4cded53a7f1090f51e6d0029",
	"totalFee": 1007070,
	"txhash": "0xc4674bf0a3ee0796d3ae139ac40a480fa40d4e59ed0af9aa22d57dbc3c21a96e",
	"usedGas": 100707
}
```
The result of `"failure": false`row, which indicates the deploy contract was successful.
The result of `"contract": "0xc3e7b32db87dd5b8d70a78666518c6395d0f0092"` row is the contract address.

### 3. Call contract

#### Sendtx

  - `sendtx` to call the contract

```js
  // Request
  client sendtx --amount 0   --payload 0x6d4ce63c --from .keystore-shard-1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --to 0x12fe58608430e36ba6bfb0a9bc5623a634530002

  // Response
  Please input your key file password:
  account 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 current nonce: 1, sending nonce: 1
 transaction sent successfully
 {
	"Hash": "0xae073c03abc04ad182792bc5bf9faeb04d1c80888c985e839f896fd5fd08bf9f",
	"Data": {
		"From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
		"To": "0x12fe58608430e36ba6bfb0a9bc5623a634530002",
		"Amount": 0,
		"AccountNonce": 1,
		"GasPrice": 10,
		"GasLimit": 200000,
		"Timestamp": 0,
		"Payload": "0x6d4ce63c"
	},
	"Signature": {
		"Sig": "RB7a0T8ej34R7co1OgRsdYh3we1DQmJ1INUq1Tysoi4Sgf89u0Njvld+wOh1+XARhc/ojM4B0rpP4dIqqg7rvAA="
	}
 }
```

  - Query the result

```js
  // Request
  client getreceipt --hash 0xae073c03abc04ad182792bc5bf9faeb04d1c80888c985e839f896fd5fd08bf9f

  // Response
  {
	"contract": "0x",
	"failed": false,
	"poststate": "0x0685695c28fde434c3d9b1e857849ad761cc607a804aa32bef4185469c359995",
	"result": "0x0000000000000000000000000000000000000000000000000000000000000005",
	"totalFee": 216960,
	"txhash": "0xae073c03abc04ad182792bc5bf9faeb04d1c80888c985e839f896fd5fd08bf9f",
	"usedGas": 21696
  }
```

#### Call

  - `call` the contract, the `call` command is separate from the blockchain and is suitable for querying data without changing the state.

```js
  // Request
  client call --payload 0x6d4ce63c --to 0x12fe58608430e36ba6bfb0a9bc5623a634530002 --height -1

  // Response
  {
	"contract": "0x",
	"failed": false,
	"poststate": "0x6c81260cea77c64aa240534c27a3c46cf41749f4c027546675819b3b1fb58ccb",
	"result": "0x0000000000000000000000000000000000000000000000000000000000000005",
	"totalFee": 21696,
	"txhash": "0x452c1bbd09292411095780badf8f2b18b5e7ba72910214e683d741ff3547df3e",
	"usedGas": 21696
}
```
## How to customize your node configurations

Under seeleteam/go-seele/cmd/node/config, you can find four node*.json files. You can create your own Seele node by customizing any one of them.

1. After creating your account ([How to create an account](How-To-Create-An-Account.html)), replace "coinbase" field with your public key.

2. Modify the "shard" field with the correct shard number associated with your account.

3. Create another private-public key pair. Replace "privateKey" field in "p2p" section with your private key. This private key is used for p2p network only and should be different from the private key you use to mine and send transactions. **Do not use private keys associated with your coinbase or any other transaction accounts here!**

4. You could connect to some static nodes in the network by configuration. The format of "staticNodes" field is ["ip:port",...], for example, ["127.0.0.1:8057"].

5. If "isDebug" and "printLog" fields are true, the display is in debug mode and log mode when you run the Seele node. Default values should be false.

6. The "networkID", "difficult" and "timestamp" field for nodes in the same network should be the same. Nodes with different values in these field **can not** connect to each other.

## [GCC](https://gcc.gnu.org/) install newbie guide

Install Document: https://gcc.gnu.org/install/

Download Link: https://gcc.gnu.org/install/binaries.html

Or you can go directly to the [website](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/) to download the release installer. (Recommended)

## Start Metrics

If you want to start the metrics, it is necessary to install InfluxDB first.

Download Link: https://portal.influxdata.com/downloads

After downloading Influxdb, go to the Influxdb folder and update Influxdb.conf:

```
[http]
  # Determines whether the HTTP endpoint is enabled.
  # enabled = true

  # The bind address used by the HTTP service.
  # bind-address = ":8086"
  bind-address = ":8087"
```

Then, start the influxdb with influxdb.conf.

```
influxd run -config influxdb.conf
```

And in another cmd window, use the influxdb client to create the database "influxdb".

```
influx -port 8087
create database influxdb
exit
```

Finally, start the node with -t true.

## Q&A

### genesis block hash mismatch

If the log looks like the following:

- Windows:

```
data folder: C:\Users\seele\.seele\node1
INFO[0000] NewSeeleService BlockChain datadir is C:\Users\seele\.seele\node1\db\blockchain  caller="seeleservice.go:62" module=seele
INFO[0000] NewSeeleService account state datadir is C:\Users\seele\.seele\node1\db\accountState  caller="seeleservice.go:72" module=seele
ERRO[0000] NewSeeleService genesis.Initialize err. genesis block hash mismatch  caller="seeleservice.go:88" module=seele
genesis block hash mismatch
```

- Linux:

```
log folder: /var/folders/dq/mcz24sr571g48wrbjvdbpndw0000gn/T/seeleTemp/log
data folder: /Home/seele/.seele/node1
INFO[0000] NewSeeleService BlockChain datadir is /Home/seele/.seele/node1/db/blockchain  caller="seeleservice.go:62" module=seele
INFO[0000] NewSeeleService account state datadir is /Home/seele/.seele/node1/db/accountState  caller="seeleservice.go:72" module=seele
ERRO[0000] NewSeeleService genesis.Initialize err. genesis block hash mismatch  caller="seeleservice.go:88" module=seele
genesis block hash mismatch
```

You can just delete the .seele/node1 folder and restart. The absolute path to the .seele folder is in the logs printed above.
