# Editing seele-md 

### Workflow

Clone, edit, push. 
Open [edit window](https://app.gitbook.com/@seeletech/spaces) and [view window](https://seeletech.gitbook.io/wiki/) to see synchronization happening automatically.

### Format 

Formatting Errors will cause errors without details at synchronization. Common possibilities:
- SUMMARY.md not having the complete `*[]()` format

Gitbook looks at `.gitbook.yaml` for
- root directory: ex `./`
- introduction page: ex `INTRODUCTION.md`
- side bar structure: ex `SUMMARY.md`

SUMMARY.md must have the following format:

```markdown
# Summary

## First Section Title

* [page1 title](page.md)
    * [subpage title](page.md)
* [page2 title](page.md)

## Second Section Title

* [page1 title](page.md)
```


