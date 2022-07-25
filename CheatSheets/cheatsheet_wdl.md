## WDL (workflow description language; pronounced "widdle")

### Intro

[WDL]() is a workflow language to define tasks and workflows.
[Cromwell]() is the execution engine (written in Java) that supports running WDL scripts, on:
* local machine (e.g., own laptop)
* local cluster / compute farm (e.g., Garvan's HPC)
* cloud platform (e.g., Google Cloud, Amazon AWS)

### Use case: CellRegMap

Writing a WDL pipeline to run [CellRegMap]() [here](https://github.com/annacuomo/CellRegMap_pipeline) with Michael Franklin's help.

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
(worked fine for me, but only after checking I had docker installed, i.e., typing ```docker info``` before trying the command again).

Note: [miniwdl] works fine locally, but doesn't work on cluster/GCP, so for that we need Cromwell.

#### Set up to run WDL pipeline on HPC (high performance computing)

To set it up on a high computing system, it is a bit more involved and requires to install [cromwell](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/).

Cromwell is set up to work well on the cloud (e.g., pipelines from the Broad Institute largelt use WDL / cromwell / Terra), but it is a bit more complicated to set up on non-cloud high perfomance computing systems like the Garvan's HPC.

##### Cromwell
First, download/install cromwell (instructions [here](https://cromwell.readthedocs.io/en/stable/tutorials/FiveMinuteIntro/)) from [here](https://github.com/broadinstitute/cromwell/releases/tag/80).

p.s. I actually downloaded [version 56](https://github.com/broadinstitute/cromwell/releases/tag/56) as 80 didn't work for me. 

##### Java
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

##### step 1: Hello World workflow

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

* [Main workflow]
* [Tasks (WDL)]
* [.py scripts in images]
* [inputs .json file]
* [config (cluster specific)]

To run it, go to the repo:
```
cd /to/where/my/repo/is/CellRegMap_pipeline/
```
pull all changes (I am making changes locally, using [VSCode]():
```
git pull
```
if you made changes to wdl scripts in tasks, re-zip the tasks folder:

```zip -r tasks.zip tasks```

then, run:
```
java -Dconfig.file=qsub.conf -jar /share/ScratchGeneral/anncuo/cromwell/cromwell-56.jar run run_cellregmap.wdl --imports tasks.zip --inputs inputs.json
```

Note the full path for where cromwell is, the config file, the zipped tasks, the inputs.

To debug, check progress, intermediate files, etc, need to go to the "execution" folder, that looks something like this:

_/share/ScratchGeneral/anncuo/github_repos/CellRegMap_pipeline/cromwell-executions/RunCellRegMap/63e322c3-e29b-4de3-9893-8b04b6f3207d/call-EstimateBetas/shard-0/execution/_

* it is split by "call" (e.g., call-EstimateBetas)
* by "shard" if run in scatters

Inside execution, there will be standard errors and output, generated files, and the script that was run.

Type ```watch qstat``` to follow how cromwell submits jobs and their state (e.g. "r" for running)

## Resources

[WDL specs](https://github.com/openwdl/wdl/blob/main/versions/development/SPEC.md).

## References

https://www.rc.virginia.edu/userinfo/howtos/rivanna/wdl-bioinformatics/
