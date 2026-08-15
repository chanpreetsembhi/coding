
#### Creating a repository.

```
git init
```

#### Stage.

 - How to add file.

```
git add file.txt
```

- Check added file.

```
git status
```

#### Commit

```
git commit -m "commit message"
```
==**Note:** -m for message==

How to check all changes

```
git log

git log --oneline
```

---
## Revert Commit and push

```bash
git reset HEAD~1
```

==1 is for one commit==

Delete Un stage code

```bash
git reset --hard HEAD~1
```

Push Code

```bash
git push -f origin main
```