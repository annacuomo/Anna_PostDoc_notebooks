# Hail

[Hail](https://hail.is/) used at Broad and CPG, python-based but with its own object types and syntax.

The following commands read in a hail table and hail matrix table, respectively"
```
import hail as hl
ht = hl.read_table(my_object.ht)
mt = hl.read_matrix_table(my_object.mt)
```
As it turns out, a variant-specific ```Table``` is obtained by running 
```
variant_table = mt.rows()
``` 
retaining site-level data and annotations. 

Similarly, one could run 
```
sample_table = mt.cols()
```
which would retain sample-level data and annotations.

## Recurring commands 

### filter to this sample's non-ref calls
```
mt = hl.variant_qc(mt)
mt = mt.filter_rows(mt.variant_qc.n_non_ref > 0)
```
### filter mt1 based on rows from mt2
```
mt1_with_mt2_rows_only = mt1.semi_join_rows(mt2.rows())
```

### filter mt to a range
```
gene_interval = 'chr1:156053680-156053690'  
mt0 = hl.filter_intervals(mt, [hl.parse_locus_interval(gene_interval, reference_genome='GRCh38')])
```

### using Matt's script to copy subsets of hail tables / matrix tables to test

From my own copy of [the scripts folder in analysis runner](https://github.com/populationgenomics/analysis-runner/tree/main/scripts), run

For Hail Table - HT - objects: 
```
analysis-runner --dataset tob-wgs \
    --description "subset vep annotated ht" \
    --output-dir "tob_wgs_rv" --access-level standard \
    python3 subset_hail_table.py -i gs://cpg-tob-wgs-main/tob_wgs_vep/104/vep104.3_GRCh38.ht \
    --chr chr22 --pos 23702743-23804425 --out VPREB3_50K_window_vep
```

For (Hail) Matrix Table - MT - objects: 
```
analysis-runner --dataset tob-wgs \
    --description "subset mt to chr1 only" \
    --output-dir "tob_wgs_rv" --access-level standard \
    python3 subset_matrix_table.py -i gs://cpg-tob-wgs-main/mt/v7.mt  \
    --chr chr1 --out v7_chr1_copy
```

## Plotting
For plotting, see examples [here](https://github.com/populationgenomics/tob-wgs/tree/rare-variant-association/scripts/rv_expression_association/plot), note the
* actual plotting script (s)
* README to specify running commands using the analysis-runnrt

Plots then appear in the broswe, like in this [example](https://test-web.populationgenomics.org.au/tob-wgs/plot/v0/histogram_maf_post_filter.png)

## Example / template scripts

### Matt
* https://github.com/populationgenomics/automated-interpretation-pipeline/blob/main/reanalysis/annotation.py
* https://github.com/populationgenomics/automated-interpretation-pipeline/blob/main/reanalysis/hail_filter_and_label.py
* https://github.com/populationgenomics/rare-disease/blob/main/data_transfer/subset_matrix_table.py
* https://github.com/populationgenomics/rare-disease/blob/validation/validation/mt_to_vcf.py
* https://github.com/populationgenomics/automated-interpretation-pipeline/blob/main/reanalysis/interpretation_runner.py

### Kat
* https://github.com/populationgenomics/tx-adapt/blob/vep/vep/run_vep.py
* https://github.com/populationgenomics/tob-wgs/blob/run_only_existing_files/scripts/eqtl_hail_batch/conditional_analysis.py

## Resources

* [Hail webpage](https://hail.is/)
* [Hail docs](https://hail.is/docs/0.2/index.html)
* [Discuss.hail](https://discuss.hail.is/)
* [Zulip](https://hail.zulipchat.com/login/)
* [Kat's hail batch scripts](https://github.com/populationgenomics/ancestry/tree/main/scripts/hail_batch/)
* [MatrixTable Cheat Sheet](https://hail.is/docs/0.2/_static/cheatsheets/hail_matrix_tables_cheat_sheet.pdf)
* [Hail tutorials](https://hail.is/docs/0.2/tutorials-landing.html)
