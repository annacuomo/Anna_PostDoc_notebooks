# Pandas dataframe commands I always forget

## initiate pandas data frame

```Python
import pandas as pd
data = {"cell": cells, "cluster": clusters}
df0 = pd.DataFrame(data, columns=cols, index=idx)
```

## subset data frame based on a column

```Python
cov_naive_Bcell = cov_df[cov_df['predicted.celltype.l2'] == 'B naive']
```

## but if the column is an index instead:

```Python
df_subset = df[df.index =="XYZ"]
```

## select specific column(s)

```Python
df[["colname"]]
```

or

```Python
df.loc[:,["col1","col2"]]
```

## select rows based on column values

```Python
df_sel = df.loc[df['col'].isin(selected_values)]
```

## reorder columns Pandas df (alphabetically)

```Python
df = df.reindex(sorted(df.columns), axis=1)
```

for rows,

```Python
df = df.reindex(sorted(df.index), axis=0)
```

## NAs (pandas)

https://datatofish.com/check-nan-pandas-dataframe/

## replace specific values

```Python
adata.obs['individual_test']=adata.obs['individual'].replace('CPG247841', 'CPG305235')
```

where you are creating a new column (individual_test) which is identical to individual except for that one value that gets replaced (CPG247841 is the original, CPG305235 the new)

# combine dataframes

```Python
results_all_df = []
for pv_df in pv_dfs:
    df = pd.read_csv(to_path(pv_df), index_col=0, sep='\t')
    results_all_df.append(df)
results_all_df = pd.concat(results_all_df)
```

* [equivalent in R](https://github.com/annacuomo/Anna_PostDoc_notebooks/blob/main/CheatSheets/R/cheatsheet_R.md#much-faster-rbind)
* [reference](https://stackoverflow.com/questions/28669482/appending-pandas-dataframes-generated-in-a-for-loop)

## join using Pandas

https://sparkbyexamples.com/pandas/pandas-join-explained-with-examples/

## confusion matrix from df using pandas

```Python
confusion_matrix = pd.crosstab(df['y_actual'], df['y_predicted'], rownames=['Actual'], colnames=['Predicted'])
print(confusion_matrix)
```

## equivalent to table in python (pandas DataFrame)

```Python
df.column_name.value_counts()
```

# Resources

* [Pandas illustrated](https://betterprogramming.pub/pandas-illustrated-the-definitive-visual-guide-to-pandas-c31fa921a43)
