### Create a new branch and go into it

```bash
git checkout -b name-of-branch
```

### Delete branch

```git branch -d name-of-branch``` or ```git branch -D name-of-branch``` if github refuses to help.

### Reset previous version

```bash
git reset --hard 9344d8b
```

ref: https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit

### To add all files including deleted ones

* `git add -A .`
* `git add -u .`
* `git clean -f`

None of these is actually working atm, work in progress lol

[what I'm trying now](https://stackoverflow.com/questions/45342654/failing-to-push-to-github-this-exceeds-githubs-file-size-limit), i.e.:

```bash
git filter-branch --tree-filter 'rm -rf path/to/your/file' HEAD
git push -f origin main
```

It worked!

### Another useful command

Error: ```fatal: The remote end hung up unexpectedly```

[Thread](https://stackoverflow.com/questions/15240815/git-fatal-the-remote-end-hung-up-unexpectedly):

```bash
git config http.postBuffer 524288000
```

### Add to .gitignore files you don't want to version

* [Example 1](https://github.com/annacuomo/TenK10K_analyses_HPC/blob/main/.gitignore)
* [Example 2](https://github.com/annacuomo/CellRegMap_analyses/blob/main/.gitignore)
