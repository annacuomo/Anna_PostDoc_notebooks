### To add all files including deleted ones
* git add -A . 
* git add -u .
* git clean -f

None of these is actually working atm, work in progress lol

[what I'm trying now](https://stackoverflow.com/questions/45342654/failing-to-push-to-github-this-exceeds-githubs-file-size-limit), i.e.:
```
git filter-branch --tree-filter 'rm -rf path/to/your/file' HEAD
git push -f origin main
```
It worked!

[Another useful thread](https://stackoverflow.com/questions/15240815/git-fatal-the-remote-end-hung-up-unexpectedly)

### Add to .gitignore files you don't want to version

* [Example 1](https://github.com/annacuomo/TenK10K_analyses_HPC/blob/main/.gitignore)
* [Example 2](https://github.com/annacuomo/CellRegMap_analyses/blob/main/.gitignore)
