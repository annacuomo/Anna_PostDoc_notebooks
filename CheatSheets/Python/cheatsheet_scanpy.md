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
