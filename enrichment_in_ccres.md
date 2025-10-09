# Enrichment of METR eVariants in characterised cCREs from Cherry et al. (2020), Wang et al (2022), ENCODE and EpiMap 

## Introduction

## Methods

### cCRE datasets

| Dataset | Description | 
| ------- | ----------- |
| Cherry et al. (2020) | cCREs in retina and RPE calculated by intersecting bulk ATACseq with H3K27ac ChIPseq. |
| Wang et al. (2022) | Regions of accessible chromatin from Retina scATACseq, comprising 8 different retina cell types |
| EpiMap | Tissue specific cCREs from 18 different adult tissue types. |
| ENCODE | Cell type agnostic regulatory elements, classified into promoters, proximal/distal enhancers, CTCF-only and poised cCREs |

To calculate the relative enrichment of eVariants which overlapped with each type of regulatory element, we used bootstrapping analysis.
We carried out 1,000 subsampling iterations.
For each iteration, 100,000 eVariants were randomly selected with replacement.
We then matched each eVariant with another non-eQTL variant from our cohort that had a similar allele frequency and gene density (number of gene TSSs within 1Mb of the variant).
Each subset of eVariants and matched control variants was intersected with the cCRE datasets described above using BEDtools (Quinlan and Hall, 2010).

We then calculated the relative enrichment as the ratio of eVariants to control variants which overlapped each type of cCRE.
For each cCRE type we then calculated the mean relative enrichment and the 95% confidence interval. If there was no relative enrichment, we would expect the mean score to equal 1. Therefore, to calculate significance p-values from the bootstrapped results we created a null distribution where mean = 1 and std. deviation = std. deviation of the bootstrapped result set. We then calculated the Z-score between the observed bootstrapped mean and the mean of the null distribution.
