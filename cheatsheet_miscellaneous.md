## R

#### to read in a compressed file with a .gz extension
```df = read.csv(gzfile(filename), sep="\t")```

### ggplot
##### colour scales (gradients)
```
library(RColorBrewer)
p + scale_colour_gradientn(colors = brewer.pal(9,"Blues"))
```

## python

#### equivalent to gsub in python:

```
import re
re.sub("_", "-", mystring)
```
