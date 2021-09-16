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

Plink can do format conversion, SNP filtering and sample filtering at one command line.

Format conversion: from IMPUTE2 output .gen/.bgen files to Plink files

SNP filtering: call rate >90%, no significant deviation from Hardy-Weinberg Equilibrium (p>1.0×10-6), and minor allele frequency >1%

Sample filtering: >10% missing rate were removed

Full Plink command line: ```plink2  --gen chr10.gen.gz --sample chr10.samples --out fr02_chr10  --threads 8 --snps-only --geno 0.1 --hwe 1e-6 --maf 0.01 --import-dosage-certainty 0.9 --make-bed --oxford-single-chr 10```

The input _chr10.samples_ is a three coloumn files (blank-seperated), where the first two rows are fixed.
```ID1 ID2 missing
0 0 0
FID1 FID1 0
FID2 FID2 0
```

## 3. Principle component analysis (PCA)

The genetic principle component analysis was conducted by using FlashPCA v2.0 (https://github.com/gabraham/flashpca).

LD-filtering: many SNPs are highly assocaited (in linkage disequilibrium), the PCA is only calculated from a subset of them after LD-filtering.

Remove long-range LD regions: some genomic regions have long-range LD which will bias the analysis.

_LongRangeLDRegions.txt_ (coordinations are based on reference genome GRch38, plink-friendly file format):
```
1 47534328 51534328 region1
2 133742429 137242430 region2
2 182135273 189135274 region3
3 47458510 49962567 region4
3 83450849 86950850 region5
5 98664296 101164296 region6
5 129664307 132664308 region7
5 136164311 139164311 region8
6 24999772 33532223 region9
6 139678863 142178863 region10
8 8142478 12142491 region11
11 87789108 90766832 region12
12 109062195 111562196 region13
20 33412194 35912078 region14
2 86000000 100500000 region15
3 89000000 97500000 region16
5 44000000 51500000 region17
6 57000000 64000000 region18
7 55000000 66000000 region19
8 43000000 50000000 region20
10 37000000 43000000 region21
11 45000000 57000000 region22
12 33000000 40000000 region23
```

Plink commands for LD-filtering and remove long-range LD regions (take chr10 as example): ```plink2 --gen chr10.gen.gz --sample chr10.samples --out chr10  --threads 8 --snps-only --geno 0.1 --hwe 1e-6 --maf 0.01 --import-dosage-certainty 0.999999 --make-bed --oxford-single-chr 10 --indep-pairwise 1000 80 0.6 --exclude range LongRangeLDRegions.txt```

Run PCA: ```flashpca_x86-64 --bfile fr02_all_rmLrld_pruned_r01 --suffix _rmLrld_pruned_r01.txt```

## 4. Functional annotation of SNPs

ANNOVAR v2018Apr16 (https://annovar.openbioinformatics.org/en/latest/) was used to annotate SNPs of interst.

Commands:

```
perl annotate_variation.pl -geneanno -dbtype refGene -buildver hg38 SNP_avinput path_to_annova_humandb
perl annotate_variation.pl -regionanno -dbtype cytoBand -buildver hg38 SNP_avinput path_to_annova_humandb
```
_path_to_annova_humandb_ is the path of ANNOVAR installed folder.

The fist command is to add gene (functional) information for input SNPs.

The second command is to add cytoBand information for input SNPs.


# :thought_balloon: **_Sex chromosomes (X and Y) were not considered throughout the project_** :thought_balloon:
