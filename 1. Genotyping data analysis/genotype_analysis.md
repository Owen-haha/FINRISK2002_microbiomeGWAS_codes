## 1. Imputation

**Pre-imputation quality control**

Samples with call rate <95%, sex discrepancies, excess heterozygosity and non-European ancestry were excluded. Variants with call rate <98%, deviation from Hardy-Weinberg Equilibrium (p<1×10-6), and minor allele count <3 were filtered. 

**Pre-phased

Before imputation, the genotyping data was pre-phased by using Eagle2 v2.3 (https://alkesgroup.broadinstitute.org/Eagle/). 


The imputation was performed by using IMPUTE2 v2.3.0 (http://mathgen.stats.ox.ac.uk/impute/impute_v2.html).

The reference panels was described in https://doi.org/10.1038/s41591-020-0800-0, which included 2,690 high-coverage whole-genome sequencing and 5,092 whole-exome sequencing samples. 

Imputed SNPs with INFO >0.7 were kept for further analysis.

## 2. Quality control after imputation

Plink v2.0 (https://www.cog-genomics.org/plink/2.0/) was used for the genotype data process after imputation.

**Format conversion**
From IMPUTE2 output .bz files to Plink files.

**SNP**


**Sample**

Full Plink command lines:

## 3. Principle component analysis

The genetic principle component analysis was conducted by using FlashPCA v2.0 (https://github.com/gabraham/flashpca).

LD-filtering

Remove Chromosome 6 HLA regions (GRch38)



## 4. Functional annotation of SNPs

ANNOVAR v2018Apr16 (https://annovar.openbioinformatics.org/en/latest/) was used to annotate SNPs of interst.


_Sex chromosomes (X and Y) were not considered in the projects._
