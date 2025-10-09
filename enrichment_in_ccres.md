# Enrichment of METR eVariants in characterised cCREs from Cherry et al. (2020), Wang et al (2022), ENCODE and EpiMap 

## Introduction

We wanted to calculate if our eQTL variants were enriched in known regulatory elements.
To do this we calculated the number of eQTL variants which overlapped with known candidate cis-regulatory elements from different cell/tissue types divided by the number of non-eQTL variants from the METR cohort with a similar allele frequency and proximity to gene TSSs. 
We used bootstrapping to calculate 95% confidence intervals and to calculate significance.

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

## Results

METR-eVariants were enriched in cell-type agnostic promoters (`p= 8.05×10-19`) and proximal enhancers (`p = 8.48×10-26`), compared to control variants matched for allele frequency and gene density.
There was no enrichment of eVariants in distal enhancers, CTCF binding sites or DNase-H3K4me3 sites (Figure 1).

When stratified by cell-specific regulatory regions, bootstrapping analysis indicated a significant enrichment of METR-eVariants in NSR-specific (`p-value = 4.52×10-28`) and RPE-specific cCREs (`p-value = 8.74×10-10`) from Cherry et al. (2020) compared to control variants matched for allele frequency and gene density (number of gene TSSs within 1Mb of variant).

Moreover, when comparing the overlap of METR-eQTL variants to scATACseq peaks from Wang et al. (2023), we observed an enrichment of METR-eQTL variants in chromatin-accessible regions from all the retina cell types we queried: rod cells (`p-value = 6.69 ×10-58`), cone cells (`p-value = 6.58 ×10-57`), astrocytes (`p-value = 7.78 ×10-25`), horizontal cells (`p-value = 2.31 ×10-21`) retinal ganglion cells (`p-value = 2.21 ×10-20`), Muller glia (`p-value = 5.35 ×10-19`), bipolar cells (`p-value = 7.02 ×10-18`) and amacrine cells (`p-value = 2.08 ×10-6`).

Additionally, non-eye cCREs from adult tissues in EpiMap were also enriched for METR-eVariants, although the enrichment was lower than in the NSR and RPE (Figure 3B). 

