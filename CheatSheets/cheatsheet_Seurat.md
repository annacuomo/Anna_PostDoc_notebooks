# Seurat

### create
```
pbmc.rna <- CreateSeuratObject(counts = ge_df, project = "bioheart.multiome.ge", min.cells = 3, min.features = 200)
pbmc.rna
```

###  fetch (normalised) expression of a specific gene
```gene1<- FetchData(mySample, vars = "myGene")``` 

### create (mean) pseudobulk by a group (e.g., individual)
AverageExpression ([docs](https://rdrr.io/github/satijalab/seurat/man/AverageExpression.html))
```
mat = AverageExpression(
  sce,
  assays = "SCT",
  features = relevant_genes,
  return.seurat = FALSE,
  group.by = "individual"
)
``` 

## Vignettes

https://satijalab.org/seurat/index.html
