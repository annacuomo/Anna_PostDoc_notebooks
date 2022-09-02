## Hail

[Hail](https://hail.is/) used at Broad and CPG, python-based by with its own object types and syntax.

The following commands read in a hail table and hail matrix table, respectively"
```
import hail as hl
ht = hl.read_table(my_object.ht)
mt = hl.read_matrix_table(my_object.mt)
```
Not super sure of the difference yet, tables should be "easier"? About variants only rather than variable and samples?

### Recurring commands 

#### filter to this sample's non-ref calls
```
mt = hl.variant_qc(mt)
mt = mt.filter_rows(mt.variant_qc.n_non_ref > 0)
```
filter mt1 based on rows from mt2
```
mt1_with_mt2_rows_only = mt1.semi_join_rows(mt2.rows())
```

### Plotting
For plotting, see examples [here](https://github.com/populationgenomics/tob-wgs/tree/rare-variant-association/scripts/rv_expression_association/plot), note the
* actual plotting script (s)
* README to specify running commands using the analysis-runnrt

Plots then appear in the broswe, like in this [example](https://test-web.populationgenomics.org.au/tob-wgs/plot/v0/histogram_maf_post_filter.png)

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
