
# Configuration

## Brief

- `compiler` [TODO] choose which compiler to use
- `transactions` object of constructors arranged by contract file name
  - `limit` mainchain transaction limit
  - `depth` how many blocks to wait for to count transactions as complete in mainchain
  - `privateKey` default privatekey to use for all transactions with mainchain
  - `fromAddress` default address to use for all transactions with mainchain
- `subchain` subchain configs:
  - `limit` subchain transaction limit
  - `depth` how many blocks to wait for to count transactions as complete in subchain
  - `node` http-address to use for subchain
- `shard` object of http-address of mainchain arranged by shard
  - `1` http-address to use for shard 1 of mainchain
  - `2` http-address to use for shard 2 of mainchain
  - `3` http-address to use for shard 3 of mainchain
  - `4` http-address to use for shard 4 of mainchain
- `constructors`
  - `"StemRootchain.sol"` The constructor for subchain contract
- `addressBook` object of contract-address arranged by contract file name
  - `"StemRootchain.sol"` The subchain address

## More


### `constructors`

The `"StemRootchain.sol"` field in `constructors` is matched to an array:
- [0] abi array
- [1] value array
- [2] transaction amount when deploy

This is exactly as what [seele-cotnract-core](https://www.npmjs.com/package/seele-contract-core) requires. Refer to the example in appendix.

- `_subchainName`, (`bytes32`): strings hashed into
- `_genesisInfo`, (`bytes32[]`):
  - filled by `anc fill` option
- `_staticNodes`, (`bytes32[]`):
- `_creatorDeposit`, (`uint256`):
- `_ops`, (`address[]`):
  - `[0]` mintAccount (refer to StemCreation.sol)
  - `[1]` meltAccount (refer to StemCreation.sol)
- `_opsDeposits`, (`uint256[]`):
  - `[0]`: 0
  - `[1]`: 0
- `_refundAccounts`, (`address[]`):
  - `[0]`: `"0x0000000000000000000000000000000000000000"`
  - `[1]`: `"0x0000000000000000000000000000000000000000"`

### `addressBook`

Delete the `"StemRootchain.sol"` field in `addressBook` and re-run `anc make -d` to re-deploy the StemRootchain.sol contract which essentially reuses the other addresses and updates the contract you're now focused on. The `"StemRootchain.sol"` field will contain the contract-address that all anc action assumes.

Similarly, to change more parameters like challenge period and relay periods, you would change them in the StemRootchain.sol file in your subchain project's `./src` directory, then you can delete the `"StemCreation.sol"` field along with `"StemRootchain.sol"` field to re-deploy your subchain.

### `genesis`

`"rootaccounts"`: 
`"validators"`: equal to the constructors

# Appendix

```json
"StemRootchain.sol": [
  [
    {
      "name": "_subchainName",
      "type": "bytes32"
    },
    {
      "name": "_genesisInfo",
      "type": "bytes32[]"
    },
    {
      "name": "_staticNodes",
      "type": "bytes32[]"
    },
    {
      "name": "_creatorDeposit",
      "type": "uint256"
    },
    {
      "name": "_ops",
      "type": "address[]"
    },
    {
      "name": "_opsDeposits",
      "type": "uint256[]"
    },
    {
      "name": "_refundAccounts",
      "type": "address[]"
    }
  ],
  [
    "0x416e6e6965",
    [
    ],
    [
      "0x1071052039"
    ],
    "1",
    [
      "0x0adB61076AF511b8bAdb1264477ba4Be3D302D86",
      "0xfb96c3011d73fecB3F75FFAAac8F02cf83D59298",
      "0xca35b7d915458ef540ade6068dfe2f44e8fa733c",
      "0x627306090abab3a6e1400e9345bc60c78a8bef57",
      "0x4b0897b0513fdc7c541b6d9d7e929c4e5364d2db",
      "0x583031d1113ad414f02576bd6afabfb302140225"
    ],
    [
      "0",
      "0",
      "100",
      "100",
      "100",
      "100"
    ],
    [
      "0x0000000000000000000000000000000000000000",
      "0x0000000000000000000000000000000000000000",
      "0x3f78b08f45730f59a15319af41ba5a750021c541",
      "0x3f78b08f45730f59a15319af41ba5a750021c541",
      "0x3f78b08f45730f59a15319af41ba5a750021c541",
      "0x3f78b08f45730f59a15319af41ba5a750021c541"
    ]
  ],
  10000
]
```
