## Python

#### initiate pandas data frame
```
import pandas as pd
data = {"cell": cells, "cluster": clusters}
df0 = pd.DataFrame(data, columns=cols, index=idx)
```

#### subset data frame based on a column
```
cov_naive_Bcell = cov_df[cov_df['predicted.celltype.l2'] == 'B naive']
```
#### but if the column is an index instead:
```
df_subset = df[df.index =="XYZ"]
```
#### select specific column(s)
```
df[["colname"]]
```
or
```
df.loc[:,["col1","col2"]]
```
#### select rows based on column values
```
df_sel = df.loc[df['col'].isin(selected_values)]
```

#### create anndata object from X matrix
```
import anndata as ad
adata = ad.AnnData(X=X, obs=obs, var=var, dtype='float')
```

#### correlation (cor in R)
```
np.corrcoef[1,0] = np.corrcoef[0,1]
```

#### equivalent to gsub in python:
```
import re
mynewstring = re.sub("_", "-", mystring)
```
or
```
mynewstring = mystring.replace("_", "-")
```
#### equivalent to table in python (pandas DataFrame):
```
df.colunm_name.value_counts()
```

#### read arguments in .py script
Option 1:
```
import sys
chrom = str(sys.argv[1])
```
Option 2:
```
import click
@click.command()
@click.option("--chrom", required=True, help="More info here")
def main(
    chrom: str,
):
```

#### to check version of python package
```
import cellregmap as crm
crm.__version__
```
#### python try except
https://www.w3schools.com/python/python_try_except.asp


### Plotting

#### show matrix
```
import matplotlib.pyplot as plt
plt.matshow(M)
```

#### histogram
```
plt.hist(y)
plt.show()
```

```
plt.scatter(x,y)
```

#### save plot
```
plt.savefig("fig.pdf")
```

## Resources
* [Pandas illustrated](https://betterprogramming.pub/pandas-illustrated-the-definitive-visual-guide-to-pandas-c31fa921a43)
* [Numpy illustrated](https://betterprogramming.pub/numpy-illustrated-the-visual-guide-to-numpy-3b1d4976de1)
