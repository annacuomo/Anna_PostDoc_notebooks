### Useful commands on Google Cloud Platform (GCP)

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

### Python scripts to run on the cloud

AnyPath, ouputh_path, etc..

### Resources
* [How to cloud](https://github.com/danking/hail-cloud-docs/blob/master/how-to-cloud.md)
* [Google cloud HOW TO guides](https://cloud.google.com/storage/docs/how-to)
