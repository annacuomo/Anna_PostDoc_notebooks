## Useful bash commands
### Basics 

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
### Loop
```
for ((i=0; i <= 1000; i++)); do
    python $py_script $i 
done
```

### Complicated (for me) example
this command (used [here](https://github.com/annacuomo/TenK10K_analyses_HPC/blob/main/scripts/run_CRM.qsub)):
* opens the file,
* then using awk specifies it is comma "," separated, then selects rows where the 4th column is = 22
* then using sed selects the "1"st row
* awk again ("," separated again), then consider second column only to get tp the gene name
```
cat file.txt | awk -F ',' '$4 == 22' | sed -n 1p | awk -F "," '{print $2}'
```
## References

[Cheatsheet](https://devhints.io/bash)

[15 Special Characters You Need to Know for Bash](https://www.howtogeek.com/439199/15-special-characters-you-need-to-know-for-bash/)
