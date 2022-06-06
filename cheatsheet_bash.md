## Useful bash commands
### Am pretty average at bash commands at the moment, but can always try to get better!

Let's start with head and tail:
```
head file.txt
```
will display the first 10 (?) lines of the file, and tail the last.

To change how many lines are displayed, e.g. 50, just type:
```
head -n 50 file.txt
```
and again same with tail.

If more commands are needed, you can display the whole file using "cat", and then "pipe" ("|", used to chain commands) the next command:
```
cat file.txt | head -n 50
```

### Complicated example
this 
* opens the file,
* then using awk specifies it is comma "," separated, then selects rows where the 4th column is = 22
* then using sed selects the "1"st row
```
cat file.txt | awk -F ',' '$4 == 22' | sed -n 1p
```
## References

[15 Special Characters You Need to Know for Bash](https://www.howtogeek.com/439199/15-special-characters-you-need-to-know-for-bash/)
