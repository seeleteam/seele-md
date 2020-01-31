```yml
Title: Seele HD Wallet Specification
Author: Tinoma
Created: 2020-01-15
```

## PURPOSE

For compatibility between HD (Hierarchical Deterministic) Wallets that follows the [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) schema, this document aims to specify the rules of address discovery for supporting Seele.

## SCHEME

- Specification:
| Field         | Value | Comments                                                                          |
| ------------- | ----- | --------------------------------------------------------------------------------- |
| purpose       | 44'   | BIP44 purpose.                                                                    |
| coin_type     | 456'  | Registered [here](https://github.com/satoshilabs/slips/blob/master/slip-0044.md). |
| account       | 0'    | Assume first account.                                                             |
| change        | 0     | Assume external chain.                                                            |
| address_index | x     | Find the first address encountered in each shard. Four addresses in total.        |

- Example:
```javascript
{
    mnemonic: "hurdle broccoli blast rug mixed expire soldier able maze heavy jeans equip"
}
// According to the specification above,
// among the addresses discovered as shown below:
// address[1] is chosen for shard 1
// address[3] is chosen for shard 2
// address[2] is chosen for shard 3
// address[0] is chosen for shard 4
```
| Path                  | Address                    | Shard |
| --------------------- | -------------------------- | ----- |
| **m/44'/456'/0'/0/0** | **0x...de48c8d41ff280091** | **4** |
| **m/44'/456'/0'/0/1** | **0x...722a597a01aa80d01** | **1** |
| **m/44'/456'/0'/0/2** | **0x...68ae8b413efb55891** | **3** |
| **m/44'/456'/0'/0/3** | **0x...3be0587deb333c771** | **2** |
| m/44'/456'/0'/0/4     | 0x...c9f82c473615956c1     | 3     |
| m/44'/456'/0'/0/5     | 0x...076e71ade650ec5d1     | 2     |
| m/44'/456'/0'/0/6     | 0x...49994f209553e24c1     | 1     |
| ...                   | ...                        | ...   |

- JS pseudo code:

  ```javascript
  const bip32               = require('bip32');
  const bip39               = require('bip39');
  const bip44               = require('bip44');
  // return seele address from privateKey
  function addressOfprivateKey(privateKey){...}
  // return seele shard from address
  function shardOfAddress(address){...}
  //
  function accountFromWord(word){
    var seed = bip39.mnemonicToSeedSync(word).toString('hex')
    return accountFromSeed(seed)
  }

  function accountFromSeed(seed){
    var seedbuf = Buffer.from(seed, 'hex')
    var rootobj = bip32.fromSeed(seedbuf)
    var account = []
    for ( var shard = 1 ; shard <= 4 ; shard++ ){
      var addr = { p: null, a: null, s:null }
      var i = 0
      while( addr.s != shard ){
        addr.i = i
        addr.p = '0x' + rootobj.derivePath(`m/44'/${bip44.SEELE.index}'/0'/0/${i}`).privateKey.toString('hex')
        addr.a = addressOfprivateKey(addr.p)
        addr.s = shardOfAddress(addr.a)
        i++;
      }
      account.push(addr)
    }
    return account
  }
  const mnemonic  = "hurdle broccoli blast rug mixed expire soldier able maze heavy jeans equip"
  const account   = accountFromWord(mnemonic)
  console.log(account);
  // expects
  // [
  //   {
  //     s: 1,
  //     p: '0x6f713371e6d5d513fe66b9f6f5974aec46c0a9a5fdd49d24b48128519e6efb1e',
  //     a: '0x5fc511565316e45e84f3383722a597a01aa80d01',
  //     i: 1
  //   },
  //   {
  //     s: 2,
  //     p: '0xa457b3adedecddacfa1b08f97a6ed8e25b5ed4b1a9692d725c5ed87bd80e36a1',
  //     a: '0xac5d5a1fc5ebbea4f2044b33be0587deb333c771',
  //     i: 3
  //   },
  //   {
  //     s: 3,
  //     p: '0x19350808989722ee84dda5fe20686ca8af5cf7671e5193d3e0cddf039901a3da',
  //     a: '0x14130ff8b350230ca326fd468ae8b413efb55891',
  //     i: 2
  //   },
  //   {
  //     s: 4,
  //     p: '0xb168d0823a616d111ba4abf4c27bb9331d3326dedde270d9b0bc77b767c6744e',
  //     a: '0x05df8b2bf801195092f218dde48c8d41ff280091',
  //     i: 0
  //   }
  // ]
  ```

## REFERENCE

- [EIP601](https://eips.ethereum.org/EIPS/eip-601) Ethereum hierarchy for deterministic wallets
- [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) Multi-Account Hierarchy for Deterministic Wallets
- [BIP43](https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki) Purpose Field for Deterministic Wallets
- [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) Mnemonic code for generating deterministic keys
- [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) Hierarchical Deterministic Wallets
