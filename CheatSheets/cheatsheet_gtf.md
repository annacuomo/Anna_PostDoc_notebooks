# convert gtf file (gencode gene annotation)

ref: # https://www.biostars.org/p/272889/

```R
gtf_file = "/reference_data/gencode.v44.basic.annotation.gtf"
library(data.table)
genes <- fread(gtf_file)
setnames(genes, names(genes), c("chr","source","type","start","end","score","strand","phase","attributes") )

# [optional] focus, for example, only on entries of type "gene", 
# which will drastically reduce the file size
genes <- genes[type == "gene"]
head(genes)

# the problem is the attributes column that tends to be a collection
# of the bits of information you're actually interested in
# in order to pull out just the information I want based on the 
# tag name, e.g. "gene_id", I have the following function:
extract_attributes <- function(gtf_attributes, att_of_interest){
  att <- strsplit(gtf_attributes, "; ")
  att <- gsub("\"","",unlist(att))
  if(!is.null(unlist(strsplit(att[grep(att_of_interest, att)], " ")))){
    return( unlist(strsplit(att[grep(att_of_interest, att)], " "))[2])
  }else{
    return(NA)}
}

# this is how to, for example, extract the values for the attributes of interest (here: "gene_id")
genes$gene_id <- unlist(lapply(genes$attributes, extract_attributes, "gene_id"))
genes$gene_name <- unlist(lapply(genes$attributes, extract_attributes, "gene_name"))
genes$gene_type <- unlist(lapply(genes$attributes, extract_attributes, "gene_type"))
genes$gene_type = gsub(";","",genes$gene_type)
head(genes)

genes$gene_ids = gsub("\\..*","",genes$gene_id)

output_file = gsub(".gtf","_df.txt",gtf_file)
fwrite(genes, output_file)
```
