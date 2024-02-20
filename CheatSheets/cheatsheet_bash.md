## Useful bash commands

### Basics 

Let's start with head and tail:

```bash
head file.txt
```

will display the first 10 (?) lines of the file, and tail the last.

To change how many lines are displayed, e.g. 50, just type:

```bash
head -n 50 file.txt
```
and again same with tail.

If more commands are needed, you can display the whole file using "cat", and then "pipe" ("|", used to chain commands) the next command:

```bash
cat file.txt | head -n 50
```

```cat```'s equivalent for (bg)zipped files:

```bash
gunzip -c myfile.vcf.bgz
```

### File dimensions

Number of rows:

```bash
cat myfile.tsv | wc -l
```

Number of columns:

```bash
head -1 myfile.tsv | tr '\t' '\n' | wc -l
```

### Loop

```bash
for ((i=0; i <= 1000; i++)); do
    python $py_script $i 
done
```

### One-line loop

```bash
for i in {1..5}; do echo "Hi, $i"; done
```

Note the dollar sign in front of the i (```$i```)

### Find empty files in a dir

```bash
find /share/ScratchGeneral/anncuo/OneK1K/saige_eqtl/output/results/rare/ -empty 
```

and delete them:

```bash
find /share/ScratchGeneral/anncuo/OneK1K/saige_eqtl/output/results/rare/ -empty -exec rm {} \;
```

### Get permissions + file size in a directory

```bash
ls -lh
```

### Get file size of *all* files in a directory

The above only gives you the size at that current level, if you want to recursively get the size of all files in sub-directories as well, do:

```bash
du -h
```


### Compare files (check they are not identical)

```bash
cmp --silent SAIGE-QTL.sif.2 SAIGE-QTL.sif.3 || echo "files are different"
````

which prints ```files are different``` at the first byte difference.

### Complicated (for me) example

this command (used [here](https://github.com/annacuomo/TenK10K_analyses_HPC/blob/main/scripts/run_CRM.qsub)):

* opens the file,
* then using awk specifies it is comma "," separated, then selects rows where the 4th column is = 22
* then using sed selects the "1"st row
* awk again ("," separated again), then consider second column only to get tp the gene name

```bash
cat file.txt | awk -F ',' '$4 == 22' | sed -n 1p | awk -F "," '{print $2}'
```

## Random

Black: [The uncompromising code formatter](https://black.readthedocs.io/en/stable/).

To install, simply ```pip install black```.

Then, 

```bash
black my_script.py
``` 

to reformat.

## References

* [Cheatsheet](https://devhints.io/bash)
* [15 Special Characters You Need to Know for Bash](https://www.howtogeek.com/439199/15-special-characters-you-need-to-know-for-bash/)
