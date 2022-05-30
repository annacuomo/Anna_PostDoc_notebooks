## Curating a database for single-cell eQTL studies.

Idea: equivalent to Valentine Svennson's [database of single-cell studies](https://www.nxn.se/single-cell-studies), but for (single-cell) eQTL studies specifically.

Starting this [here](https://docs.google.com/spreadsheets/d/1xlqeol6cuSTHsJs_IG2sAiawZX4M6Rwxubh7VKEBj0U/edit#gid=0), current fields:

```
Date, Shorthand, DOI, Reported unique individuals, Reported total cells, Pseudobulk [y/n],	Dynamic eQTL [y/n], scRNA-seq technique, eQTL mapping method, article type, Authors, Journal, bioRxiv DOI, bioRxiv Date, Tissue, Organism, Title.
```

Current count: n=18, spanning 2018-2022.

## Open in python:

```
import pandas as pd
data = pd.read_csv('https://nxn.se/single-cell-studies/data.tsv', sep='\t')
```

### Discussion point: which fields?
```
data.columns
Index(['Shorthand', 'DOI', 'Authors', 'Journal', 'Title', 'Date',
       'bioRxiv DOI', 'Reported cells total', 'Organism', 'Tissue',
       'Technique', 'Data location', 'Panel size', 'Measurement',
       'Cell source', 'Disease', 'Contrasts', 'Developmental stage',
       'Number of reported cell types or clusters', 'Cell clustering',
       'Pseudotime', 'RNA Velocity', 'PCA', 'tSNE', 'H5AD location',
       'Isolation', 'BC --> Cell ID _OR_ BC --> Cluster ID',
       'Number individuals'],
      dtype='object')
```

### Discussion point: is there a convention for journal names?
```
data['Journal'].unique()
array(['Proceedings of the National Academy of Sciences', 'Cell',
       'Neuron', 'Cerebral Cortex', 'Nucleic Acids Research',
       'Neuroscience Research', 'BMC Genomics', 'Journal of Neuroscience',
       'Nat Methods', 'Developmental Cell', 'Cell Stem Cell',
       'Genome Research', 'PLoS ONE', 'Nat Biotechnol', 'Dev. Dyn.',
       'Cell Reports', 'Nat Cell Biol', 'Genome Biol', 'Nature',
       'Nat Struct Mol Biol', 'Science', 'bioRxiv', 'Development',
       'Genome Res.', 'Nat Neurosci', 'The EMBO Journal',
       'Mol Psychiatry', 'Current Biology', 'Molecular Cell',
       'Proc Natl Acad Sci USA', 'Molecular Systems Biology',
       'Nat Immunol', 'Thorax', 'Methods', 'Nat Commun', 'GigaSci',
       'EMBO Rep', 'Cell Res', 'Immunol Cell Biol', 'Hum. Reprod.',
       'Cancer Discovery', 'eLife', 'Cell Discov', 'Blood', 'Diabetes',
       'Endocrinology', 'JCI Insight', 'Cell Systems', 'Cell Metabolism',
       'J. Exp. Med.', 'Nat Genet', 'Sci Rep', 'Nat Microbiol',
       'Nucleic Acids Res', 'Mol Syst Biol', 'Cancer Cell',
       'Science Immunology', 'PLoS Biol', 'Sci. Immunol.',
       'Cancer Discov', 'BMC Biol', 'J.I.', 'Nature Plants',
       'Protein Cell', 'Journal of Clinical Investigation',
       'Front. Cell. Neurosci.', 'Hepatology', 'Front. Endocrinol.',
       'Sci Data', 'JASN', 'Molecular Therapy',
       'The American Journal of Human Genetics', 'Circ Res',
       'Developmental Biology', 'Stem Cell Reports', 'iScience',
       'J. Neurosci.', 'Bioinformatics', 'Nat Biomed Eng', 'Immunity',
       'Nat Med', 'Journal of Investigative Dermatology', 'Ann Rheum Dis',
       'Genome Med', 'PLoS Genet', 'acta neuropathol commun', 'EMBO Rep.',
       'Blood Adv', 'GigaScience', 'Genes Dev.', 'Cancer Commun',
       'EMBO J.', 'Front. Immunol.', 'Gastroenterology', 'J. Biol. Chem.',
       'Stem Cells', 'Am J Respir Crit Care Med',
       'Journal of Molecular Cell Biology', 'Blood Cancer Journal',
       'Mucosal Immunol', 'Am J Respir Cell Mol Biol',
       'Journal of Allergy and Clinical Immunology', 'Aging Cell',
       'Alcohol Clin Exp Re', 'European Heart Journal', 'J Virol',
       'Experimental Eye Research', 'Sci. Transl. Med.', 'IJMS',
       'Sci. Adv.', 'Nat Protoc', 'Circulation', 'J Neuroinflammation',
       'J Ovarian Res',
       'Cellular and Molecular Gastroenterology and Hepatology',
       'Theranostics', 'Mol Reprod Dev', 'Invest. Ophthalmol. Vis. Sci.',
       'Circulation Research', 'EMBO rep', 'Briefings in Bioinformatics',
       'Alz Res Therapy', 'EMBO J', 'FEBS Lett', 'Cytometry',
       'Br J Haematol', 'J Dent Res', 'Cytogenet Genome Res',
       'Genes Cells', 'Front. Cell. Infect. Microbiol.',
       'Journal of Experimental Medicine', 'Plant and Cell Physiology',
       'Biology Methods and Protocols', 'Front. Mol. Neurosci.',
       'Nat Metab', 'Neuroscience', 'Science Bulletin', 'eNeuro',
       'Bioscience, Biotechnology, and Biochemistry', 'EMBO Mol Med',
       'Glia', 'NAR Genomics and Bioinformatics', 'Nat. Nanotechnol.',
       'medRxiv', 'Cells', 'Cancer Res', 'Cancer Letters',
       'Cold Spring Harb Mol Case Stud', 'Nat Cancer', 'npj Genom. Med.',
       'J Leukoc Biol', 'Int J Oral Sci', 'Environ. Sci. Technol.',
       'PLoS Pathog', 'EBioMedicine', 'Human Gene Therapy',
       'OncoImmunology', 'Small', 'Cell. Mol. Life Sci.',
       'J Neurosci Res', 'Commun Biol', "Journal of Crohn's and Colitis",
       'OMICS: A Journal of Integrative Biology', 'Cancers',
       'Blood Advances', 'Cardiovascular Research', 'Kidney360',
       'Intensive Care Med',
       'Biochemical and Biophysical Research Communications',
       'Neurobiology of Disease', 'Front. Cell Dev. Biol.',
       'National Science Review', 'Journal of Hepatology',
       'STAR Protocols', 'Clinical and Translational Medicine',
       'Cell Tissue Res', 'Life Sci. Alliance', 'Micromachines',
       'Cell Mol Immunol', 'Biotechnol Lett',
       'Emerging Microbes & Infections', 'Shock',
       'Journal of Autoimmunity', 'Clin. Transl. Immunol.', 'ATVB',
       'Arthritis Res Ther', 'Proteomics', 'Front. Plant Sci.',
       'Cell Reports Medicine', 'The Ocular Surface', 'Cell Biosci',
       'The Plant Cell', 'Biomolecules', 'Acta Neuropathol',
       'Genomics, Proteomics & Bioinformatics', 'FASEB j.',
       'Cell Death Dis', 'Research Square', 'RSquare',
       'Breast Cancer Res', 'Cell Death Discov.', 'Oncogene', 'Genomics',
       'J Cereb Blood Flow Metab', 'Journal of Biological Chemistry',
       'J Immunother Cancer', 'EMBO Reports', 'eBioMedicine',
       'Sci. Signal.', 'Int. J. Biol. Sci.', 'Bioscience Reports',
       'Stem Cell Res Ther', 'Hepatol Commun', 'Cancer Prev Res', 'Brain',
       'mBio', 'Small Methods', 'Front. Neurol.', 'Cell Insight',
       'Human Molecular Genetics', 'mSphere', 'Hypertension',
       'Front. Genet.', 'Front. Cardiovasc. Med.'], dtype=object)
   ```
   
## References
[A curated database reveals trends in single-cell transcriptomics](https://academic.oup.com/database/article/doi/10.1093/database/baaa073/6008692)
