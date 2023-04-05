# Seurat

## Getting started

### create new object

```R
pbmc.rna <- CreateSeuratObject(counts = ge_df, project = "bioheart.multiome.ge", min.cells = 3, min.features = 200)
```
### basic analysis

```R
pbmc.rna <- NormalizeData(pbmc.rna)
pbmc.rna <- FindVariableFeatures(pbmc.rna)
pbmc.rna <- ScaleData(pbmc.rna)
pbmc.rna <- RunPCA(pbmc.rna)
```

### save

```R
saveRDS(pbmc, file = "../output/pbmc3k_final.rds")
```

### set "identities"

```R
Idents(object = pbmc.atac) <- pbmc.atac@meta.data$predicted.l1
```

## Other

###  fetch (normalised) expression of a specific gene

```R
gene1 <- FetchData(mySample, vars = "myGene")
``` 

### create (mean) pseudobulk by a group (e.g., individual)

AverageExpression ([docs](https://rdrr.io/github/satijalab/seurat/man/AverageExpression.html))

```R
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
