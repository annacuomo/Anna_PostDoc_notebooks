VCF: variant calling file

## index

### using bcftools

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
