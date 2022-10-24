# Useful commands on Google Cloud Platform (GCP)

## Command line

### create environment with GC SDK 
```mamba create --name gcp -c conda-forge google-cloud-sdk```
```conda activate gcp```
for more details, see [CPG's Getting Started Docs](https://github.com/populationgenomics/team-docs/blob/main/getting_started.md)

### to authenticate oneself
```gcloud auth login```
This will open a browser where you can login with your google credentials.

### get Google Cloud SDK's current version, check available versions and update
```gcloud version```, ```gcloud components list --show-versions``` and ```gcloud components update```

### copy one file into an existing bucket (this may not work anymore)
```gsutil cp /my/file/on/the/cluster.csv gs://path-on-gcp/bucket/```

### list files in a bucket
```gcloud alpha storage ls --recursive gs://path-on-gcp/bucket/```

## Accessing files (saving to and opening new file) in a notebook
This is very annoying always, as the cloud doesn't quite work like a regular storing file system.

### Saving to file

Current working strategy.

First, create a simple ```dataset.toml``` file in the jupyter notebook, that contains the following lines (modify parameters if needed):
```
[workflow]
access_level="test"
dataset="tob-wgs"
```

Next, set config which will be then set when calling ```dataset_path``` (this is what analysis runner does automatically):
```
from cpg_utils.config import set_config_paths
from cpg_utils.hail_batch import dataset_path

set_config_paths(['/home/jupyter/dataset.toml'])
mt_path = dataset_path('output_filename_suffix')
```

## Accessing files (saving to and opening new file) using the analysis runner

Talk about [AnyPath](), [ouputh_path]()

### Saving to file

#### R
* [Example by Kat](https://github.com/populationgenomics/tx-adapt/blob/find_ta_candidates/ta_candidates/get_ta_candidates.R)
* [Own example]()
* [(old) docs](https://github.com/populationgenomics/analysis-runner/blob/main/examples/r/script.R#L23)

#### Python
* [Example 1](https://github.com/populationgenomics/tob-wgs/blob/rare-variant-association/scripts/rv_expression_association/get_gene_set.py#L50)
* [Example 2](https://github.com/populationgenomics/tob-wgs/blob/get-variants/scripts/rv_expression_association/get_vep_variants.py#L59-L74)
* [Example 3](https://github.com/populationgenomics/tob-wgs/blob/rare-variant-association/scripts/rv_expression_association/plot/plot_alt_af.py#L63)

### opening a file

#### Python
Some python libraries (like pandas) deal fine with it.
Others don't.

* [Example](https://github.com/populationgenomics/tob-wgs/blob/get-variants/scripts/rv_expression_association/get_vep_variants.py#L9-L10)

#### R
For R this never works, so..

[Open cloud objects in R](https://cran.r-project.org/web/packages/googleCloudStorageR/vignettes/googleCloudStorageR.html)

* [Example](https://github.com/populationgenomics/tob-wgs/blob/get-variants/scripts/rv_expression_association/run_SKAT.R)



## Resources
* [How to cloud](https://github.com/danking/hail-cloud-docs/blob/master/how-to-cloud.md)
* [Google cloud HOW TO guides](https://cloud.google.com/storage/docs/how-to)


* [Hail batch input files](https://hail.is/docs/batch/tutorial.html#input-files) ????
