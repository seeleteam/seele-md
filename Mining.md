# Mining
***

## CPU Mining

Currently, Seele provides CPU Miner.

***Attention***，If you want to do mining on Seele，please make sure you are running the Seele Node on the Main-Net，and has to be run as full node.If you are not familiar with Seele，please read [Getting Started With Seele](Getting-Started-With-Seele.html).

### Start mining on Seele Node

You could start mining at the same time when Seele Node is starting，[Setting Up a Node](Getting-Started-With-Seele.html#setting-up-a-node) will help you on how to build a Node and start Seele Node.

Seele Node provides the `--miner, -m` command line parameter to specify whether to start mining when Node starts. The default is to start. If you don't want to mine, you can use `--miner stop` when starting Node. The Seele Node also provides the `--threads` command line argument to set the number of threads used by the Miner started by Node.

#### Example

<b>A configuration file is required at start of Seele Node, and the format of the configuration file is referenced [configpath](#configpath)</b>.

##### configpath
```sh
{
	  "basic":{
	    "name": "seele node1",
	    "version": "1.0",
	    "dataDir": "node1",
	    "address": "0.0.0.0:55027",
	    "coinbase": "0x010117ee8edfd14a1925e45e4cb698f195651b5a136e69ee9b394b7e8166cb1f"
	  },
	  "p2p": {
	    "privateKey": "0x8c5fe84f836732ae7935e70ed7f578851fabf533d327a36b4e9fc49b455aa721",
	    "staticNodes": [],
	    "address": "0.0.0.0:39007",
	    "networkID": 1
	  },
	  "log": {
	    "isDebug": true,
	    "printLog": false
	  },
	  "httpServer": {
	    "address": "127.0.0.1:65027",
	    "crosssorgins": [
	      "*"
	    ],
	    "whiteHost": [
	      "*"
	    ]
	  },
	  "wsserver": {
	    "address": "127.0.0.1:8080",
	    "pattern": "/ws"
	  },
	  "genesis": {
	    "accounts":{
	      "0x010171048615cfef6d03e10df133200a4266d3a8856795dd7e8873e300ecfbe4":100,
	      "0x01014a36b60fbd2bf80b1f9da08d98b11166075a595622fedca4435ec35533e0":200
	    },
	    "difficult":10000000,
	    "shard":1
	  }
	}
```

// Start mining by default when starting Seele Node</br>

```sh
node start -c configpath
``` 

// Start mining when starting Seele Node, and set the number of threads used by Miner to 2

```js
node start -c configpath --threads 2
```

// Mining does not start when starting Seele Node

```js
node start -c configpath --miner stop
```

### Start mining with Seele Full Client

If you already have a Seele full node, you can use the full node client to start and manage your Node Miner [Create a Full Node Client](Getting-Started-With-Seele.html#create-a-full-node-client) will help you on how to acquire a full client node。

#### Example

Client starts mining：

```js
client miner start

true
```

Client starts mining and sets the number of Miner threads to 2：

```js
client miner start --threads 2

true
```

Client stops mining：

```js
client miner stop

true
```

Get the Seele Node Miner running status：

```js
client miner status

"Running"

or

"Stopped"
```

Get Seele Node Miner Coinbase:

```js
client miner getcoinbase

"0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"
```

Sets Seele Node Miner Coinbase:

```js
client miner setcoinbase "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21"

true
```

Sets Seele Node Miner thread to 2:

```js
client miner setthreads --threads 2

true
```

Get Seele Node Miner Engine Information:

```js
client miner getengineinfo

{
	"hashrate": 495812.2433994204,
	"threads": 1
}
```

## Other Mining

Other Mining is currently under development.
