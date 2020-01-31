Seele Node
==========

Command Line Options
--------------------

::

   node -h
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

::

   node key -h
   generate a key pair and print them with hex values
    For example:
   node key --shard 1

   Usage:
     node key [flags]

   Flags:
     -h, --help         help for key
         --shard uint   shard number

::

   node start -h
   usage example:
           node.exe start -c cmd\node.json
           start a node.

   Usage:
     node start [flags]

   Flags:
         --accounts string   init accounts info
     -c, --config string     seele node config file (required)
     -h, --help              help for start
     -l, --light             whether start with light mode
     -t, --metrics           start metrics
     -m, --miner string      miner start or not, [start, stop] (default "start")
         --threads int       miner thread value (default 1)

::

   node validatekey -h
   For example:
               node.exe validatekey

   Usage:
     node validatekey [flags]

   Flags:
     -h, --help         help for validatekey
     -k, --key string   private key
