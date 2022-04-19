## R

#### to read in a compressed file with a .gz extension
```df = read.csv(gzfile(filename), sep="\t")```

#### q-value (Storey method for multiple testing correction - FDR)
```
library(qvalue)
qv = qvalue(pv)$qvalues
```
#### adjust p-value
```
p.adjust(p, method = "BH")
p.adjust.methods # to see alternative methods
```

#### corrplot
```
library(corrplot)
df = cbind(df0, df1)
corrplot(cor(df))
```

#### remove NAs
```
df <- df[rowSums(is.na(df)) == 0, ]
```

## python

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
