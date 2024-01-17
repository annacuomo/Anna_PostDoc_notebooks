# PLINK

PLINK stands for, published in, main uses

## To use PLINK on HPC, as installed by Tim Ho

```bash
(base) -bash-4.2$ module use /share/ClusterShare/apps/brenner/Modules/modulefiles
(base) -bash-4.2$ module load plink
(base) -bash-4.2$ plink2 --help
```

## PLINK misc

### remove duplicate SNPs

```bash
plink2 --bfile /share/ScratchGeneral/anncuo/OneK1K/plink_files/plink_chr2 --set-all-var-ids @:#[b37]$r,$a --rm-dup force-first --make-bed --out /share/ScratchGeneral/anncuo/OneK1K/plink_files/plink_pruning/plink_chr2_noduplicates
```

### LD pruning

```bash
plink2 --bfile MyDataLessDuplicates --indep-pairwise 50 5 0.05 --out chr2
```

### Make new plink files (bed, bim, fam) considering only specific variants

```bash
plink2 --extract chr2.prune.in --bfile plink_chr2_noduplicates --make-bed --out chr2_pruned
```

### Make new plink files (bed, bim, fam) considering only specific samples

```bash
plink2 --keep sc_samples.txt --bfile chr2_pruned --make-bed --out chr2_pruned_sc_samples
```

### Make plink files from VCF file (VCF -> plink)

```bash
plink2 --vcf myvcf.vcf --maf 0.01 --max-maf 0.05 --make-bed --out myplink
```

### Export plink files as VCF (plink -> VCF)

```bash
plink2 --bfile my_plink_prefix --recode vcf-iid --out my_vcf_prefix
```

Use ```--recode vcf``` for sample ids as FID_IID, and ```vcf-iid``` or ```vcf-fid``` to specify only one.

## Pandas Plink

```python
from pandas_plink import read_plink1_bin, write_plink1_bin

geno = read_plink1_bin(in_file)
write_plink1_bin(geno, out_file, verbose=False)
```
