### Multiple plots

```R
library(cowplot)
plot_grid(p1, p2, ncol = 2)
```

### Jupyter notebook 

```R
# size of plot(s)
options(repr.plot.width = 10, repr.plot.height = 4) 
```

### Histogram ([Example here](https://github.com/annacuomo/Anna_PhD_notebooks/blob/main/sc_neuroseq/iPSCs/fig3b_3e.ipynb))

```R
p = ggplot(df_to_plot, aes(x=gene)) + geom_histogram(alpha = 0.8, bins=15) 
```

### Barplot

```R
ggplot(data, aes(x=name, y=value)) + geom_bar(stat = "identity")
```

add error bars: https://r-graph-gallery.com/4-barplot-with-error-bar.html

### Alluvial plots

```R
install.packages("ggalluvial")
library(ggalluvial)
```

[Examples](https://cran.r-project.org/web/packages/ggalluvial/vignettes/ggalluvial.html)

### Order bar chart by value

```R
ggplot(corr.m, aes(x = reorder(miRNA, -value), y = value, fill = variable)) + 
  geom_bar(stat = "identity")
```

### Add rectange to plot ([Example](https://github.com/single-cell-genetics/singlecell_endodiff_paper/blob/main/plotting_notebooks/lead_switchin.ipynb))

```R
p = p + geom_rect(mapping = aes(xmin = xmin, xmax = xmax, ymin = ymin, ymax = ymax), color = col, fill = col)
```

### Linear trend across points

```R
p = ggplot(df, aes(x=x, y=y)) + geom_point()
p + stat_smooth(se = F, linetype=2, col="darkgrey"))
```

#### To get a linear trend per group

```R
p + stat_smooth(se=F, linetype = 2, aes(group=as.factor(GROUP), colour=as.factor(GROUP)))
```

## Label name

```R
p + labs(colour=GROUP)
```

## Increase text in plots

```R
# size of text in plot (axes labels, title, etc..)
p + theme(text = element_text(size=20))
```

## Remove legend

```R
p + theme(legend.position="none")
````

## Rotate axes labels 

```R
p + theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))
```

## Add text to plot, AKA "annotate"

```R
p + annotate("text", label = "added_text", x = x_value, y = y_value)
```

## QQ plot

```R
df$pv_uniform <- runif(dim(df)[1], min = 0, max = 1)
p <- ggplot(df, aes(x = sort(-log10(pv_uniform)), y = sort(-log10(p.value)))) + 
    geom_abline(slope = 1, intercept = 0, col = "firebrick") +
    geom_point(alpha = 0.5, pch = 1) + xlab("-log10(expected p-values)") + ylab("-log10(observed p-values)") +
    theme_bw() + ggtitle("mytrait") +
    theme(legend.position="none", panel.border = element_blank())
```

## Manhattan plot

```R
library(dplyr)
library(ggplot2)

# enforce numeric position
df0$POS = as.numeric(df0$POS)

# prepare dataframe for Manhattan
don <- df0 %>% 
  
  # Compute chromosome size
  group_by(CHR) %>% 
  summarise(chr_len=max(POS)) %>% 
  
  # Calculate cumulative position of each chromosome
  mutate(tot=cumsum(chr_len)-chr_len) %>%
  select(-chr_len) %>%
  
  # Add this info to the initial dataset
  left_join(df0, ., by=c("CHR"="CHR")) %>%
  
  # Add a cumulative position of each SNP
  arrange(CHR, POS) %>%
  mutate(BPcum=POS+tot)
  
# axes
axisdf = don %>% group_by(CHR) %>% summarize(center=( max(BPcum) + min(BPcum) ) / 2 )

# plot
ggplot(don, aes(x=BPcum, y=-log10(p.value))) +
    
    # Show all points
    geom_point(aes(color=as.factor(CHR)), alpha=0.8, size=1.3) +
    scale_color_manual(values = rep(c("grey", "skyblue"), 22 )) +
    
    # custom X axis:
    scale_x_continuous( label = axisdf$CHR, breaks=axisdf$center ) +
    scale_y_continuous(expand = c(0, 0) ) +     # remove space between plot area and x axis
  
    # Custom the theme:
    theme_bw() +
    theme( 
      legend.position="none",
      panel.border = element_blank(),
      panel.grid.major.x = element_blank(),
      panel.grid.minor.x = element_blank()
    )
```

* [Ref1](https://github.com/annacuomo/Notebooks_private/blob/main/scripts/TenK10K/saige_qtl/saige_eqtl_onek1k/make_manhattan_files.R)
* [Ref2](https://r-graph-gallery.com/101_Manhattan_plot.html)

## Upset plots

https://jokergoo.github.io/ComplexHeatmap-reference/book/upset-plot.html


## Save plot

```R
fig_dir <- "/.../figures/"
pdf(paste0(fig_dir,"myplot.pdf"), width=8, height=6)
ggplot()
dev.off()
```

## Colour scales

### Gradients

#### RColorBrewer

```R
library(RColorBrewer)
p + scale_colour_gradientn(colors = brewer.pal(9,"Blues"))

# for alternative palettes, try:
RColorBrewer::display.brewer.all()
```

### Gradients

#### ggthemes

```R
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

```R
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
