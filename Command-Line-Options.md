# Command Line Options

## Client
```
$ client --help
NAME:
   client - interact with node process

USAGE:
   client [global options] command [command options] [arguments...]

COMMANDS:
     call              call contract
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
     savekey           save private key to a keystore file
     sendtx            send transaction to node
     sign              generate a signed transaction and print it out
     subchain          system sub chain commands
     help, h           Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --help, -h  show help
```
```
$ client call --help
NAME:
   client call - call contract

USAGE:
   client call [command options] [arguments...]

OPTIONS:
   --address value, -a value  address for client to request (default: "127.0.0.1:8027")
   --height value             block height (default: -1)
   --payload value            transaction payload info
   --to value                 to address
```
```
$ client domain --help
NAME:
   client domain - system domain name commands

USAGE:
   client domain command [command options] [arguments...]

COMMANDS:
     owner     get the domain name owner
     register  register a domain name

OPTIONS:
   --help, -h  show help
```
```
$ client dumpheap --help
NAME:
   client dumpheap - dump heap for profiling, return the file path

USAGE:
   client dumpheap [command options] [arguments...]

OPTIONS:
   --address value, -a value  address for client to request (default: "127.0.0.1:8027")
   --file value               heap dump file name, defualt heap.dump (default: "heap.dump")
   --gc                       GC before heap dump, defualt false
```

## Node
```
$ node --help
use "node help [<command>]" for detailed usage

Usage:
  node [command]

Available Commands:
  help        Help about any command
  key         generate a key pair with specified shard number
  start       start the node of seele
  validatekey validate the private key and generate its public key

Flags:
  -h, --help   help for node

Use "node [command] --help" for more information about a command.
```
```
$ node key --help
generate a key pair and print them with hex values
 For example:
node key --shard 1

Usage:
  node key [flags]

Flags:
  -h, --help         help for key
      --shard uint   shard number
```
```
node start --help
usage example:
                node.exe start -c cmd\node.json
                start a node.

Usage:
  node start [flags]

Flags:
      --accounts string   init accounts info
  -c, --config string     seele node config file (required)
  -h, --help              help for start
  -t, --metrics           start metrics
  -m, --miner string      miner start or not, [start, stop] (default "start")
      --threads uint      miner thread value (default 1)
```
```
node validatekey --help
For example:
                        node.exe validatekey

Usage:
  node validatekey [flags]

Flags:
  -h, --help         help for validatekey
  -k, --key string   private key
```