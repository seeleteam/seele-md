# Seele API

Seele's API is comprised of remote and local functions:

### Remote

- Served remotely by a go-seele node, queried through http requests in json-rpc format, wrapped by language specific SDK's.
- references:
  - [JSON-RPC | Node Version <= v1.2.7](./RPC127.md)
  - [JSON-RPC | Node Version >= v1.3.0](./RPC.md)
- examples: getBalance, addTx, ...

### Local

- Executed locally, implemented by language specific SDK's.
- references:
  - [seele-sdk-javascript](https://seele.pro/docs/jsdoc/index.html) (v1.0.5)
  - [seele-sdk-java](https://github.com/seeleteam/seele-sdk-java) (beta)
  - seele-sdk-python (TODO)
  - seele-sdk-go (TODO)
- examples: signTx, decryptKeyfile, ...

### Javascript SDK

Seele currently has two javascript SDKs: [seeleteam.js](https://www.npmjs.com/package/seeleteam.js) and [seele-sdk-javascript](https://www.npmjs.com/package/seele-sdk-javascript). [SeeleWallet](https://github.com/seeleteam/SeeleWallet/releases/latest) will switch to [seele-sdk-javascript](https://www.npmjs.com/package/seele-sdk-javascript), SeeleAnchor(subchain gui) will be developed with [seele-sdk-javascript](https://www.npmjs.com/package/seele-sdk-javascript), [seeleteam.js](https://www.npmjs.com/package/seeleteam.js) will probably be deprecated but not in near future. Here's a comparison:

| feature               |   seeleteam.js    | seele-sdk-javascript |
| --------------------- |:-----------------:|:--------------------:|
| rpc: node <=v1.2.7    | &#x2713;(v1.6.8+) |  &#x2713;(v1.1.0+)   |
| rpc: node >=v1.3.0    | &#x2713;(v2.0.0+) |  &#x2713;(v2.1.0+)   |
| Key functions         |     &#x2713;      |       &#x2713;       |
| Tx functions          |     &#x2713;      |       &#x2713;       |
| Keystore functions    |                   |       &#x2713;       |
| Mnemonic & HD         |                   |       &#x2713;       |
| Contract Support      |                   |       &#x2713;       |
| Subscription          |                   |       &#x2713;       |
| Doc (jsdoc or sphinx) |                   |       &#x2713;       |
| Testing (mocha)       |                   |       &#x2713;       |
