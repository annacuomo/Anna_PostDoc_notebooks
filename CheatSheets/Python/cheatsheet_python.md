# Python

## Pandas

### initiate pandas data frame

```Python
import pandas as pd
data = {"cell": cells, "cluster": clusters}
df0 = pd.DataFrame(data, columns=cols, index=idx)
```

### subset data frame based on a column

```Python
cov_naive_Bcell = cov_df[cov_df['predicted.celltype.l2'] == 'B naive']
```

### but if the column is an index instead:

```Python
df_subset = df[df.index =="XYZ"]
```

### select specific column(s)

```Python
df[["colname"]]
```

or

```Python
df.loc[:,["col1","col2"]]
```

### select rows based on column values

```Python
df_sel = df.loc[df['col'].isin(selected_values)]
```

### reorder columns Pandas df (alphabetically)

```Python
df = df.reindex(sorted(df.columns), axis=1)
```

for rows,

```Python
df = df.reindex(sorted(df.index), axis=0)
```

### NAs (pandas)

https://datatofish.com/check-nan-pandas-dataframe/

### join using Pandas

https://sparkbyexamples.com/pandas/pandas-join-explained-with-examples/

### confusion matrix from df using pandas

```Python
confusion_matrix = pd.crosstab(df['y_actual'], df['y_predicted'], rownames=['Actual'], colnames=['Predicted'])
print(confusion_matrix)
```

### equivalent to table in python (pandas DataFrame)

```Python
df.colunm_name.value_counts()
```

## scanpy / anndata

### create anndata object from X matrix

```Python
import anndata as ad
adata = ad.AnnData(X=X, obs=obs, var=var, dtype='float')
```

## general

### correlation (cor in R)

```Python
import numpy as np
np.corrcoef[1,0] = np.corrcoef[0,1]
```

### equivalent to gsub in python

```Python
import re
mynewstring = re.sub("_", "-", mystring)
```

or

```Python
mynewstring = mystring.replace("_", "-")
```

### read arguments in .py script

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

### check if file exists

```Python
import os
os.path.exists(path-i-am-checking)
```

### time of running something

```Python
import time
start_time = time.time()
main()
print("--- %s seconds ---" % (time.time() - start_time))
```

### if path doesn't exist (check as above), creata new dir

```Python
if os.path.exists(path) == False:
	os.makedirs(path)
```

### to check version of python package

```Python
import cellregmap as crm
crm.__version__
```

### python try except

https://www.w3schools.com/python/python_try_except.asp


## Plotting

### show matrix

```Python
import matplotlib.pyplot as plt
plt.matshow(M)
```

### histogram

```Python
import matplotlib.pyplot as plt
plt.hist(y)
plt.show()
```

### scatter

```
import matplotlib.pyplot as plt
plt.scatter(x,y)
```

### Venn

```Python
# pip install matplotlib-venn
from matplotlib_venn import venn2, venn2_circles, venn2_unweighted
from matplotlib_venn import venn3, venn3_circles
from matplotlib import pyplot as plt
%matplotlib inline
venn2(subsets = (30, 10, 5), set_labels = ('Group A', 'Group B'))
```

Slightly more complex example for neuroseq paper (Studies overlap figure; [Fig. 3A](https://github.com/single-cell-genetics/singlecell_neuroseq_paper/blob/main/plotting_notebooks/Figure_3/Figure_3a.ipynb))

### save plot

```Python
plt.savefig("fig.pdf")
```

## Resources

* [Pandas illustrated](https://betterprogramming.pub/pandas-illustrated-the-definitive-visual-guide-to-pandas-c31fa921a43)
* [Numpy illustrated](https://betterprogramming.pub/numpy-illustrated-the-visual-guide-to-numpy-3b1d4976de1)
