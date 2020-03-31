# Dev

---

## Setup

### Components

>The subchain controller, `seele-anchor-cli` (short as 'anc'),  is consist of many components that require tuning. The following is the project's major dependencies.

```bash
seele-anchor-cli             // employ, call subchain contracts
├── seele-stemsdk-javascript // subchain node api, keys, tx
└── seele-contract-core      // compile, deploy contracts
    └── seele-sdk-javascript // mainchain node api, keys, tx
```

### Environment

> Place the components in your project root. In every component's root directory, run `npm link`, then in `seele-anchor-cli` run `npm i`. Your changes in `seele-stemsdk-javascript` should reflect in `seele-anchor-cli`.

```bash
project_root
├── seele-anchor-cli
├── seele-contract-core
└── seele-stemsdk-javascript
```

---

## Testing

### Using snc

This is a tool used for fast access to a subchain-mainchain-private environment. In case someone is curious, `snc` stands for Seele Nice Commandline.

```bash
# 1. Initiate config directory in .subchain/node
snc init
# 2. After configuring, use the following
snc start         # start nodes
snc list          # list all running nodes
snc list --l      # list all running nodes in more details
snc kill          # kiill all nodes
snc clean         # clears ~/.seele dir and ~/seeleTemp
snc node version  # check node version
snc node compile mainchain  # replace mainchain nodes
snc node compile subchain   # replace subchain nodes
```

The `./test/node` directory contains the configuration file `nodecliconfig.json` for `snc start`, use the `nodecliconfig.json_bac` in case your editor or terminal crashes. The `nodecliconfig.json` is configured as follows:
- main-conf: array of mainchain configs to start
- stem-conf: array of subchain configs to start
- main-info: cli filled after `snc start`
- stem-info: cli filled after `snc start`

The `./test/node/cli.js` file contains the code for this tool. The function defined in this file, `run()`, wraps regular bash statements. With this, it would easy to modify the too drastic `"rm -rf ~/.seele; rm -rf seeleTemp;"` command to **NOT DELETE** all your node database that `snc clean` runs.

### Using anc

Most `anc` command are introduced in [user guide](./0-user.md), using the `-h` option in anc and you may find other helpful options. One common one is the following:

```bash
# Add -p option to deposite for other accounts instead of just yourself
# Add -n option to self configure nonce
# Similarly for adtx, send
anc trade in ...\
-p 0xd345ed9cdfe3fc27a0382c5dbcaeec17836343a75e00cac37a81660714af8260
-n 11
```

Refer to the `scriptTest.js` and `flow.test.js`, in the `./test` directory to know how to write your own test scripts in javascript, or `scriptTest.sh` to write in bash.

Running `npm test` would run all files in `./test` directory with `.test.js` filename extesion, use `.only` and `.skip` to only run a single test, or selectively skip tests.
