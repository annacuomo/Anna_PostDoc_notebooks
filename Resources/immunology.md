# Overview
I know very little about immunology, so just learning stuff and writing things I learn / need to remember as I go.

From [wiki](https://en.wikipedia.org/wiki/Haematopoiesis):
![image](https://user-images.githubusercontent.com/25035866/213349144-120e539b-7483-4a26-a094-fa0fd1817edd.png)

* Lymphocyes include T and B cells, NK cells other?
* Myeloid cells
* Red blood cells

# Cell types

## Monocytes
* CD14 positive (and negative CD16) monocytes are also called classical monocytes (MonoC): CD14++CD16--
* CD16 positive (and negative CD14) monocytes are also called non-classical monocytes (MonoNC): CD16++CD14--
* Intermediate monocytes have high levels of CD14 and low (but positive) levels of CD16: CD14++CD16+

## T cells

Main categories:

* Helper T-cells = CD4+ T-cells
  * TH1, TH2
* Cytotoxic T-cells = CD8+ T-cells
* Regulatory T-cells = T-regs

Other (?):

* Memory T-cells?
* NKT-cells?


## B cells
* Naive
* Memory

# Markers to annotate cell types

First distinction: myeloid vs lymphoid

Myeloid cells are CD33+

## Collection(s) of immune cell type gene markers

PBMC cell type gene markers from [Seurat tutorial](https://satijalab.org/seurat/articles/pbmc3k_tutorial.html):

* Naive CD4+ T
  * IL7R, CCR7
* CD14+ Mono
  * CD14, LYZ	      
* Memory CD4+
  * IL7R, S100A4 
* B 	  
  * MS4A1
* CD8+ T
  * CD8A	
* FCGR3A+ Mono          
  * FCGR3A, MS4A7	
* NK 
  * GNLY, NKG7
* DC
  * FCER1A, CST3
* Platelet
  * PPBP	          

# Resources
Cell type gene markers: https://www.rndsystems.com/resources/cell-markers/immune-cells/
