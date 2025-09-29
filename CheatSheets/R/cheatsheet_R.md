# Recurrent R commands

## Reading in files

### much faster reading (and writing) using data.table

```R
df = as.data.frame(data.table:::fread(input_filename, header = T, stringsAsFactors = FALSE))
data.table:::fwrite(df0, output_filename)
```

### to read in a compressed file with a .gz extension

```R
df <- read.csv(gzfile(filename.txt.gz), sep="\t")
```

### to read in Matrix (.mtx) objects

```R
df <- Matrix::readMM(mymatrix.mtx)
```

### to read in h5ad objects

```R
library(rhdf5)
```

[Example](https://github.com/annacuomo/Anna_PhD_notebooks/blob/main/Covid/full_data_toR.ipynb)

### read arguments in Rscript

```R
args <- commandArgs(trailingOnly=TRUE)
chr_number <- args[1]
```

### check if file exists

```R
file.exists(myfile)
```

### check if dir / path exists and create if not

```R
if (!dir.exists(output_dir)) {dir.create(output_dir)}
```

add ```recursive=TRUE``` if the parent directory does not exist either, and do ```file.exists``` instead for files.

### basic R function

```R
myfun <- function(param1, param2){
    # body of function
    return(myout)
}
```

## Data manipulation

### initialise data frame

```R
df <- data.frame(mat)
rownames(df) = rows
colnames(df) = cols 
```

### remove duplicate rows

e.g., only retain top variant for a gene

```R
results <- results[-which(duplicated(results$gene)),]
```

### re-order factor levels for any categorical variable

```R
df$region <- factor(df$region, levels=c('A', 'E', 'D', 'C', 'B'))
```

### categorical into unique numbers

https://www.kaggle.com/discussions/getting-started/396165

### number of characters in string

```R
nchar(mystring)
```

### MUCH faster rbind

instead of doing:

```R
df_combine = data.frame()
for (file in files){
    df_curr = read.csv(file)
    df_combine = rbind(df_combine, df_curr)
}
```

do 

```R
library(data.table)
df_list = list()
for (file in files){
    df_list[[file]] = read.csv(file)
}
df_combine = rbindlist(df_list)
```

it is *much* faster!!

#### rbind tables with different columns

```R
rbindlist(df_list, fill=TRUE)
```

just adds NAs for missing values.

### sample n rows from a dataframe

```df[sample(nrow(df), n), ]```

### long to wide using reshape

```R
library(reshape)
df = data.frame(sample = c("sample1","sample2","sample1","sample2"), name = c("n1","n2","n2","n1"), value = c(1,2,3,4))
mat = cast(df, sample ~ name)
```

### remove NAs

```R
df <- df[rowSums(is.na(df)) == 0, ]         # removes rows with any NA
df <- df[rowSums(is.na(df)) != ncol(df), ]  # removes rows with all NA
```

### replace NAs (eg with 0s)

```R
data[is.na(data)] <- 0
```

### swap values (e.g. 0s for very small values)

```R
p.value[p.value==0] <- 10^(-16)
```

### join using data.table (vs e.g. dplyr)

[Cheatsheet](https://gist.github.com/nacnudus/ef3b22b79164bbf9c0ebafbf558f22a0)

### use of seq (linspace)

```R
beta = seq(from = 0.1, to = 1, by = 0.1)
```

### note that sort by default excludes NAs, so may result in different vector lengths


## Analysis

### q-value (Storey method for multiple testing correction - FDR)

```R
library(qvalue)
qv = qvalue(pv)$qvalues
```

If you get the error: ```Error in smooth.spline(lambda, pi0, df = smooth.df) : missing or infinite values in inputs are not allowed```, try:

```R
qv = qvalue(pv, pi0=1)$qvalues
```

### adjust p-value

```R
p.adjust(p, method = "BH")
p.adjust.methods # to see alternative methods
```

### quantiles

```R
qts = quantile(v, probs = c(0.3, 0.7))
bottom_cells = rownames(df[df$gene < qts[1],])
top_cells = rownames(df[df$gene > qts[2],])
```

see [notebook](https://github.com/annacuomo/Anna_PhD_notebooks/blob/main/CellRegMap/neuroseq/June_2021/example_figure5_SLC35E2_step1.ipynb).

### quick enrichment for gene list

```R
# install.packages("enrichR")
library(enrichR)
setEnrichrSite("Enrichr")
dbs <- listEnrichrDbs()
# run the over over-representation analysis in kegg
enrich_pw <- enrichr(list_of_egenes, 'KEGG_2021_Human')
```

## Plotting

### corrplot

```R
library(corrplot)
df = cbind(df0, df1)
corrplot(cor(df))
```

### UMAP packages

```R
install.packages("umap")
library(umap)
```

works fine in R, but to run Seurat's ```obj = RunUMAP(obj)``` you seemingly have to install umap-learn, i.e.,:

```R
pip install umap-learn
```

in the command line. Haven't quite managed to get it to work myself though.

## File exploration

### check if file exists

```R
file.exists("myfile.R")
```

returns ```TRUE``` (or ```FALSE```)

### list files in directory

```R
list.files(mydir)
```

## Coding

### record time a function lasted

```R
start_time <- Sys.time()
my_function()
end_time <- Sys.time()
end_time - start_time
```

## Installation

### using CRAN

```R
install.packages("dplyr")
```

### using Bioconductor

```R
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("qvalue")
```

### check package version

```R
packageVersion("snow")
```

## Resources

* Twitter cheatsheet https://x.com/R_Graph_Gallery/status/1846553315657580981



