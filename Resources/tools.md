# Collection of tools / resource-websites

### get rsids

* [biomart](http://asia.ensembl.org/biomart/martview/deac7bacee5389a78edf872de8b7b357)
* [biomart ref37](https://grch37.ensembl.org/biomart/martview/377d8e5f76faab7d8517fe0ced390427)

can specify dataset (aka species, type of variant of interest) and then also a range (e.g., chrom, start and end).
to look up a specific variant useful to just do online, else can download entire tables for larger ranges.

### Variant Annotations
* MPC: **M**issense badness, **P**olyphen-2, missense **C**onstraint (Lily Wang (Talkowski lab), Kaitlin Samocha)
* REVEL
* [M-CAP](https://www.nature.com/articles/ng.3703) / [S-CAP](https://www.nature.com/articles/s41588-019-0348-4)
* CADD: Combined Annotation–Dependent Depletion [v1](https://www.nature.com/articles/ng.2892) and [v2](https://academic.oup.com/nar/article/47/D1/D886/5146191)
* [SIFT]()
* [PolyPhen-2]()
* [MetaLR]()
* [RIVER]()

### Genomic Variants
* [VEP - variant effect predictor](https://asia.ensembl.org/info/docs/tools/vep/index.html)
* [gnomad (v3)](https://gnomad.broadinstitute.org/region/22-23241400-23241440?dataset=gnomad_r3)
* [Ensembl](https://asia.ensembl.org/Homo_sapiens/Variation/Mappings?db=core;r=22:23240940-23241940;v=rs5759655;vdb=variation;vf=184891459)
* [Open Targets Genetics](https://genetics.opentargets.org/variant/1_154453788_C_T)

### Acronyms / names
* VCF: variant call format
* Jupyter: Julia, python, R

## Single-cell tools
[Pretty comprehensive / overwhelming list](https://www.scrna-tools.org/)

### Filtering
* Doublet removal
* Ambient RNA removal
* Empty droplet removal

### Demultiplexing
* Cardelino
* Vireo
* Demuxlet

### Processing
* Batch correction
  * MNN
  * CCA (Seurat) 
  * Harmony
* Normalisation
  * scran
  * sctransform   

### Meta-Pseudo cells
* SEA
* MetaCell
* Vision pooling

### Cell-level downstream analysis
* Clustering 
* Cell type annotation
  * scmap 
  * scPred
  * CellTypist 
* Pseudotime inference

### Gene-level downstream analysis
* DE (differential expression)
  * [MAST]() 
* GRN (gene regulatory network)
  * SCODE
  * [SCENIC](https://www.nature.com/articles/nmeth.4463) 

### Workflows / objects
* [Scanpy](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-017-1382-0)
* Seurat
* SingleCellExperiment
* scran
* scater

## Miscellaneous
* [Google Scholar](https://scholar.google.com.au/)
* [Magic Eraser](https://www.magiceraser.io/)

