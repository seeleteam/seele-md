# How To Send Debt

- The different between transaction and debt is that transaction happened in two accounts on the same shard,debt happened in two accounts on different shards.

You should have two accounts on different shards.[Here](How-To-Create-An-Account.html) will help you to get the accounts.

## 1. Transfer

  - You need a rich account to transfer money (for example, 100000 fan) from shard1 account to shard2 account.
```
shard1 account: 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21
shard2 account: 0xd228e1dd02bdce9656b8e195a77e0da0b70daea1
```

```js
// Request
client sendtx --from .keystore-shard1-0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21 --to 0xd228e1dd02bdce9656b8e195a77e0da0b70daea1 --amount 100000
Please input your key file password:
account: 0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21, transaction nonce: 1
transaction sent successfully
{
        "Hash": "0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1",
        "Data": {
                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "To": "0xd228e1dd02bdce9656b8e195a77e0da0b70daea1",
                "Amount": 100000,
                "AccountNonce": 1,
                "GasPrice": 10,
                "GasLimit": 42000,
                "Timestamp": 0,
                "Payload": ""
        },
        "Signature": {
                "Sig": "CyeAgd+RgPnb27XJXOWT8CnbtwSmyDMJ6oIEFKDiZ5UWIv7ImX0MRsf615BnwxxHt/A0P1OPQ0MY01LC3sWAPwA="
        }
}

It is a cross shard transaction, its debt is:
{
        "Hash": "0x5ecc232012ae6a1cfe9ab88ca38583872c0bc0b2e1da4e987f5dc98cbde8c0f1",
        "Data": {
                "TxHash": "0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1",
                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                "Nonce": 1,
                "Account": "0xd228e1dd02bdce9656b8e195a77e0da0b70daea1",
                "Amount": 100000,
                "Price": 10,
                "Code": ""
        }
}
```

  - Query the transfer result with the tx `Hash` on shard 1.

```
client getreceipt --hash 0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1
{
        "contract": "0x",
        "failed": false,
        "poststate": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "result": "0x",
        "totalFee": 0,
        "txhash": "0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1",
        "usedGas": 42000
}
```

The result of `"failed": false`row, indicating that the transfer was successful.
By the way, if tx is not packed by the miner or the miner is packing, you may see`get error when call rpc leveldb: not found`. Don't worry, just wait for servals seconds, or you can use `client gettxbyhash` to query tx `status`.

## 2. Get debt

  - When the transaction got over 120 blocks confirmed, you will get the pending debt on shard 2.

```
client getdebts --address 127.0.0.1:8028
[
        {
                "Data": {
                        "Account": "0xd228e1dd02bdce9656b8e195a77e0da0b70daea1",
                        "Amount": 100000,
                        "Code": "",
                        "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "Nonce": 1,
                        "Price": 10,
                        "TxHash": "0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1"
                },
                "Hash": "0x5ecc232012ae6a1cfe9ab88ca38583872c0bc0b2e1da4e987f5dc98cbde8c0f1"
        }
]
```

  - Few second later, the debt will be packed by shard 2 new block.

```
client getdebtbyhash --hash 0x5ecc232012ae6a1cfe9ab88ca38583872c0bc0b2e1da4e987f5dc98cbde8c0f1 --address 127.0.0.1:8028
{
        "blockHash": "0x02276e91e7e69fa133c614057728379cb0587e1d750941799ed03a665d9377ad",
        "blockHeight": 478,
        "debt": {
                "Data": {
                        "Account": "0xd228e1dd02bdce9656b8e195a77e0da0b70daea1",
                        "Amount": 100000,
                        "Code": "",
                        "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                        "Nonce": 1,
                        "Price": 10,
                        "TxHash": "0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1"
                },
                "Hash": "0x5ecc232012ae6a1cfe9ab88ca38583872c0bc0b2e1da4e987f5dc98cbde8c0f1"
        },
        "debtIndex": 0,
        "status": "block"
}
```

```
client getblock --height 478 -f=true  --address 127.0.0.1:8028
{
        "debts": [
                {
                        "Data": {
                                "Account": "0xd228e1dd02bdce9656b8e195a77e0da0b70daea1",
                                "Amount": 100000,
                                "Code": "",
                                "From": "0x4c10f2cd2159bb432094e3be7e17904c2b4aeb21",
                                "Nonce": 1,
                                "Price": 10,
                                "TxHash": "0x07d874cad8305bdcb813221425725d0c4ce651a20420e98cc0e911e181ae1da1"
                        },
                        "Hash": "0x5ecc232012ae6a1cfe9ab88ca38583872c0bc0b2e1da4e987f5dc98cbde8c0f1"
                }
        ],
        "hash": "0x02276e91e7e69fa133c614057728379cb0587e1d750941799ed03a665d9377ad",
        "header": {
                "Consensus": 0,
                "CreateTimestamp": 1542770231,
                "Creator": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831",
                "DebtHash": "0xace17fc0943681060586db3ee72302ed1fe439213f3f9db419fbf54a65afb431",
                "Difficulty": 100,
                "ExtraData": "",
                "Height": 478,
                "PreviousBlockHash": "0x0075f608519738e0f81853d8551ec7b88ebc442d5d560ca916fdddb57b326f35",
                "ReceiptHash": "0xaad5b991fd1c7486b2ae20d2cafc7a75e0330a11f065c5d20a8f402cd02c1f17",
                "StateHash": "0xbe46b414d95179e8b14414c5356d0cedce11cf66b5fbaf989c64a5df5f95a303",
                "TxDebtHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "TxHash": "0xc44264dfe45bb09b09df9fa17c7b1848319d644a9ae392923619a6520bf4ac0f",
                "Witness": "MTE3ODU2OTQ0MTA4ODQ1MDUzMjU="
        },
        "totalDifficulty": 47900,
        "transactions": [
                {
                        "accountNonce": 0,
                        "amount": 150000000,
                        "from": "0x0000000000000000000000000000000000000000",
                        "gasLimit": 0,
                        "gasPrice": 0,
                        "hash": "0x715a0ac01ea7cb04af94a722dce3167979017f719dbeb58590f365e89fcced2a",
                        "payload": "",
                        "to": "0x0ea2a45ab5a909c309439b0e004c61b7b2a3e831"
                }
        ],
        "txDebts": []
}
```

  - Confirm the shard 2 account balance.

```
client getbalance --account 0xd228e1dd02bdce9656b8e195a77e0da0b70daea1 --address 127.0.0.1:8028
{
        "Account": "0xd228e1dd02bdce9656b8e195a77e0da0b70daea1",
        "Balance": 100000
}
```
