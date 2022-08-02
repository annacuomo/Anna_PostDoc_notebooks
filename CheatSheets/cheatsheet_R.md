## R

#### to read in a compressed file with a .gz extension
```df = read.csv(gzfile(filename.txt), sep="\t")```

#### q-value (Storey method for multiple testing correction - FDR)
```
library(qvalue)
qv = qvalue(pv)$qvalues
```
If you get the error: ```Error in smooth.spline(lambda, pi0, df = smooth.df) : missing or infinite values in inputs are not allowed```, try:
```
qv = qvalue(pv, pi0=1)$qvalues
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
#### quick enrichment for gene list
```
# install.packages("enrichR")
library(enrichR)
setEnrichrSite("Enrichr")
dbs <- listEnrichrDbs()
# run the over over-representation analysis in kegg
enrich_pw <- enrichr(list_of_egenes, 'KEGG_2021_Human')
```

#### remove NAs
```
df <- df[rowSums(is.na(df)) == 0, ]
```
#### package version
```
packageVersion("snow")
```
#### UMAP packages
```
install.packages("umap")
library(umap)
```
works fine in R, but to run Seurat's ```obj = RunUMAP(obj)``` you seemingly have to install umap-learn, i.e.,:
```
pip install umap-learn
```
in the command line. Haven't quite managed to get it to work myself though.

#### installation
##### using CRAN
```
install.packages("dplyr")
```
##### using Bioconductor
```
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("qvalue")
```

### Seurat
```gene1<- FetchData(mySample, vars = "myGene")``` to fetch (normalised) expression of a specific gene

