## 1. Genotype imputation

**Pre-imputation quality control**

Samples with call rate <95%, sex discrepancies, excess heterozygosity and non-European ancestry were excluded. Variants with call rate <98%, deviation from Hardy-Weinberg Equilibrium (p<1×10-6), and minor allele count <3 were filtered. 

**Pre-phased**

Before imputation, the genotyping data was pre-phased by using Eagle2 v2.3 (https://alkesgroup.broadinstitute.org/Eagle/). 

**Imputation**

The imputation was performed by using IMPUTE2 v2.3.0 (http://mathgen.stats.ox.ac.uk/impute/impute_v2.html).

The reference panels was described in https://doi.org/10.1038/s41591-020-0800-0, which included 2,690 high-coverage whole-genome sequencing and 5,092 whole-exome sequencing samples. 

Imputed SNPs with INFO >0.7 were kept for further analysis.

## 2. Quality control after imputation

Plink v2.0 (https://www.cog-genomics.org/plink/2.0/) was used for the genotype data process after imputation.

Format conversion: from IMPUTE2 output .gen/.bgen files to Plink files

SNP filtering: call rate >90%, no significant deviation from Hardy-Weinberg Equilibrium (p>1.0×10-6), and minor allele frequency >1%

Sample filtering: >10% missing rate were removed

Full Plink command lines: ```plink2  --gen chr10.gen.gz --sample chr10.samples --out fr02_chr10  --threads 8 --snps-only --geno 0.1 --hwe 1e-6 --maf 0.01 --import-dosage-certainty 0.9 --make-bed --oxford-single-chr 10```

## 3. Principle component analysis (PCA)

The genetic principle component analysis was conducted by using FlashPCA v2.0 (https://github.com/gabraham/flashpca).

LD-filtering: 

Remove Chromosome 6 HLA regions (GRch38):

Run PCA: 

## 4. Functional annotation of SNPs

ANNOVAR v2018Apr16 (https://annovar.openbioinformatics.org/en/latest/) was used to annotate SNPs of interst.



_Sex chromosomes (X and Y) were not considered in the projects._
