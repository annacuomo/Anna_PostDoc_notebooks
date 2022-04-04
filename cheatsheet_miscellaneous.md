## R

#### to read in a compressed file with a .gz extension
```df = read.csv(gzfile(filename), sep="\t")```

### ggplot
#### colour scales (gradients)
```
library(RColorBrewer)
p + scale_colour_gradientn(colors = brewer.pal(9,"Blues"))

# for alternative palettes, try:
RColorBrewer::display.brewer.all()
```
#### colour scales (discrete)
```
library(ggthemes)
p + scale_color_canva(palette = "Pool party")

# for alternative palettes, try:
require("scales")
for (i in 1:length(names(canva_palettes))){
    print(show_col(canva_pal(names(canva_palettes)[i])(4)))   
    print(names(canva_palettes)[i])
}
```

## python

#### equivalent to gsub in python:

```
import re
re.sub("_", "-", mystring)
```
