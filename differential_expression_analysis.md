# Gene Ontology terms enriched in differentially expressed genes in the neurosensory retina and retinal pigment epithelium

## Introduction
Following the deseq and edgeR analysis to identify [differentially expressed genes in the NSR and RPE](notes_on_deseq.md) (n = 14,957 differentially expressed genes identified by deseq, of which 7,353 were upregulated in the RPE compared to NSR and 7,604 were downregulated in the RPE compared to the NSR), we wanted to identify what gene ontology biological pathways were enriched in the upregulated genes in each tissue. 

## Methods
To carry out this analysis, I utilised WebGestalt's R API. I ran a Gene Set Enrichment Analysis of the gene ontology biological process terms for the differntially expressed genes between RPE and NSR. The list of differentially expressed genes was used as input, alongside the log2 fold change associated with each gene. The following code was used to run the enrichemnt analysis:

```R
input_table = read.csv("RPE_vs_NSR_DESEQ_results_all.csv", header = TRUE, sep = ',')
filter_table = input_table[input_table$padj < 0.05,]

gene_ids_no_suffix = sapply(strsplit(filter_table$X, "\\."), `[`, 1)
gene_ranks = data.frame(
  ensembl_gene_id =gene_ids_no_suffix,
  score =  filter_table$log2FoldChange,
 stringsAsFactors = FALSE
)

# Run GSEA for GO Biological Process
res <- WebGestaltR(
  enrichMethod      = "GSEA",
  organism = "hsapiens",
  enrichDatabase    = "geneontology_Biological_Process",
  interestGene      = gene_ranks,
  interestGeneType  = "ensembl_gene_id",
  fdrMethod         = "BH",
  sigMethod         = "fdr",
  sigValue          = 0.05,
  minNum            = 10,
  maxNum            = 500,
  isOutput          = FALSE   # don't generate HTML report
)
```

As the input table log2 fold change values were relative to the RPE, the output was a table with the GO biological process terms enriched in upregulated genes in the RPE (`enrichment score > 0`) and in upregulated genes in the NSR (`enrichment score < 0`).

The output of WebGestalt was then processed through `rrvgo`, an R package used to calculate the semantic similarity between a set of gene ontology terms, which can be used to cluster similar terms together and select a single representative term for each cluser. The clustering threshold was originally set at 0.7 (medium). 

## Results

987 GO BP terms were enriched in genes upregulated in the RPE (`FDR < 0.05`) and 238 GO BP terms were enriched in the NSR. 

### Gene Ontology Biological Process Terms enriched in RPE

The 987 GO biological process terms enriched in the RPE were grouped into 55 clusters (clustering threshold = 0.8) with `rrvgo` [Fig 1](fig1). The significance of each cluster can be described using two metrics: the overall number of GO terms assigned to it (size) and the minimum adjusted p-value of the GO terms within it (min p-value). 

![fig1]('images/RPE_GO_BP_clusters_freq.png')
