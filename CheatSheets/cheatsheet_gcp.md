# Useful commands on Google Cloud Platform (GCP)

## Accessing files
This is very annoying always, as the cloud doesn't quite work like a regular storing file system.

### saving to file

Talk about [AnyPath](), [ouputh_path]()

#### Notebook

#### Analysis runner

* [Example 1](https://github.com/populationgenomics/tob-wgs/blob/rare-variant-association/scripts/rv_expression_association/get_gene_set.py#L50)
* [Example 2](https://github.com/populationgenomics/tob-wgs/blob/get-variants/scripts/rv_expression_association/get_vep_variants.py#L59-L74)
* [Example 3](https://github.com/populationgenomics/tob-wgs/blob/rare-variant-association/scripts/rv_expression_association/plot/plot_alt_af.py#L63)

### opening a file

#### Python
Some python libraries (like pandas) deal fine with it.
Others don't.

#### R
For R this never works, so..

[Open cloud objects in R](https://cran.r-project.org/web/packages/googleCloudStorageR/vignettes/googleCloudStorageR.html)

* [Example](https://github.com/populationgenomics/tob-wgs/blob/get-variants/scripts/rv_expression_association/run_SKAT.R)

### Miscellaneous

#### create environment with GC SDK 
```mamba create --name gcp -c conda-forge google-cloud-sdk```
```conda activate gcp```
for more details, see [CPG's Getting Started Docs](https://github.com/populationgenomics/team-docs/blob/main/getting_started.md)

#### to authenticate oneself
```gcloud auth login```
This will open a browser where you can login with your google credentials.

#### get Google Cloud SDK's current version, check available versions and update
```gcloud version```, ```gcloud components list --show-versions``` and ```gcloud components update```

#### copy one file into an existing bucket
```gsutil cp /my/file/on/the/cluster.csv gs://path-on-gcp/bucket/```

#### list files in a bucket
```gcloud alpha storage ls --recursive gs://path-on-gcp/bucket/```

## Resources
* [How to cloud](https://github.com/danking/hail-cloud-docs/blob/master/how-to-cloud.md)
* [Google cloud HOW TO guides](https://cloud.google.com/storage/docs/how-to)


* [Hail batch input files](https://hail.is/docs/batch/tutorial.html#input-files) ????
