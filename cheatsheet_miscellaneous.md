## R

### to read in a compressed file with a .gz extension
df = read.csv(gzfile(filename), sep="\t")

## python

### equivalent to gsub in python:

```
import re
re.sub("_", "-", mystring)
```
