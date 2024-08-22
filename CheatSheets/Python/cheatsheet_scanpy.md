# Scanpy / AnnData commands I often forget

## create anndata object from X matrix

```Python
import anndata as ad
adata = ad.AnnData(X=X, obs=obs, var=var, dtype='float')
```

## subset by obs

```Python
celltype = 'CD4 Naive'
adata_CD4_Naive = adata[adata.obs['wg2_scpred_prediction'] == celltype]
```

## subset by var

```Python
chromosome = 1
adata_chr1 = adata[:, adata.var["chr"] == f'chr{chromosome}']
```

## concatenate multiple samples

```Python
datasets=[]
for file in scanpy_files:
    adata = sc.read(file)
    datasets.append(adata)
adata = datasets[0].concatenate(*datasets[1:])
```

## exclude categories by obs

```Python
adata = adata[~adata.obs['MajoritySinglet_Individual_Assignment'].isin(["unassigned","doublet"])]
```

## add cell info to anndata from a separate dataframe

```Python
import pandas as pd
adata.obs = pd.concat([adata.obs, new_obs_info_df], axis=1)
```

## extract gene expression for selected genes

```Python
gene_adata = expression_adata[:, expression_adata.var.index.isin(genes)]
expr_mat = gene_adata.X.todense() # to dense from sparse
# if you want to save it as a data frame
expr_df = pd.DataFrame(data=expr_mat, index=gene_adata.obs.index, columns=genes)
```
