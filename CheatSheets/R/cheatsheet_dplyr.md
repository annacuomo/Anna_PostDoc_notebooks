# mutate

```R
sumstats_df <- sumstats_df %>% mutate(MAF = ifelse(AF_Allele2<0.5, AF_Allele2,1-AF_Allele2))
```
```R
sumstats_df = sumstats_df %>% mutate(distance=as.numeric(snp_pos)-start)
```

# get frequencies

```R
mtcars %>%
  group_by(am, gear) %>%
  summarise(n = n())
```

# separate (not actually dplyr?)

split values, e.g. here top_MarkerID is defined as `chrom:snp_pos:ref:alt`

```R
sumstats_df = sumstats_df %>% tidyr::separate(top_MarkerID, into = c("chrom", "snp_pos", "ref", "alt"), sep = ":", remove = FALSE)
```


