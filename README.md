# cseaR
Cell type enrichment analysis borrowing functions from pSI, EWCE, and phenoTest R packages.

## About this package
cseaR includes code/workflow (Rmd) and pre-processed cell data for human analysis

## The CSEA methods I use are:
  * pSI R package (a "competitive" enrichment) - with list of significant (e.g. FDR < 0.05) genes
  * EWCE R package (a "summed" enrichment) - with list of significant (e.g. FDR < 0.05) genes 
  * GSEA function from phenoTest R package modified for CSEA - with full ranked t-statistics (gam error, bypassed by doing 10 genesets at a time; SUB-ideal!)

## The cell datasets I use are:
  * Darmanis Human SCT (based on data from Andrew Jaffe)
  * Lake Human SCT (Neuron subtypes) 
  * Barres Human RNA-Seq from sorted cells (pSI only since not SCT)
  * Linnarsson Mouse SCT (Celltypes and extensive subtypes -- Neuron human~mouse agreement is pretty good but glia not so much) 
  * Barres Mouse RNA-Seq from sorted cells (for mouse experiments) (pSI only since not SCT)

## Details about cell datasets

### [Darmanis, et al PNAS 2015 - Human SCT](http://www.pnas.org/content/112/23/7285.long) 

### Linnarsson: [Zeisel, et al. Science 2015 - Mouse SCT](http://science.sciencemag.org/content/early/2015/02/18/science.aaa1934)   
  * Data downloaded from [website](http://linnarssonlab.org/blobs/cortex/expression_mRNA_17-Aug-2014.txt). 

### Ben Barres - Mouse and Human (not SCT)  
[Downloaded 7/4/2016](http://web.stanford.edu/group/barres_lab/brainseq2/brainseq2.html)   
Average taken for replicates  

#### [Human RNA-Seq](http://www.cell.com/neuron/abstract/S0896-6273(15)01019-3)  
  
#### [Mouse RNA-Seq](http://www.jneurosci.org/content/34/36/11929.short)  

### [Lake et al Science 2016 - Human SCT](http://science.sciencemag.org/content/352/6293/1586)   
  * Part of [SCAP-T](http://www.scap-t.org)  
  * [README](http://genome-tech.ucsd.edu/public/Lake_Science_2016)
  * Data
    + Summarized data available publically [online](http://genome-tech.ucsd.edu/public/Lake_Science_2016)
    + Full raw data available at dbGaP (accession phs000833.v4.p1)
  * Tissue = 6 cortical regions: FC (BA8, BA10), TC (BA21, BA22, BA41), and VC (BA17)  
    + BA8 = frontal cortex (FC)  
    + BA10 = anterior pre-frontal cortex (PFC)  
    + BA17 = visual cortex in occipital lobe (VC)    
    + BA21 = middle temportal cortex; auditory (mTC)    
    + BA22 = superior temporal cortex; auditory (sTC)  
    + BA41 = anterior transverse temporal gyrus (aTC) 
  * Selection = NeuN+ nuclei from normal postmortem tissue (PMI = 22hrs)  
  * # Individuals = 1 ("Patient 1568")  
  * Source = NICHD Brain and Tissue Bank for Developmental Disorders (Univ Maryland)  
  * Age = 51  
  * Sex = F   
  * Hemisphere = both (these 6 regions are known to have low inter-hemispheric differences)  
  * # Cells  --> see corrected Suppl. Methods online!  
    + From paper = 4,488 (total) --> 3,227 (filtered) 
    + From README & summary data = 4,039 (total) --> 3,083 (filtered)  
  * exprsData (TPM):  
    + Lake-2016_Gene_TPM.dat = both exon and intron reads  
    + Lake-2016_Exon_TPM.dat = exon-only reads  
  * phenoData:  
    + For 3,083 annotated single nuclei (4,039 - low mapping outliers and potential doublets)  
    + For both Gene and Exon .dat files  
    + Neuronal subtypes: excitatory (Ex1-Ex8) and inhibitory (In1-In8)  
    + BA origin  
    + dbGaP sample name  (accession# phs000833.v4.p1; raw data and additional phenoData avail for each sample is available from dbGaP.
  * Recommendations:
    + Use phenoData to subset for only 3,083 quality-filtered data sets  
    + Exclude "MT-" genes (mitochondrial) that may have randomly associated with nuclear membrane  
  * [Publically-availbable online files](http://genome-tech.ucsd.edu/public/Lake_Science_2016):
    + Lake-2016_Gene_TPM.dat (exprsData!)  
    + Lake-2016_Gene_TPM_Sample-annotation.txt (phenoData!)  
    + Lake-2016_Exon_TPM.dat  
    + Lake-2016_Exon_TPM_Sample-annotation.txt  

#### Cell breakdown

Lake | FC  | PFC  |  VC  | mTC  | sTC  | aTC  | tot. | Linn. | Cell    
Type | BA8 | BA10 | BA17 | BA21 | BA22 | BA41 |  n   | Type1 | Markers (not complete)2   
-----| ----| -----| -----| -----|------|------|------|-------|-----------------------------------------------------------------------
Ex1  |  70 |  153 |   62 |  218 |  131 |  424 | 1058 |       | CNR+, CUX2+, THSD7A+, CBLN2+  
Ex2  |  35 |   32 |    0 |   19 |    6 |    4 |   96 |       | CUX2+, RORB+, SYNPR+, THSD7A+, BHLHE22+, CBLN2+  
Ex3  |   4 |   15 |  181 |    5 |   10 |   84 |  299 |       | CUX2+, RORB+, SYNPR+, THSD7A+, BHLHE22+, SV2C~  
Ex4  |  17 |   56 |    0 |   35 |   25 |   41 |  174 |       | SLC17A7++, CNR1+, RORB+, SYNPR+, FOXP2+, GABRG1+  
Ex5  |  65 |   64 |   11 |   49 |   27 |   34 |  250 |       | SLC17A7++, RORB+, KCNK2+, FOXP2+, PCP4+  
Ex6  |  42 |   37 |   10 |   31 |   11 |    8 |  139 |       | CDH11++, SULF1+, PDE9A+, HTR2C+, SYT6+, FOXP2+, PCP4+, CBLN2+, GRM4+    
Ex7  |  21 |   37 |    1 |   29 |   17 |   10 |  115 |       | CNR1+, CBLN2+  
Ex8  |   8 |   17 |    3 |    7 |    6 |    6 |   47 |       | SYNPR++, NR4A2++, OPRK+, PDE9A+, CBLN2+, SLC6A8+, ADRA2A+, NPY1R+  
-----| ----| -----| -----| -----|------|------|------|-------|-----------------------------------------------------------------------
In1  |  34 |   41 |    6 |   17 |   18 |   44 |  160 |       | CNR1+, VIP+, RELN+, CCK+ 
In2  |   2 |   12 |    7 |    7 |    9 |   18 |   55 | ~Int6 | GAD1++, CNR1+, VIP+, OPRK1+, CCK+  
In3  |  10 |   13 |    1 |   14 |    6 |   27 |   71 |       | PDE9A+, HTR2C+, VIP+, RELN+, CCK+, CNR1~  
In4  |  37 |   25 |    9 |    9 |   14 |   27 |  121 |       | GAD1++, SV2C++, RELN+, CCK+, KCNH1+, GABRG1+, KCNAB1+, SST~, CNR~  
In5  |  22 |   10 |    2 |   11 |    9 |    8 |   62 |       | SV2C+, LHX6+, CCK+, KCNAB1+    
In6  |  77 |   18 |   16 |   37 |   18 |   73 |  239 |  Int3 | GAD1++, PVALB+, SULF1+, PDE9A+, LHX6+, ASIC2+, GRIK3+    
In7  |   4 |    6 |    3 |    5 |   10 |   34 |   62 |  Int1 | SST+, LHX6+, NPY+, GRIK3+  
In8  |  21 |   28 |   16 |   20 |   12 |   38 |  135 |  Int2 | SST+, LHX6+, CACNA1G+, RELN~  
-----| ----| -----| -----| -----|------|------|------|-------|-----------------------------------------------------------------------
n    | 564 |  328 |  513 |  329 |  880 |  469 | 3083 |       |
  
  * SLC17A7 aka VGLUT1  
  * GAD1 aka GAD67
  * 1: Source: FigS12; Linnarsson mouse data had an additional 7 RELN+ subtypes, not shown in FigS12
  * 2: Sources: FigS11, FigS12, FigS16 (red)  

