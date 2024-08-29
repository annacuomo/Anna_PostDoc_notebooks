# VCF: variant calling file

## using bcftools

### index

First, load bcftools, on brenner using Tim Ho's installation you can do:

```bash
module use /share/ClusterShare/apps/brenner/Modules/modulefiles
module load bcftools
```

next, index your (zipped) vcf as:

```bash
bcftools index -c myfile.vcf.gz
```

or

```bash
bcftools index -t myfile.vcf.gz
```

for ```.csi``` or ```.tbi``` files respectively

### annotate

add ID column based on other cols

```bash
bcftools annotate --set-id +'%CHROM\_%POS\_%REF\_%FIRST_ALT' myfilename.vcf > new.vcf
```

ref: https://www.biostars.org/p/278522/

## zip file

```bash
module use /share/ClusterShare/apps/brenner/Modules/modulefiles
module load htslib
bgzip -c myfile.vcf > myfile.gz
```


## some random manipulation from other repos

* https://github.com/powellgenomicslab/tenk10k_phase1/blob/main/Demuxafy/preprocessing/prepare_inputs.md#vcf-manipulation


