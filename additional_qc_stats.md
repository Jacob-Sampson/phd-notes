# Relationship between RNA integrity number and other RNASeq QC metrics

## Introduction

The METR-GT cohort has a relativley high PMI time (median = 40 hours). Therefore, we wanted to investigate whether this could compromise measures of RNA integrity (RNA Integrity Number) and other RNA sequencing QC metrics (such as 3'/5' bias or read length).

## Results

The median RNA Integrity number for NSR samples is ##, and for RPE is ##. The RIN is greater than 7 for ## NSR samples and ## RPE samples.
To investigate if 5' bias could impact our results, we used the 3'/5' bias metric from RNASeQC. According to their documentation (https://github.com/getzlab/rnaseqc/blob/master/Metrics.md), this metric captures the ratio of sequencing depth between the 3' end of the gene (150 bp region) and the 5' end of the gene (150 bp region) for genes with a length greater than 600 bp and with at least 5 unambiguous reads.
A gene with even coverage in both its 3' and 5' windows will have a bias of 0.5, values near 1 or 0 indicate degradation.


