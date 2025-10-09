# Comparison between METR-eQTL dataset and eQTLs from Stunz et al. (2020)

## Introduction

Following comments by the reviewers of our manuscript, we thought it would be appropriate to extend the METR eQTL comparison to an additional retina eQTL study by Strunz et al. (2020).

## Methods

We downloaded eQTLs from Strunz et al. here: https://myfiles.uni-regensburg.de/ssf/s/readFile/share/37554/1498947399071012793/publicLink/Retina_merged3_hg38_FastQTL_eVariants_chrALL_FDR_0.05.txt 

We intersected the eGenes and eVariants from Strunz with METR-NSR eQTLs. To intersect eVariants we used dbSNP rsIDs.
For eGenes shared between METR-NSR and Stunz we proceeded to determine if the eGenes shared the top eVariant or if the top METR eVariant was in high LD with the top Strunz eVariant (`r2 > 0.8`). 

## Results

### Description of Strunz et al. eQTLs

