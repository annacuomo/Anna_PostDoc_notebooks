## Colour scales

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

## Resources

https://ggplot2-book.org/scale-colour.html
https://r-graph-gallery.com/ggplot2-color.html
http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/
https://www.datanovia.com/en/blog/top-r-color-palettes-to-know-for-great-data-visualization/
