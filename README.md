# Seele Wiki

last updated nov 1, 2019

- Help improve this documentation by creating pull requests or issues on [github](https://github.com/seeleteam/seele-md)!
- Official [website](https://seelenet.com/)
- Communities managed by developers!
  - [telegram](https://t.me/seeletech)
  - [Twitter](https://twitter.com/SeeleTech)
  - [weibo](https://www.weibo.com/u/6561132287)
  - [linkedin](https://www.linkedin.com/company/seeletech)
  - [medium](https://medium.com/@SeeleTech)
  - [github](https://github.com/seeleteam)

![](RSC/Seele-logo.jpg)

# Updating [seele-md]( https://github.com/seeleteam/seele-md.git)

### Workflow

Clone, edit, push. Try with gitbook locally: ```npm install gitbook-cli -g``` then ```gitbook serve```. Navigate [website](https://seeletech.gitbook.io/wiki/) to see synchronization happening automatically.

### Format

Formatting mistakes will halt synchronization. Common possibilities:
- Incomplete `*[]()` in `STRUCTURE.md`

Gitbook checks `.gitbook.yaml` for
- Root directory: ex `./`
- Introduction page: ex `FIRSTPAGE.md`
- Side-bar structure: ex `STRUCTURE.md`

Since local gitbook doesn't read ```.gitbook.yaml``` as of v2.6.9, the names of the instruction page and side-bar structure has to be ```README.md``` and ```SUMMARY.md``` respectively. Also, to avoid compiling errors due to file lengths, the search plugin, ```lunr```, is disabled in ```book.json```.

`SUMMARY.md` must have the following format:

```bash
# Summary

## First Section Title

* [page1 title](page.md)
    * [subpage title](page.md)
* [page2 title](page.md)

## Second Section Title

* [page1 title](page.md)
```
