# mutate

```R
sumstats_df <- sumstats_df %>% mutate(MAF = ifelse(AF_Allele2<0.5, AF_Allele2,1-AF_Allele2))
```
```R
sumstats_df = sumstats_df %>% mutate(distance=as.numeric(snp_pos)-start)
```

# separate (not actually dplyr?)

```R
sumstats_df = common_acat_df %>% tidyr::separate(top_MarkerID, into = c("chrom", "snp_pos", "ref", "alt"), sep = ":", remove = FALSE)
```
