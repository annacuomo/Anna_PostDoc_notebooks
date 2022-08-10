## WDL (workflow description language; pronounced "widdle")

### Intro

[WDL](https://openwdl.org/) is a workflow language to define tasks and workflows.
[Cromwell](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/) is the execution engine (written in Java) that supports running WDL scripts, on:
* local machine (_e.g._, own laptop)
* local cluster / compute farm (_e.g._, Garvan's HPC)
* cloud platform (_e.g._, Google Cloud Platform, Amazon AWS, Microsoft Azure)

### Use case: CellRegMap

A WDL pipeline to run [CellRegMap](https://github.com/limix/CellRegMap) is available at [this repo](https://github.com/populationgenomics/CellRegMap_pipeline) (written with a lot of help from [Michael Franklin](https://github.com/illusional)) and on [Dockerhub](https://hub.docker.com/repository/docker/annasecuomo/cellregmap_pipeline).

### Getting started

Here is a [simple WDL](https://github.com/annacuomo/CellRegMap_pipeline/blob/main/hello_all_in_one_file.wdl) to test.

Locally, install ```miniwdl``` as:
```
pip install miniwdl
```
check that you have [Docker](https://docs.docker.com/get-docker/) installed, then run:
```
miniwdl run hello_all_in_one_file.wdl
```
(worked fine for me, but only after checking I had docker installed, _i.e._, typing ```docker info``` before trying the command again).

Note: [miniwdl] works fine locally, but doesn't work on cluster/GCP, so for that we need Cromwell.

#### Set up to run WDL pipeline on HPC (high performance computing)

To set it up on a high computing system, it is a bit more involved and requires to install [cromwell](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/).

Cromwell is set up to work well on the cloud (_e.g._, pipelines from the [Broad Institute](https://www.broadinstitute.org/) largely use WDL / cromwell / Terra), but it is a bit more complicated to set up on non-cloud high perfomance computing systems like the Garvan's HPC.

##### Cromwell
First, download/install cromwell (instructions [here](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/)) from [here](https://github.com/broadinstitute/cromwell/releases/tag/80).

p.s. I actually downloaded [version 56](https://github.com/broadinstitute/cromwell/releases/tag/56) as 80 didn't work for me. 

##### Java
Running cromwell requires a working Java environment, so if you don't have it, you should download it from [here](https://www.oracle.com/java/technologies/downloads/#java8) (I downloaded **x64 Compressed Archive** from the Linux options, for the cluster's Centos7 machine).
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

##### step 1: Hello World workflow

Create the myWorkflow from the instructions page:
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
and run it by typing:
```
java -jar cromwell-56.jar run myWorkflow.wdl
```
This worked fine locally, but to run on the cluster we need one more step.

##### qsub Config file
Second, you need a qsub specific config file like [this one](https://github.com/annacuomo/CellRegMap_pipeline/blob/main/qsub.conf) (thanks to Michael Geaghan).

Finally, run your wdl by typing:
```
java -Dconfig.file=/path/to/config/file/qsub.conf -jar cromwell-56.jar run myWorkflow.wdl
```
This worked fine for the Hello World WDL with default parameters, next step is to try an actual workflow.

### CellRegMap WDL pipeline

Now that we are happy that the simple example wdl script works, let's work on the actual pipeline.

[Pipeline repo](https://github.com/annacuomo/CellRegMap_pipeline/) structure:

* [Main workflow]() - main WDL pipeline
* [Tasks (WDL)]() - these are tasks that get called by the main workflow, written in WDL
* [.py scripts in images]() - these will get added to the container
* [inputs .json file]() - all input files need to be specified here
* [config (cluster specific)]() - this file specifies how you submit the

To run it, go to the repo:
```
cd /to/where/my/repo/is/CellRegMap_pipeline/
```
pull all changes (I am making changes locally, using [VSCode](https://code.visualstudio.com/)):
```
git pull
```
if you made changes to wdl scripts in tasks, re-zip the tasks folder:

```
zip -r tasks.zip tasks
```

then, run:
```
java -Dconfig.file=qsub.conf -jar /share/ScratchGeneral/anncuo/cromwell/cromwell-56.jar run runCellRegMap.wdl --imports tasks.zip --inputs inputs.json
```

Note the full path for where cromwell is, the main workflow name, the config file, the zipped tasks, the inputs file.

To debug, check progress, intermediate files, etc, need to go to the "execution" folder, that looks something like this:

```/share/ScratchGeneral/anncuo/github_repos/CellRegMap_pipeline/cromwell-executions/RunCellRegMap/63e322c3-e29b-4de3-9893-8b04b6f3207d/call-EstimateBetas/shard-0/execution/```

* the path starts with where the repo is
* inside which cromwell creates a folder called cromwell-executions, with the (only one for now) main workflow
* it is split by "call" (_e.g._, call-EstimateBetas)
* by "shard" if run in scatters

Inside execution, there will be standard errors and output, generated files, and the script that was run.

Type ```watch qstat``` to follow how cromwell submits jobs and their state (_e.g._, "r" for running) - note that this is specific to this qsub cluster (vs _e.g._, bsub etc..)

#### Build container

To use a docker image instead of a conda environment ([commit](https://github.com/populationgenomics/CellRegMap_pipeline/commit/a11dac55f020ed442c47491eef47c987d60fc35a)), you need to add:
* [Dockerfile](https://github.com/populationgenomics/CellRegMap_pipeline/blob/create-wdl-workflow/image/Dockerfile)
* [requirements.txt](https://github.com/populationgenomics/CellRegMap_pipeline/blob/create-wdl-workflow/image/requirements.txt) - Python packages to install (specify version!)
* [deploy.yaml](https://github.com/populationgenomics/CellRegMap_pipeline/blob/create-wdl-workflow/.github/workflows/deploy.yaml) - contains instructions to build docker image and push to dockerhub (github action)

Create repo in dockerhub, add secrets in github (specific repo-> settings-> secrets-> actions-> new repository secret) DOCKERHUB_USERNAME (annasecuomo) and DOCKERHUB_TOKEN, after creating a token in dockerhub (account settings -> security -> new access token). 

#### visualise pipeline
Install womtools from [here](https://github.com/broadinstitute/cromwell/releases/tag/56) (note that as for cromwell the newest version 83 doesn't quite work so I am using v 56).
Then, run:
```
java -jar ../cromwell/womtool-56.jar graph runCellRegMap.wdl
```
copy results into: https://dreampuf.github.io/GraphvizOnline, and you get something like this:

![graphviz (1)](https://user-images.githubusercontent.com/25035866/183782252-11d38773-f6c0-40f7-bef0-14b075406be9.svg)

## Resources

[WDL specs](https://github.com/openwdl/wdl/blob/main/versions/development/SPEC.md).

[WDL best practices](https://docs.dockstore.org/en/stable/advanced-topics/best-practices/wdl-best-practices.html)

[python logging](https://docs.python.org/3/howto/logging.html)

[what to look for in a code review](https://google.github.io/eng-practices/review/reviewer/looking-for.html)

[case styles in programming](https://systemweakness.com/case-styles-in-programming-b4ee6012fd5f)

## References

https://www.rc.virginia.edu/userinfo/howtos/rivanna/wdl-bioinformatics/ (intro)
