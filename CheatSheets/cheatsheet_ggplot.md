### Multiple plots
```
library(cowplot)
plot_grid(p1, p2, ncol = 2)
```
### Jupyter notebook 
```
# size of plot(s)
options(repr.plot.width = 10, repr.plot.height = 4) 
```
### Histogram ([Example here](https://github.com/annacuomo/Anna_PhD_notebooks/blob/main/sc_neuroseq/iPSCs/fig3b_3e.ipynb))
```
p = ggplot(df_to_plot, aes(x=gene)) + geom_histogram(alpha = 0.8, bins=15) 
```
### Add rectange to plot ([Example](https://github.com/single-cell-genetics/singlecell_endodiff_paper/blob/main/plotting_notebooks/lead_switchin.ipynb))
```
p = p + geom_rect(mapping = aes(xmin = xmin, xmax = xmax, ymin = ymin, ymax = ymax), color = col, fill = col)
```
### Linear trend across points
```
p = ggplot(df, aes(x=x, y=y)) + geom_point()
p + stat_smooth(se = F, linetype=2, col="darkgrey"))
```
#### to get a linear trend per group
```
p + stat_smooth(se=F, linetype = 2, aes(group=as.factor(GROUP), colour=as.factor(GROUP)))
```
## label name
```
p + labs(colour=GROUP)
```

## Venn
```
# pip install matplotlib-venn
from matplotlib_venn import venn2, venn2_circles, venn2_unweighted
from matplotlib_venn import venn3, venn3_circles
from matplotlib import pyplot as plt
%matplotlib inline
venn2(subsets = (30, 10, 5), set_labels = ('Group A', 'Group B'))
```
Slightly more complex example for neuroseq paper (Studies overlap figure; [Fig. 3A](https://github.com/single-cell-genetics/singlecell_neuroseq_paper/blob/main/plotting_notebooks/Figure_3/Figure_3a.ipynb))

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
or see [this notebook](https://github.com/annacuomo/Anna_PhD_notebooks/blob/main/sc_endodiff/Canva%20Palettes.ipynb).

#### RColorBrewer
```
library(RColorBrewer)
p + scale_colour_brewer(palette = "Set1")
```

### Resources

* http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf
* https://ggplot2-book.org/scale-colour.html
* https://r-graph-gallery.com/ggplot2-color.html
* http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/
* https://www.datanovia.com/en/blog/top-r-color-palettes-to-know-for-great-data-visualization/
* https://www.nceas.ucsb.edu/sites/default/files/2020-04/colorPaletteCheatsheet.pdf
* https://github.com/dill/beyonce
* https://r-charts.com/distribution/histogram-binwidth-ggplot2/
