### To add all files including deleted ones
* git add -A . 
* git add -u .
* git clean -f

None of these is actually working atm, work in progress lol

[what im trying now](https://stackoverflow.com/questions/45342654/failing-to-push-to-github-this-exceeds-githubs-file-size-limit):
```
git filter-branch --tree-filter 'rm -rf path/to/your/file' HEAD
git push
```

### Add to .gitignore files you don't want to version

[Example]()
