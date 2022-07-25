## Snakemake

I have been wanting to learn in better detail how to use snakemake (and whether that is ideal at all, as opposed to nextflow, and I am sure many other alternatives - e.g. should I just switch to hail-bath altogether [in line with CPG](https://github.com/populationgenomics/team-docs/blob/main/hail_batch_dev.md)?).

I have used it extensively to map eQTLs in my PhD but I have largely copy-pasted someone else's, only adapting to my own specific needs.
Now, I'd like to gain a deeper understanding to be able to do exactly what I want in different settings, and to be able to efficiently debug by myself without anyone else's help.


### Examples 


#### Snakemake to run single-cell (pseudobulk) eQTL

This is my own snakemake to run the [limix QTL pipeline](https://github.com/single-cell-genetics/limix_qtl) to map eQTLs in our [neuronal differentiation study](https://github.com/single-cell-genetics/singlecell_neuroseq_paper) ([paper](https://www.nature.com/articles/s41588-021-00801-6)) - building on one of [Marc Jan Bonder](https://twitter.com/mjbonder)'s templates:

https://github.com/annacuomo/CellRegMap_analyses/blob/main/neuroseq/usage/scripts/snakemake.py

#### from Drew (verbatim):

This directory has an example: https://github.com/powellgenomicslab/iPSC_Village_scripts/tree/main/Variance/post_review

The files you should pay attention to are:
* variance_partition_post_review.smk The snakemake file that will run my command (an R script) for each variable which in this case is each gene
* variance_partition_post_review.R This is the R script that is called in the smk file
* variance_partition_post_review_snake.sh These are the commands that I use to run the smk file

I had already written a file that listed all the genes that I wanted to run in this script and that is what is read in to the smk file at the beginning to tell it what to run. 
This example is pretty simple since there is just one rule to run but you can build multiple rules that are dependent on one another that will automatically start running when the last rule is completed. 
Let me know if you're interested in seeing a pipeline version that has multiple rules