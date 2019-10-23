# Updating [seele-md]( https://github.com/seeleteam/seele-md.git) 

### Workflow

Clone, edit, push. 
Open [edit window](https://app.gitbook.com/@seeletech/spaces) and [view window](https://seeletech.gitbook.io/wiki/) to see synchronization happening automatically.

### Format 

Formatting mistakes will halt synchronization. Common possibilities:
- Incomplete `*[]()` in `SUMMARY.md`

Gitbook checks `.gitbook.yaml` for
- Root directory: ex `./`
- Introduction page: ex `INTRODUCTION.md`
- Side-bar structure: ex `SUMMARY.md`

`SUMMARY.md` must have the following format:

```markdown
# Summary

## First Section Title

* [page1 title](page.md)
    * [subpage title](page.md)
* [page2 title](page.md)

## Second Section Title

* [page1 title](page.md)
```


