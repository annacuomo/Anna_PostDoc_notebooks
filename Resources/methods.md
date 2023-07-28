## Linear Mixed Models (LMMs)

* LIMIX
  * [preprint](https://www.biorxiv.org/content/10.1101/003905v2),
  * [wiki (LIMIX for eQTL mapping)](https://github.com/single-cell-genetics/limix_qtl/wiki).
* BOLT-LMM
  * [paper](https://www.nature.com/articles/ng.3190) (Loh et al, Nature Genetics 2015),
  * [BOLT-LMM v2](https://www.nature.com/articles/s41588-018-0144-6) (Loh et al, Nature Genetics 2018),
  * [manual](https://alkesgroup.broadinstitute.org/BOLT-LMM/BOLT-LMM_manual.html).
* LEMMA (Linear Environment Mixed Model Analysis)
  * [paper](https://www.sciencedirect.com/science/article/pii/S0002929720302779) (Kerin & Marchinin, AJHG 2020),
  * [code](https://mkerin.github.io/LEMMA/).
* fastGWA
  * [paper](https://www.nature.com/articles/s41588-019-0530-8) (Jiang et al, Nature Genetics 2019)
  * [software](https://yanglab.westlake.edu.cn/software/gcta/#fastGWA)
* SAIGE (Scalable and Accurate Implementation of GEneralized mixed model)
  * [paper](https://www.nature.com/articles/s41588-018-0184-y) (Zhou et al, Nature Genetics 2018),
  * [code](https://github.com/weizhouUMICH/SAIGE/)
* regenie
  * [paper](https://www.nature.com/articles/s41588-021-00870-7) (Mbatchou et al, Nature Genetics 2021),
  * [webpage](https://rgcgithub.github.io/regenie/)
  * [repo](https://github.com/rgcgithub/regenie)
* GridLMM
  * [code](https://github.com/deruncie/GridLMM)
* [Estimation and Inference for Very Large Linear Mixed Effects Models](https://arxiv.org/pdf/1610.08088.pdf)
* [lme4](https://github.com/lme4/lme4)
* [mgcv](https://www.maths.ed.ac.uk/~swood34/mgcv/#:~:text=mgcv%20is%20an%20R%20package,splines%20with%20automatic%20smoothness%20estimation.)

PCG (preconditioned conjugate gradient) to solve LMMs ([paper](https://www.sciencedirect.com/science/article/pii/0377042788903585?ref=pdf_download&fr=RR-2&rr=71fa1dad6e88a831)) - used in BOLT-LMM I think

## Rare Variants (RV) association methods

* [Review / Overview (2014)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4085641/) (Lee et al, AJHG 2014)
* SKAT (Sequence Kernel Association Test)
  * [paper](https://www.sciencedirect.com/science/article/pii/S0002929711002229) (Wu et al, AJHG 2011)
* SKAT-O 
  * [paper](https://academic.oup.com/biostatistics/article/13/4/762/241404) (Lee et al, Biostatistics 2012)
  * linear combination of SKAT and burden tests statistics
* SAIGE-GENE - can conduct SKAT-type associations as well as burden tests for unbalanced case-control studies
  * [paper](https://www.nature.com/articles/s41588-020-0621-6) (Zhou et al, Nature Genetics 2020)
  * [SAIGE-GENE+](https://www.nature.com/articles/s41588-022-01178-w) (Zhou et al, Nature Genetics 2022)
  * used by [Karczewski et al Cell Genomics 2022](https://www.sciencedirect.com/science/article/pii/S2666979X22001100)
* LRTq (specific for expression association, i.e., identification of RV-eGenes)
  * [code](https://github.com/avallonking/LRTq),
  * [paper](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1009596) (Li et al, Plos Genetics 2021).

Adding to [this doc](https://docs.google.com/document/d/1zWrtY_1xe0Ye63ukfwb940g1mLwsvRDe-LgHkDyOzvs/edit) for an overview of methods to detect the effects of RV on expression specifically.

## eQTL methods

* Matrix eQTL
  * [paper](https://academic.oup.com/bioinformatics/article/28/10/1353/213326) (Shabalin, Bioinformatics 2012),
  * [webpage](http://www.bios.unc.edu/research/genomic_software/Matrix_eQTL/).
* Tensor QTL
  * [code](https://github.com/broadinstitute/tensorqtl),
  * [paper](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1836-7) (Taylor-Weiner*, Aguet* et al., Genome Biology 2019).
* QTLtools
  * [webpage](https://qtltools.github.io/qtltools/),
  * [paper](https://www.nature.com/articles/ncomms15452) (Delaneau et al., Nature Communications 2017).
* [HEFT](https://academic.oup.com/bioinformatics/article/30/3/369/228688) - webpage no longer exists?
* LORSEN
  * [paper](https://www.frontiersin.org/articles/10.3389/fgene.2021.690926/full)
  * [repo](https://github.com/gaochengPRC/LORSEN)

## Overleaf

LateX scripts for own document getting together info / formulae [here](https://github.com/annacuomo/Review_G_LMM_for_genetics)
