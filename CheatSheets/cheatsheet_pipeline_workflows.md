## WDL

Setting this up for CellRegMap [here](https://github.com/annacuomo/CellRegMap_pipeline) with Michael Franklin's help.

Here is a [simple WDL](https://github.com/annacuomo/CellRegMap_pipeline/blob/main/hello_all_in_one_file.wdl) to test.

Locally, install ```miniwdl``` as:
```
pip install miniwdl
```
check that you have [Docker](https://docs.docker.com/get-docker/) installed, then run:
```
miniwdl run hello_all_in_one_file.wdl
```
(worked fine for me, but only after checking I had docker installed, i.e. typing ```docker info``` before trying the command again).

### Set up to run WDL pipeline on HPC

To set it up on a high computing system, it is a bit more involved and requires to install [cromwell](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/).

Cromwell is set up to work well on the cloud (e.g., pipelines from the Broad Institute largelt use WDL / cromwell / Terra), but it is a bit more complicated to set up on non-cloud high perfomance computing systems like the Garvan's HPC.

#### Cromwell
First, download/install cromwell (instructions [here](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/)) from [here](https://github.com/broadinstitute/cromwell/releases/tag/80).

p.s. I actually downloaded [version 56](https://github.com/broadinstitute/cromwell/releases/tag/56) as 80 didnt work for me. 

#### Java
Running cromwell requires a working Java environment, so if you don't have it, you should download it from [here](https://www.oracle.com/java/technologies/downloads/#java8) (I downloaded **x64 Compressed Archive** from the Linux options, for my Centos7 machine).
Note that you may need to create an Oracle account to download Java, if you don't have one!

To ensure the newly downloaded java gets called when you type in ```java```, unzip the file you downloaded by typing:
```
 tar zxvf jdk-8u333-linux-x64.tar.gz
```
add the path in your **.bashrc** file, by adding these two lines:

```
MY_JAVA_DIR=/wherever/you/putit
export PATH=$MY_JAVA_DIR:$PATH
```
For me, "wherever/you/put/it" ends in ```jdk1.8.0_333/bin```.

Remember to log out and back into your cluster for the change to be active, and then check that it works by typing ```which java```.

#### step 1: Hello World workflow

```
java -jar cromwell-56.jar run myWorkflow.wdl
```
using the myWorkflow from the instructions page:
```
workflow myWorkflow {
    call myTask
}

task myTask {
    command {
        echo "hello world"
    }
    output {
        String out = read_string(stdout())
    }
}
```

#### qsub Config file
Second, you need a qsub specific config file like [this one](https://github.com/annacuomo/CellRegMap_pipeline/blob/main/qsub.conf) (thanks to Michael Geaghan).

Finally, run your wdl by typing:
```
java -Dconfig.file=/path/to/config/file/qsub.conf -jar cromwell-56.jar run myWorkflow.wdl
```
This worked fine for the Hello World WDL with default parameters, next step is to try an actual workflow.

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
