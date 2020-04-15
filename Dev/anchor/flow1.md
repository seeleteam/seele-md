# Requirement

| Software | Version | Links                                                                    | Check           |
| -------- | ------- | ------------------------------------------------------------------------ | --------------- |
| MacOS    | 10.15+  | [Install](https://www.apple.com/macos/catalina/)                         | About This Mac  |
| nodejs   | 13.6.0+ | [Install](https://www.npmjs.com/get-npm)                                 | `node -v`       |
| npm      | 6.13.4+ | [Install](https://www.npmjs.com/get-npm)                                 | `npm -v`        |
| git      | 2.21.1+ | [Install](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) | `git --version` |
| go       | 1.13.6+ | [Install](https://golang.org/doc/install)                                | `go version`    |

\* Recommend 7g+ RAM space.

# Setup

Run the following commands in terminal:

```bash
# Install anc (subchain controller) globaly
npm i seele-anchor-cli -g
# Verify installation
anc -v

# Install snc (go-seele helper) globaly
npm i seele-nicer-cli -g
# Verify installation
snc -v

# Navigate to seeleteam's project directory
cd ~/go/src/github.com/seeleteam/
# Clone subchain project
git clone http://github.com/seeleteam/go-seele-sub.git
# Clone mainchain project
git clone http://github.com/seeleteam/go-seele.git
# Rename mainchain project
mv go-seele go-seele-main
```

# Start

Edit crontab

```bash
# Edit
crontab -e
# Add line: * * * * * anc keep -l
# List
crontab -l
```



```bash

```

# Use
