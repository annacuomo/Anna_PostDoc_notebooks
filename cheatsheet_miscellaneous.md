## R

#### to read in a compressed file with a .gz extension
```df = read.csv(gzfile(filename), sep="\t")```

#### corrplot
```
library(corrplot)
df = cbind(df0, df1)
corrplot(cor(df))
```


## python

#### equivalent to gsub in python:

```
import re
re.sub("_", "-", mystring)
```
