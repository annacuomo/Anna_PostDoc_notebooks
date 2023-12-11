## RNA-seq

### Sequencing files: FASTQ

Stores the nucleotide sequence plus information on the sequencing quality

### Alignment files: SAM/BAM/CRAM

* SAM: tab-delimited text format to store genomic alignment: header (@) + alignment sections.
* BAM: binary version of SAM (more memory efficient)
* CRAM: compressed version of BAM (takes up even less space)

samtools is a command line tool to manipulate and view sam / bam etc files, e.g.:

```
samtools view MyFile.bam
```

## Genotypes

VCF (variant call format) is the standard file format for storing variation data.
Each row represents a locus, with columns representing info on that locus and then genotypes at that locus for one or more individuals (one column per individual).


## Resources

* [Video 2 of 6 as part of the INTRA scRNA-seq workshop](https://www.youtube.com/watch?v=rB9-xj8Q1gU&t=14s)
* [VCF intro EBI](https://www.ebi.ac.uk/training/online/courses/human-genetic-variation-introduction/variant-identification-and-analysis/understanding-vcf-format/)
* [on BAMs](https://felixfan.github.io/bam-sam/)
