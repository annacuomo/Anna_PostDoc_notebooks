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


# Plotting

## show matrix

```Python
import matplotlib.pyplot as plt
plt.matshow(M)
```

## histogram

```Python
import matplotlib.pyplot as plt
plt.hist(y)
plt.show()
```

## scatter

```
import matplotlib.pyplot as plt
plt.scatter(x,y)
```

## barplot

https://www.geeksforgeeks.org/bar-plot-in-matplotlib/

## Venn

```Python
# pip install matplotlib-venn
from matplotlib_venn import venn2, venn2_circles, venn2_unweighted
from matplotlib_venn import venn3, venn3_circles
from matplotlib import pyplot as plt
%matplotlib inline
venn2(subsets = (30, 10, 5), set_labels = ('Group A', 'Group B'))
```

Slightly more complex example for neuroseq paper (Studies overlap figure; [Fig. 3A](https://github.com/single-cell-genetics/singlecell_neuroseq_paper/blob/main/plotting_notebooks/Figure_3/Figure_3a.ipynb))

## save plot

```Python
plt.savefig("fig.pdf")
```

# Resources

* [Pandas illustrated](https://betterprogramming.pub/pandas-illustrated-the-definitive-visual-guide-to-pandas-c31fa921a43)
* [Numpy illustrated](https://betterprogramming.pub/numpy-illustrated-the-visual-guide-to-numpy-3b1d4976de1)
