## python

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

#### create anndata object from X matrix
```
import anndata as ad
adata = ad.AnnData(X=X, obs=obs, var=var, dtype='float')
```

#### equivalent to gsub in python:
```
import re
re.sub("_", "-", mystring)
```

#### show matrix
```
import matplotlib.pyplot as plt
plt.matshow(M)
```

#### other plots
```
plt.hist(y)
plt.show()
```

#### save plot
```
plt.savefig("fig.pdf")
```

#### to check version of python package
```
import cellregmap as crm
crm.__version__
```
