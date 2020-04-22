# Requirement

| Software | Version | Links                                                                    | Check           |
| -------- | ------- | ------------------------------------------------------------------------ | --------------- |
| MacOS    | 10.15+  | [Install](https://www.apple.com/macos/catalina/)                         | About This Mac  |
| nodejs   | 13.6.0+ | [Install](https://www.npmjs.com/get-npm)                                 | `node -v`       |
| npm      | 6.13.4+ | [Install](https://www.npmjs.com/get-npm)                                 | `npm -v`        |
| git      | 2.21.1+ | [Install](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) | `git --version` |
| go       | 1.13.6+ | [Install](https://golang.org/doc/install)                                | `go version`    |

\* Recommend 7g+ RAM space.

# Install

The package `seele-anchor-cli` is the command line tool used for utilizing STEM protocol. The other tool `snc` will be **optional** in near future once subchain protocol reaches its final stages.  

```bash
npm i seele-anchor-cli -g   # Install anc (subchain controller) globaly
anc -v                      # Verify installation
npm i seele-nicer-cli -g    # Install snc (go-seele helper) globaly
snc -v                      # Verify installation
```

# Start

## Create

Run the following commands to create a project and initialized in the `.subchain` folder in user's home directory. The `list` command allows switching between and deleting projects with options, use `anc list -h` for reference.

```bash
anc init -n mychain   # Create new subchain
anc list              # View available subchains
```

## Configure

There are four major configurable parts.

- **go-seele-sub**
  - **source code**
    - `~/go/src/github.com/seeleteam/go-seele-sub/core/genesis.go`:
    There is `func getStateDB` where you can edit Masteraccounts, the accounts with initial balances.
  - **node configuration files**
    - `~/.subchain/mychain/node`
    This directory contains your subchain node configuration files (and mainchain node configuration files if your using helper to test). For a subchain network to connect, the only parts allowed to be different between nodes:
    `basic.dataDirectory`

- **STEM contract**
  - **source code**
  - **constructer**
- **Controller**
  - **configuration file**
- **Helper**
  - **configuration file**


## Deploy

Use `snc` to start private mainchain net,   
```bash

snc init      # Download node binaries     
snc list      # List available node binaries

# Start mainchain
snc start -m
# Compile
anc make -c
# Deploy
anc make -d
# Show result
anc show
```


```bash
# Start subchain
snc start -s
#

```

# Use

## User



## Operator
