## Hail Batch

Hail batch is a python-based workflow language, similar to WDL or Snakemake, but with easy use of Hail Query inside.

My main experience with this is so far is an end-to-end [workflow](https://github.com/populationgenomics/cellregmap-pipeline/blob/main/batch.py), from selecting rare variants to running association tests.

### Common commands I always forget

Set up a batch:

```Python
import hailtop.batch as hb

b = hb.ServiceBackend(
        billing_project=get_config()['hail']['billing_project'],
        remote_tmpdir=remote_tmpdir(),
    )

batch = hb.Batch('CellRegMap pipeline', backend=sb)
```

For each (python) job:

```Python

new_job = batch.new_python_job('Some description of this job')
manage_concurrency_for_job(new_job)  # manually define function to avoid too many concurrent jobs 
copy_common_env(new_job)             # see below
new_job.depends_on(old_job)
new_job.image(MY_IMAGE)
new_job.call(
        my_function,
        input=my_input,
)
```

Then, at the end:

```Python
# set jobs running
batch.run(wait=False)
```

CPG Hail Batch utils:

```Python
from cpg_utils.hail_batch import (
    copy_common_env,
    dataset_path,
    get_config,
    init_batch,
    output_path,
    remote_tmpdir,
)
```

Explain below what each of this is good for:

* copy_common_env: 
* dataset_path:

Max number of genes being run at once function definition:

```Python
# Setup MAX concurrency by genes
_dependent_jobs: list[hb.job.Job] = []

def manage_concurrency_for_job(job: hb.job.Job):
    """
    To avoid having too many jobs running at once, we have to limit concurrency.
    """
    if len(_dependent_jobs) >= max_gene_concurrency:
        job.depends_on(_dependent_jobs[-max_gene_concurrency])
    _dependent_jobs.append(job)
```

## Dataset path does not like paths starting with /

* PR: https://github.com/populationgenomics/saige-tenk10k/pull/54#pullrequestreview-1892542388
* Matt's message: https://centrepopgen.slack.com/archives/D02PT77HWBX/p1708511199972329?thread_ts=1708499378.203179&cid=D02PT77HWBX

### Other

In the future, I may want to adapt [Konrad K's SAIGE on UKBB whole exomes workflow](https://github.com/Nealelab/ukb_exomes) to running the new Poisson version of SAIGE on scRNA-seq + WGS data from TenK10K.


