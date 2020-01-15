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
        addr.p = '0x' + rootobj.derivePath(`m/44'/${bip44.SEELE.index}'/0'/0/${i}`).privateKey.toString('hex')
        addr.a = addressOfprivateKey(addr.p)
        addr.s = shardOfAddress(addr.a)
        i++;
      }
      account.push(addr)
    }
    return account
  }
  const mnemonic = "hurdle broccoli blast rug mixed expire soldier able maze heavy jeans equip"
  accountFromWord(mnemonic)
  ```

## REFERENCE

- [EIP601](https://eips.ethereum.org/EIPS/eip-601) Ethereum hierarchy for deterministic wallets
- [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) Multi-Account Hierarchy for Deterministic Wallets
- [BIP43](https://github.com/bitcoin/bips/blob/master/bip-0043.mediawiki) Purpose Field for Deterministic Wallets
- [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) Mnemonic code for generating deterministic keys
- [BIP32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki) Hierarchical Deterministic Wallets
