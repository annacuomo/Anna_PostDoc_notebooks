## Hail Batch

Hail batch is a python-based workflow language, similar to WDL or Snakemake, but with easy use of Hail Query inside.

My main experience with this is so far is an end-to-end [workflow](https://github.com/populationgenomics/cellregmap-pipeline/blob/main/batch.py), from selecting rare variants to running association tests.

### Common commands I always forget

Set up job:

```python
import hailtop.batch as hb

b = hb.ServiceBackend(
        billing_project=get_config()['hail']['billing_project'],
        remote_tmpdir=remote_tmpdir(),
    )
batch = hb.Batch('CellRegMap pipeline', backend=sb)
```

CPG Hail Batch utils:

```python
from cpg_utils.hail_batch import (
    copy_common_env,
    dataset_path,
    get_config,
    init_batch,
    output_path,
    remote_tmpdir,
)
```

Explain below what each of this is good for.

### Other

In the future, I may want to adapt [Konrad K's SAIGE on UKBB exmples workflow](https://github.com/Nealelab/ukb_exomes) to running the new Poisson version of SAIGE on scRNA-seq + WGS data from TenK10K.


