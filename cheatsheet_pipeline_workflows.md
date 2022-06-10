## Pipeline tools / workflows

* [Snakemake](https://snakemake.readthedocs.io/en/stable/)
  * [original paper](https://academic.oup.com/bioinformatics/article/28/19/2520/290322) (Köster and Rahman, Bioinformatics 2012)
  * ["rolling" paper](https://f1000research.com/articles/10-33/v1)
* [Netxflow](https://www.nextflow.io/)
  * [repo](https://github.com/nextflow-io/nextflow)
  * [paper](https://www.nature.com/articles/nbt.3820) (Di Tommaso et al, Nature Biotechnology 2017) 
* [hail-batch](https://hail.is/docs/batch/tutorial.html)
  * part of the [hail](https://hail.is/) package
* [WDL](https://support.terra.bio/hc/en-us/sections/360007274612)
* [CWL](https://www.commonwl.org/)
* [Ruffus](http://www.ruffus.org.uk/)
  * [paper](https://academic.oup.com/bioinformatics/article/26/21/2778/214489) (Goodstadt, Bioinformatics 2010)



### Snakemake

I have been wanting to learn in better detail how to use snakemake (and whether that is ideal at all, as opposed to nextflow, and I am sure many other alternatives).

I have used it extensively to map eQTLs in my PhD but I have largely copy-pasted someone else's, only adapting to my own specific needs.
Now, I'd like to gain a deeper understanding to be able to do exactly what I want in different settings, and to be able to efficiently debug by myself without anyone else's help.


### Examples 

#### from Drew (verbatim):

This directory has an example: https://github.com/powellgenomicslab/iPSC_Village_scripts/tree/main/Variance/post_review

The files you should pay attention to are:
* variance_partition_post_review.smk The snakemake file that will run my command (an R script) for each variable which in this case is each gene
* variance_partition_post_review.R This is the R script that is called in the smk file
* variance_partition_post_review_snake.sh These are the commands that I use to run the smk file

I had already written a file that listed all the genes that I wanted to run in this script and that is what is read in to the smk file at the beginning to tell it what to run. 
This example is pretty simple since there is just one rule to run but you can build multiple rules that are dependent on one another that will automatically start running when the last rule is completed. 
Let me know if you're interested in seeing a pipeline version that has multiple rules
