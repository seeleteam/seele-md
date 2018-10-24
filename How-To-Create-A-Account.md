# How To Create A Account

- The commands mentioned next, if you don't know how to use it, please check the [Seele documentation](../index.html) in detail.

## Create account by Seele Node

- For convenience, A is From address on shard 1.

  generate A account:

```js
// Request
node key --shard 1

// Response
public key:  0xb4153ca4090a11af1984cdf20b0d0cbed5ff97a1
private key: 0x28f74ba46964f6bd09be55654d58eacea72b57449d5636a8c347c15a9104f
```

## Create account by Seele Client

- For convenience, A is From address on shard 1.

  generate A account:

```js
// Request
client key --shard 1

// Response
public key:  0xb4153ca4090a11af1984cdf20b0d0cbed5ff97a1
private key: 0x28f74ba46964f6bd09be55654d58eacea72b57449d5636a8c347c15a9104f
```

## Generate keyfile for account

- Sometimes you may need to generate the from address keyfile, command:
    
```js
// Request
client savekey --privatekey 0x28f74ba46964f6bd09be55654d58eacea72b57449d5636a8c347c15a9104fbc3 --file .keystore-shard1

// Response
Password:
Repeat password:
store key successful
```
