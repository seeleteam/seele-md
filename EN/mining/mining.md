### Windows users tryout [seele-one-click-mining](https://github.com/seeleteam/seele-one-click-mining/releases/latest)! 
- Refer to the readme.txt in zip for user instructions。 


# Mining

### Download

Download the newest[executables and configuration templates](https://github.com/seeleteam/go-seele/releases/latest). The extracted directory has the following structure

```
mac/linux/win32_v#.#.#
├── node1.json //shard1 config template
├── node2.json //shard2 config template
├── node3.json //shard3 config template
├── node4.json //shard4 config template
└── build 
    ├── client //client executable: for using node services
    ├── discovery
    ├── light
    ├── node //node executable: for runnig a node
    ├── tool
    └── vm
```

Use the following commands in the `build` directory

### Accounts

Generate: generate keypairs using shard numbers

```bash
$ ./client key --shard 1
public key:  0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451
private key: 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a
```

Validate: check privatekey or pulickey validity and key shard number

```bash
$ ./client getshardnum --account 0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451
shard number: 1
$ ./client getshardnum --privatekey 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a
shard number: 1
```

Save: Create keyfile using privatekey, filename, password

```bash
./client savekey --privatekey 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a --file shard1account
Password:
Repeat password:
store key successfully, the key file path is shard1account
```

Restore: restore privateKey with keyfile and password

```bash
$ ./client deckeyfile --file shard1account
Please input your key file password:
public key:  0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451
private key: 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a
```

### Configure node.json

1. Change mining account
  - To mine in shard 1, generate a shard 1 keypaire, then place the publickey in node1.json template
  - To mine in shard 2, generate a shard 2 keypaire, then place the publickey in node2.json template
  - Similarly for 3 and 4.
2. Change node id
  - Generate a keypair whose shard matters not, and fill the template with the privatekey.

Example with configuring shard1 template.

Before 
```js
{
  "basic":{
    ...
    "coinbase": "0xcee66ad4a1909f6b5170dec230c1a69bfc2b21d1", ← publickey for mining
    ...
  },
  "p2p": {
    "privateKey": "0xf65e40c6809643b25ce4df33153da2f3338876f181f83d2281c6ac4a987b1479", ← node id
    ...
  },
  ...
}
```
after
```yml
{
  "basic":{
    ...
    "coinbase": "0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451", ← shard1 account publickey
    ...
  },
  "p2p": {
    "privateKey": "0xa12b2ef3e40389ef2e0e3130a88674071760a283c5ed53dfeae40a10cdedb9a8", ← shard2 privatekey 
    ...
  },
  ...
}
```

### Run node 

Run mining node: with 12 threads，using node1.json as configuration file.
```bash
./node start -c ../node1.json --threads 12
```
Run node without mining: 
```bash
./node start -c ../node1.json -m stop
```

### Using node services

When node starts, it checks the completeness of its database at a speed of roughly 10,000 blocks per second. Then the node will launch its services, which the client executable can access.
  - shard 1 listening port：8027
  - shard 2 listening port：8028
  - shard 3 listening port：8029
  - shard 4 listening port：8026
  
Balance:
```bash
$ ./client getbalance --account 0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451 -a 104.218.164.169:8027
{
        "Account": "0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451",
        "Balance": 0 ←balance, fan as unit, 1seele=100million fan
}
```
Node info:
```bash
$ ./client getinfo -a 127.0.0.1:8027
{
        "BlockAge": 54, ←seconds since the heighest block created
        "Coinbase": "0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451", ←mining acount
        "CurrentBlockHeight": 1225756, ←height
        "HeaderHash": "0xa12b2ef3e40389ef2e0e3130a88674071760a283c5ed53dfeae40a10cdedb9a8", ←node id
        "MinerStatus": "Stopped", ←minging or not
        "PeerCnt": "162 (19 54 45 44)", ←total peer number（peers connected from 1 2 3 4）
        "Shard": 1, ←shard number
        "Version": "v1.2.4" ←version
}

```
Use `./client` to view all available commands, and `-h` to see details of how to use them, for example `./client sendtx -h` to see how to send transactions with keyfile.

# Compile node

The following commands work on ubuntu and mac.

### Check git，gcc，go version

```bash
$ git --version
git version 2.17.1

$ gcc --version
gcc (Ubuntu 7.3.0-27ubuntu1~18.04) 7.3.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
​
$ go version
go version go1.10.4 linux/amd64
```

### Download go-seele
 Download go-seele: configure the path ~/go/src/github.com/seeleteam。
```bash
~$ cd
~$ mkdir -p go/src/github.com/seeleteam
~$ cd go/src/github.com/seeleteam
~/go/src/github.com/seeleteam$ git clone https://github.com/seeleteam/go-seele.git

Cloning into 'go-seele'...
remote: Enumerating objects: 53, done.
remote: Counting objects: 100% (53/53), done.
remote: Compressing objects: 100% (48/48), done.
remote: Total 10032 (delta 13), reused 15 (delta 4), pack-reused 9979
Receiving objects: 100% (10032/10032), 12.25 MiB | 18.45 MiB/s, done.
Resolving deltas: 100% (5804/5804), done.

```
### Compile go-seele：

```bash
~/go/src/github.com/seeleteam$ cd go-seele
~/go/src/github.com/seeleteam/go-seele$ make all
go build -o ./build/discovery ./cmd/discovery
Done discovery building
go build -o ./build/node ./cmd/node 
Done node building
go build -o ./build/client ./cmd/client
Done full node client building
go build -o ./build/light ./cmd/client/light
Done light node client building
go build -o ./build/tool ./cmd/tool
Done tool building
go build -o ./build/vm ./cmd/vm
Done vm building
~/go/src/github.com/seeleteam/go-seele$
```