# General Python

## correlation (cor in R)

```Python
import numpy as np
np.corrcoef[1,0] = np.corrcoef[0,1]
```

## equivalent to gsub in python

```Python
import re
mynewstring = re.sub("_", "-", mystring)
```

or

```Python
mynewstring = mystring.replace("_", "-")
```

## permuting / shuffling vector

```Python
from sklearn.utils import shuffle
vec_perm = shuffle(vec, random_state=0)
```

## read arguments in .py script

Option 1:

```Python
import sys
chrom = str(sys.argv[1])
```

Option 2:

```Python
import click
@click.command()
@click.option("--chrom", required=True, help="More info here")
def main(
    chrom: str,
):
```

## check if file exists

```Python
import os
os.path.exists(path-i-am-checking)
```

## if path doesn't exist (check as above), creata new dir

```Python
if os.path.exists(path) == False:
	os.makedirs(path)
```

## list files in a directory

```Python
import os
files = os.listdir(mydir)
```

## list files with a pattern

```
import glob
files = glob.glob("*.tsv")
```

## time of running something

```Python
import time
start_time = time.time()
main()
print("--- %s seconds ---" % (time.time() - start_time))
```

## to check version of python package

```Python
import cellregmap as crm
crm.__version__
```

## python try except

https://www.w3schools.com/python/python_try_except.asp


# Resources

* [Pandas illustrated](https://betterprogramming.pub/pandas-illustrated-the-definitive-visual-guide-to-pandas-c31fa921a43)
* [Numpy illustrated](https://betterprogramming.pub/numpy-illustrated-the-visual-guide-to-numpy-3b1d4976de1)
