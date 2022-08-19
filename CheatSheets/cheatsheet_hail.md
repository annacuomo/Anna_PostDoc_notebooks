## Hail

[Hail](https://hail.is/) used at Broad and CPG, ..

### Recurring commands 

#### filter to this sample's non-ref calls
```
import hail as hl
mt = hl.variant_qc(mt)
mt = mt.filter_rows(mt.variant_qc.n_non_ref > 0)
```
filter mt1 based on rows from mt2
```
mt1_with_mt2_rows_only = mt1.semi_join_rows(mt2.rows())
```

### Example / template scripts

#### Matt
* https://github.com/populationgenomics/automated-interpretation-pipeline/blob/main/reanalysis/annotation.py
* https://github.com/populationgenomics/automated-interpretation-pipeline/blob/main/reanalysis/hail_filter_and_label.py
* https://github.com/populationgenomics/rare-disease/blob/main/data_transfer/subset_matrix_table.py
* https://github.com/populationgenomics/rare-disease/blob/validation/validation/mt_to_vcf.py
* https://github.com/populationgenomics/automated-interpretation-pipeline/blob/main/reanalysis/interpretation_runner.py

#### Kat
* https://github.com/populationgenomics/tx-adapt/blob/vep/vep/run_vep.py
* https://github.com/populationgenomics/tob-wgs/blob/run_only_existing_files/scripts/eqtl_hail_batch/conditional_analysis.py

### Resources

* [Hail webpage](https://hail.is/)
* [Hail docs](https://hail.is/docs/0.2/index.html)
* [Discuss.hail](https://discuss.hail.is/)
* [Zulip](https://hail.zulipchat.com/login/)
* [Kat's hail batch scripts](https://github.com/populationgenomics/ancestry/tree/main/scripts/hail_batch/)
* [MatrixTable Cheat Sheet](https://hail.is/docs/0.2/_static/cheatsheets/hail_matrix_tables_cheat_sheet.pdf)
* [Hail tutorials](https://hail.is/docs/0.2/tutorials-landing.html)
