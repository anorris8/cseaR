# cseaR
Cell type enrichment analysis borrowing functions from pSI, EWCE, and phenoTest R packages.

## The CSEA methods I use are:
  * pSI R package (a "competitive" enrichment) - with list of significant (e.g. FDR < 0.05) genes
  * EWCE R package (a "summed" enrichment) - with list of significant (e.g. FDR < 0.05) genes 
  * GSEA function from phenoTest R package modified for CSEA - with full ranked t-statistics --> this is new, so if you see a typo let me know! (also I was unable to troubleshoot the gam error, so if you are able to fix that, I would be SO grateful!)

## The cell datasets I use are:
  * Darmanis Human SCT (based on data from Andrew Jaffe)
  * Lake Human SCT (Neuron subtypes) 
  * Barres Human RNA-Seq from sorted cells (pSI only since not SCT)
  * Linnarsson Mouse SCT (Celltypes and extensive subtypes -- Neuron human~mouse agreement is pretty good but glia not so much) 
  * Barres Mouse RNA-Seq from sorted cells (for mouse experiments) (pSI only since not SCT)

## About this package
It includes code/workflow (Rmd) and pre-processed cell data for human analysis

