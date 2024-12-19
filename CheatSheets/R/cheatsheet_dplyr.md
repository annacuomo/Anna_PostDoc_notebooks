# mutate

sumstats_df <- sumstats_df %>% mutate(MAF = ifelse(AF_Allele2<0.5, AF_Allele2,1-AF_Allele2))
