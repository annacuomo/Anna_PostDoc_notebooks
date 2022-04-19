## Multiple plots
```
library(cowplot)
plot_grid(p1, p2, ncol = 2)
```

## Jupyter notebook 
```
# size of plot(s)
options(repr.plot.width = 10, repr.plot.height = 4) 
```

## Text in plots
```
# size of text in plot (axes labels, title, etc..)
p + theme(text = element_text(size=20))
```
## Save plot
```
fig_dir = "/.../figures/"
pdf(paste0(fig_dir,"myplot.pdf"), width=8, height=6)
ggplot()
dev.off()
```

## Colour scales

### Gradients
#### RColorBrewer
```
library(RColorBrewer)
p + scale_colour_gradientn(colors = brewer.pal(9,"Blues"))

# for alternative palettes, try:
RColorBrewer::display.brewer.all()
```
### Gradients
#### ggthemes
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
#### RColorBrewer
```
library(RColorBrewer)
p + scale_colour_brewer(palette = "Set1")
```

### Resources

https://ggplot2-book.org/scale-colour.html

https://r-graph-gallery.com/ggplot2-color.html

http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/

https://www.datanovia.com/en/blog/top-r-color-palettes-to-know-for-great-data-visualization/

https://www.nceas.ucsb.edu/sites/default/files/2020-04/colorPaletteCheatsheet.pdf
