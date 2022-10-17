## R

#### to read in a compressed file with a .gz extension
```df = read.csv(gzfile(filename.txt), sep="\t")```

#### sample n rows from a dataframe
```
 df[sample(nrow(df), n), ]
```

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

#### quantiles
```
qts = quantile(v, probs = c(0.3, 0.7))
bottom_cells = rownames(df[df$gene < qts[1],])
top_cells = rownames(df[df$gene > qts[2],])

```
see [notebook](https://github.com/annacuomo/Anna_PhD_notebooks/blob/main/CellRegMap/neuroseq/June_2021/example_figure5_SLC35E2_step1.ipynb).

#### quick enrichment for gene list
```
# install.packages("enrichR")
library(enrichR)
setEnrichrSite("Enrichr")
dbs <- listEnrichrDbs()
# run the over over-representation analysis in kegg
enrich_pw <- enrichr(list_of_egenes, 'KEGG_2021_Human')
```
#### check if file exists

```
file.exists("myfile.R")
```
returns ```TRUE``` (or ```FALSE```)

#### remove NAs
```
df <- df[rowSums(is.na(df)) == 0, ]
```
#### read arguments in Rscript
```
args = commandArgs(trailingOnly=TRUE)
chr_number <- args[1]
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

AverageExpression ([docs](https://rdrr.io/github/satijalab/seurat/man/AverageExpression.html)), let's you create (mean) pseudobulk by a group (e.g., individual)
```
mat = AverageExpression(
  sce,
  assays = "SCT",
  features = relevant_genes,
  return.seurat = FALSE,
  group.by = "individual"
)
``` 


