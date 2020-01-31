# Sharding

Seele sharding infrastructure greatly improves the scalability and efficiency of SeeleMainnet. An [introduction](https://medium.com/@SeeleTech/an-introduction-to-seeles-sharding-implementation-92ebf6e5aa53) is availble on medium explaining the details of how shards communicate via Seele's sharding protocol. SeeleMainnet currently consists of four shards: each shard containing its own chain and accounts. As a kind note, here are some notable implications, of sharding, for Seele's blockchain:

### Accounts

Each user account consists of: private-key, public-key, address. The shard of addresses are determined with the following logic:

```js
function shardOfAddress(address){
  var maxShard = 4
  var sum      = 0
  var buf = Buffer.from(address.substring(2), 'hex')
  for (const pair of buf.entries()) {if (pair[0] < 18){sum += pair[1]}}
  sum += (buf.readUInt16BE(18) >> 4)
  return (sum % maxShard) + 1
}

var address = '0x6b11bb0c9167ccd1bd9e4af80b997ed822e128a1'
console.log(shardOfAddress(address));
// prints 1
```

A smart contract also has an account, of which the address is revealed in the receipt of the transaction that deployed this contract. The shard of the contract address is also determined by the logic above. Thus all seele accounts are inherently "shardful", i.e. each account can only be used in a certain shard.

### Nodes

Refer to nodes for more details.

These "shardful" accounts are used in node configuration files. As implied in a node's configuration file, a node can only run on one shard: would maintain a **full chain** for the shard it's in, and three **light chains** for the other shards. A node can only mine and provide services based on the full chain.

The ```basic->coinbase``` field in the node's configuration file must belong to the shard specified in ```genesis->shard```. The coinbase here is the address to receive mining reward.

### Transactions

Intra-shard (sender and receiver are from the same shard) and cross-shard (sender and receiver are from different shards) transactions will be handled differently. When the sender and receiver are from the __**same**__ shard, the transaction is considered completed once it is packed into a block on the shard's chain **(15 seconds expected)**. It is, however, encouraged to wait until at least 10 blocks are mined after the block containing the transaction.

When sender and receiver are from **different** shards, the transaction is first packed into a block on the sender's shard's chain, a **debt** will be created in the receiver's shard's **debt pool**. The debt will be broadcast from debt pool to the receiver's shard's chain when at least 120 blocks are mined after its matching transaction is packed. The transaction is considered completed once the debt is packed into a block on the receiver's shard's chain. The whole process takes about 30 minutes.

### Contract

Refer to [contract](./../contract/contract.md) for more details.

Currently, the contract account and its interacting accounts must be from the same shard.

For example, someone writes a contract which can refund an external address from the contract's balance. If the external address is from an alien shard, the refund amount will be irreversibly lost.
